---
title: Reporting Services 日志文件和来源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [Reporting Services], log files
- logs [Reporting Services]
- logs [Reporting Services], about log files
- report servers [Reporting Services], log files
- report server log files
- files [Reporting Services], logs
ms.assetid: 80ef0acc-cbef-49d0-87e7-844e3ce19604
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3908c39fc6deba57bf8f0e277918e5b8167f4a77
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588272"
---
# <a name="reporting-services-log-files-and-sources"></a>Reporting Services 日志文件和来源
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表服务器和报表服务器环境使用各种日志目标来记录有关服务器操作和状态的信息。 有两个基本日志记录类别：执行日志记录和跟踪日志记录。 执行日志记录包含有关报表执行统计信息、审核、性能诊断和优化的信息。 跟踪日志记录是有关错误消息和一般诊断的信息。

 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式 | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式

 下表提供指向有关每个日志的其他信息（包括日志位置以及如何查看日志内容）的链接。

|日志|说明|
|---------|-----------------|
|[报告服务器执行日志和 ExecutionLog3 视图](report-server-executionlog-and-the-executionlog3-view.md)|执行日志是存储在报表服务器数据库中的 SQL Server 视图。<br /><br /> 报表服务器执行日志包含特定报表的有关数据，包括报表的运行时间、运行人员、目标传递位置以及所用的呈现格式。|
|SharePoint 跟踪日志|对于在 SharePoint 下运行的报表服务器，SharePoint 跟踪日志包含 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 信息。 可为 SharePoint 统一日志服务配置 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 特定信息。 有关详细信息，请参阅 [为 SharePoint 跟踪日志 (ULS) 启用 Reporting Services 事件](turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls.md)|
|[报表服务器服务跟踪日志](report-server-service-trace-log.md)|服务跟踪日志包含的信息极为详细，这对于调试应用程序或者调查问题或事件很有帮助。<br /><br /> `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`|
|[报表服务器 HTTP 日志](report-server-http-log.md)|HTTP 日志文件中包含有关由报表服务器 Web 服务和报表管理器处理的所有 HTTP 请求和响应的记录。|
|[Windows 应用程序日志](windows-application-log.md)|Microsoft Windows 应用程序日志包含报表服务器事件的有关信息。|
|Windows 性能日志|Windows 性能日志包含报表服务器的性能数据。 您可以创建性能日志，然后选择计数器来确定要收集的数据。 有关详细信息，请参阅 [监视报表服务器性能](monitoring-report-server-performance.md)。|
|安装日志文件|在安装过程中还会创建日志文件。 如果安装失败，或虽然成功但显示警告消息或其他消息，您可以检查日志文件以排除问题。 有关详细信息，请参阅 [查看和读取 SQL Server 安装程序日志文件](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。|
|IIS 日志|由 Microsoft Internet Information Services (IIS) 创建的日志文件。 有关详细信息，请参阅 [如何启用登录 Internet 信息服务 (IIS)](https://support.microsoft.com/kb/313437)。|
|视频|查看演示使用 Microsoft Power Query 查看 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 日志文件的简短视频。<br /><br /> ![查看有关 Power Query 和 SSRS 日志的视频](../media/generic-video-thumbnail.png "查看有关 Power Query 和 SSRS 日志的视频")|

## <a name="see-also"></a>另请参阅
 [Reporting Services 报表服务器 &#40;本机模式下&#41;](reporting-services-report-server-native-mode.md) [错误和事件参考 &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)


