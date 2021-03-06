---
title: Azure Application Insights 概览仪表板 | Microsoft 文档
description: 使用 Azure Application Insights 概览仪表板功能来监控应用程序。
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: mbullwin
ms.openlocfilehash: 0be54c47965c6a27c3506fd37a7bf67e4b2b7924
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2018
ms.locfileid: "34356080"
---
# <a name="application-insights-overview-dashboard-preview"></a>Application Insights 概览仪表板（预览）

Application Insights 一直都有一个总览窗格，可让用户快速、直接地评估应用程序的运行状况和性能。 新的预览版概览仪表板提供了更快更灵活的体验。

## <a name="how-do-i-test-out-the-new-experience"></a>如何测试新体验？

 在 Application Insights 中的“概述”下，选择_在新的“概述”成为默认体验之前，请先尝试它_。

![概览预览](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-01.png)

这将会启动新的默认概览仪表板：

![概览预览窗格](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-02.png)

## <a name="better-performance"></a>性能更好

时间范围选择已简化为简单的一键式界面。

![时间范围](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-03.png)

总体性能已大大提高。 每个默认动态更新的 KPI 磁贴都链接到相应的 Application Insights 功能。 例如，选择失败的请求将启动“失败”窗格：

![失败数](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-04.png)

## <a name="application-dashboard"></a>应用程序仪表板

应用程序仪表板利用 Azure 内现有仪表板技术，为你的应用程序运行状况和性能提供了一个完全可自定义的单一窗格视图。

若要访问默认仪表板，请选择左上角的“应用程序仪表板”。

![仪表板视图](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-05.png)

如果这是你第一次访问仪表板，它将启动默认视图：

![仪表板视图](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-06.png)

如果你喜欢，可以保留默认视图，也可以在仪表板中执行添加或删除操作，让仪表板契合团队的需求。

> [!NOTE]
> 所有有权访问 Application Insights 资源的用户共享相同的应用程序仪表板体验。 一个用户所做的更改将修改所有用户的视图。

若要导航回概览体验，只需选择：

![“概览”按钮](.\media\app-insights-overview-dashboard\app-insights-overview-dashboard-07.png)

## <a name="next-steps"></a>后续步骤

- [漏斗图](usage-funnels.md)
- [保留](app-insights-usage-retention.md)
- [用户流](app-insights-usage-flows.md)
- [仪表板](app-insights-dashboards.md)
