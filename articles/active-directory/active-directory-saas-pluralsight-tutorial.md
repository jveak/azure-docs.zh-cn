---
title: 教程：Azure Active Directory 与 Pluralsight 集成 | Microsoft 文档
description: 了解如何在 Azure Active Directory 和 Pluralsight 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: jeedes
ms.openlocfilehash: ec199b665f0f9ed34ac6763855cfa9d35b80a7e2
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a>教程：Azure Active Directory 与 Pluralsight 的集成

本教程介绍了如何将 Pluralsight 与 Azure Active Directory (Azure AD) 集成。

将 Pluralsight 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 Pluralsight。
- 可以让用户通过其 Azure AD 帐户自动登录到 Pluralsight（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Pluralsight 的集成，需备齐以下项目：

- Azure AD 订阅
- 已启用 Pluralsight 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Pluralsight
2. 配置和测试 Azure AD 单一登录

## <a name="adding-pluralsight-from-the-gallery"></a>从库中添加 Pluralsight
要通过配置将 Pluralsight 集成到 Azure AD 中，需从库将 Pluralsight 添加到托管式 SaaS 应用的列表中。

**若要从库添加 Pluralsight，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中，键入“Pluralsight”，在结果面板中选择“Pluralsight”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的 Pluralsight](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，将基于一个名为“Britta Simon”的测试用户配置和测试 Pluralsight 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Pluralsight 用户。 换句话说，需要建立 Azure AD 用户与 Pluralsight 中相关用户之间的关联关系。

可通过将 Azure AD 中“用户名”的值指定为 Pluralsight 中“用户名”的值来建立此关联关系。

若要使用 Pluralsight 配置和测试 Azure AD 单一登录，需完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 Pluralsight 测试用户](#create-a-pluralsight-test-user)** - 在 Pluralsight 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Pluralsight 应用程序中配置单一登录。

**若要通过 Pluralsight 配置 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的 Pluralsight 应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![“单一登录”对话框](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. 在“Pluralsight 域和 URL”部分中，执行以下步骤：

    ![Pluralsight 域和 URL 单一登录信息](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    a. 在“登录 URL”文本框中，使用以下模式键入 URL：`https://<instancename>.pluralsight.com/sso/<companyname>`

    b. 在“标识符”文本框中，键入 URL：`www.pluralsight.com`

    c. 在“回复 URL”文本框中，使用以下模式键入 URL：`https://<instancename>.pluralsight.com/sp/ACS.saml2`
     
    > [!NOTE] 
    > 这些不是实际值。 请使用实际的“回复 URL”和“注销 URL”更新这些值。 请联系 [Pluralsight 客户端支持团队](mailto:support@pluralsight.com)获取这些值。 

4. 在“SAML 签名证书”部分中，单击“元数据 XML”，并在计算机上保存元数据文件。

    ![证书下载链接](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. 本部分的目的是在 Azure 门户中启用 Azure AD 单一登录，并在 Pluralsight 应用程序中配置 SSO。

    Pluralsight 应用程序需要特定格式的 SAML 断言，这要求将自定义属性映射添加到 SAML 令牌属性配置。 以下屏幕截图显示一个示例。

    ![配置单一登录](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    >还可以添加“唯一 ID”属性，并根据组织情况为其设置适当的值（例如 EmployeeID 或其他）。 另请注意，这不是必需的属性；但是，添加以后可以标识唯一用户。 

6. 若要添加必需的 **SAML 令牌属性**，请对下表中显示的每一行执行以下步骤：
   
   | 属性名称 | 属性值 |
   | ---| --- |
   | 名字 |user.givenname |
   | 姓氏 |user.surname |
   | Email |user.mail |
   
   a. 单击“添加用户属性”，打开“添加用户属性”对话框。
    
     ![配置单一登录](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   b. 在“属性名称”文本框中，键入为该行显示的属性名称。
  
   c. 在“属性值”列表中，选择为该行显示的属性值。
  
   d. 单击“确定” 。    

7. 单击“保存”按钮。

    ![配置单一登录](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. 若要为应用程序配置 SSO，请联系 [Pluralsight专业服务](mailTo:professionalservices@pluralsight.com)团队并提供下载的元数据文件。

> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[ Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png)

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png)

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png)

4. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。
 
### <a name="create-a-pluralsight-test-user"></a>创建 Pluralsight 测试用户

本部分的目的是在 Pluralsight 中创建名为“Britta Simon”的用户。 请与 [Pluralsight 客户端支持团队](mailto:support@pluralsight.com)合作，在 Pluralsight 帐户中添加用户。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Pluralsight 的权限，允许她使用 Azure 单一登录。

![分配用户角色][200] 

**要将 Britta Simon 分配到 Pluralsight，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“Pluralsight”。

    ![应用程序列表中的 Pluralsight 链接](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png)  

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

单击访问面板中的“Pluralsight”磁贴时，用户就会自动登录到 Pluralsight 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)（访问面板简介）。 

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](active-directory-saas-tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

