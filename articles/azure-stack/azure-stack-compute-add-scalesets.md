---
title: 在 Azure Stack 中提供虚拟机规模集 | Microsoft Docs
description: 了解云操作员如何向 Azure Stack 应用商店中添加虚拟机规模集
services: azure-stack
author: brenduns
manager: femila
editor: ''
ms.service: azure-stack
ms.topic: article
ms.date: 05/08/2018
ms.author: brenduns
ms.reviewer: kivenkat
ms.openlocfilehash: 12425ab53ca16bb985a0a8658b5058998565b01a
ms.sourcegitcommit: fc64acba9d9b9784e3662327414e5fe7bd3e972e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2018
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>在 Azure Stack 中提供虚拟机规模集

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

虚拟机规模集是一种 Azure Stack 计算资源。 可以使用它们部署和管理一组相同的虚拟机。 由于所有虚拟机的配置都相同，因此规模集不需要预配虚拟机。 可以更方便地构建面向大型计算、大数据、容器化工作负荷的大规模服务。

本文将指导你完成在 Azure Stack Marketplace 中提供规模集的过程。 完成此过程之后，用户将可以将虚拟机规模集添加到其订阅。

Azure Stack 上的虚拟机规模集与 Azure 上的虚拟机规模集类似。 有关详细信息，请参阅以下视频：
* [Mark Russinovich talks Azure scale sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)（Mark Russinovich 谈论 Azure 规模集）
* [Guy Bowerman 介绍虚拟机规模集](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

在 Azure Stack 上，虚拟机规模集不支持自动缩放。 可以使用 Azure Stack 门户、资源管理器模板或 PowerShell 将更多实例添加到规模集。

## <a name="prerequisites"></a>必备组件
* **Powershell 和工具**

   安装并配置适用于 Azure Stack 的 PowerShell 和 Azure Stack 工具。 请参阅[在 Azure Stack 中启动并运行 PowerShell](azure-stack-powershell-configure-quickstart.md)。

   安装 Azure Stack 工具后，请确保导入以下 PowerShell 模块（路径相对于 AzureStack-Tools-master 文件夹中的 .\ComputeAdmin 文件夹）：
  ````PowerShell
        Import-Module .\AzureStack.ComputeAdmin.psm1
  ````

* **操作系统映像**

   如果尚未将操作系统映像添加到 Azure Stack 应用商店，请参阅[将 Windows Server 2016 VM 映像添加到 Azure Stack 应用商店](azure-stack-add-default-image.md)。

   若要支持 Linux，请下载 Ubuntu Server 16.04 并使用带以下参数的 ```Add-AzsPlatformImage``` 添加它：```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```。


## <a name="add-the-virtual-machine-scale-set"></a>添加虚拟机规模集

针对环境编辑以下 PowerShell 脚本，然后运行该脚本，以便将虚拟机规模集添加到 Azure Stack 应用商店。 

``$User`` 是用于连接管理员门户的帐户。 例如，serviceadmin@contoso.onmicrosoft.com。

````PowerShell  
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
````

## <a name="update-images-in-a-virtual-machine-scale-set"></a>更新虚拟机规模集中的映像 
创建虚拟机规模集之后，用户无需重新创建规模集即可更新规模集中的映像。 更新映像的过程取决于以下场景：

1. 虚拟机规模集部署模板为 *version* 指定了 **latest**：  

   如果规模集模板 *imageReference* 节中的 *version* 设置为 **latest**，则对规模集执行的纵向扩展操作将会针对规模集实例使用映像的最新可用版本。 完成纵向扩展后，可以删除旧的虚拟机规模集实例。  （*publisher*、*offer* 和 *sku* 的值保持不变）。 

   下面是指定 *latest* 的示例：  

    ```Json  
    "imageReference": {
        "publisher": "[parameters('osImagePublisher')]",
        "offer": "[parameters('osImageOffer')]",
        "sku": "[parameters('osImageSku')]",
        "version": "latest"
        }
    ```

   必须先下载新映像，然后纵向扩展才能使用新映像：  

   - 当 Marketplace 中的映像版本比规模集中的映像要新时：下载新映像来替换旧映像。 替换映像后，用户可以继续纵向扩展。 

   - 当 Marketplace 中的映像版本与规模集中的映像相同时：删除规模集中使用的映像，然后下载新映像。 在删除原始映像之后、下载新映像之前，无法执行纵向扩展。 
      
     需要执行此过程以重新合成利用稀疏文件格式（在版本 1803 中引入）的映像。 
 

2. 虚拟机规模集部署模板不会为 *version* 指定 **latest**，而是改为指定版本号：  

     如果下载较新版本的映像（会更改可用版本），则无法纵向扩展规模集。 这是设计使然，因为规模集模板中指定的映像版本必须可用。  

有关详细信息，请参阅[操作系统磁盘和映像](.\user\azure-stack-compute-overview.md#operating-system-disks-and-images)。  


## <a name="remove-a-virtual-machine-scale-set"></a>删除虚拟机规模集

若要删除虚拟机规模集库项，请运行以下 PowerShell 命令：

```PowerShell  
    Remove-AzsVMSSGalleryItem
````

> [!NOTE]
> 库项可能不会立即删除。 可能需要刷新门户几次，该项才会从 Marketplace 中删除。

## <a name="next-steps"></a>后续步骤
[Azure Stack 常见问题解答](azure-stack-faq.md)