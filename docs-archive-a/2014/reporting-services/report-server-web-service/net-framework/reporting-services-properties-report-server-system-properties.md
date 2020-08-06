---
title: 报表服务器系统属性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f8351417b716de362a993aeac26ac848c0da16de
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688515"
---
# <a name="report-server-system-properties"></a>报表服务器系统属性
  已保留以下系统属性名称。 您不能创建具有相同名称的用户定义属性。 您可以使用 Web 服务方法读取或修改其中的许多属性。  
  
## <a name="properties"></a>属性  
  
|属性|说明|  
|--------------|-----------------|  
|SiteName|在用户界面上显示的报表服务器站点的名称。 默认值为 `Microsoft Report Server`。 此属性可以是空字符串。 最大长度为 8,000 个字符。|  
|SystemSnapshotLimit|为报表存储的快照的最大数目。 有效值为 `-1` 到 `2`、`147`、`483`、`647`。 如果值为 `-1`，则无快照限制。|  
|SystemReportTimeout|在报表服务器命名空间中托管的所有报表的默认报表处理超时值（以秒为单位）。 该值可在报表级别进行重写。 如果设置了此属性，则超过指定时间后报表服务器会尝试停止处理报表。 有效值为 `-1` 到 `2`、`147`、`483`、`647`。 如果值为 `-1`，则处理期间命名空间中的报表不会超时。 默认值为 `1800`。|  
|UseSessionCookies|指示报表服务器与客户端浏览器通信时是否应使用会话 cookie。 默认值为 `true`。|  
|SessionTimeout|会话保持活动状态的时间长度（以秒为单位）。 默认值为 `600`。|  
|EnableMyReports|指示是否启用“我的报表”功能。 值为 `true` 表示已启用该功能。|  
|MyReportsRole|对用户的“我的报表”文件夹创建安全策略时所用角色的名称。 默认值为 `My Reports Role`。|  
|EnableExecutionLogging|指示报表执行日志记录是否处于启用状态。 默认值为 `true`。|  
|ExecutionLogDaysKept|在执行日志中保留报表执行信息的天数。 此属性的有效值包括 `0` 到 `2`、`147`、`483` 和 `647`。 如果值为 `0`，则不从执行日志表中删除项。 默认值为 `60`。|  
|SnapshotCompression|定义如何压缩快照。 默认值为 `SQL`。 有效值如下：<br /><br /> `SQL` = 在存储到报表服务器数据库中时压缩快照。 这是当前的行为。<br /><br /> **None** = 不压缩快照。<br /><br /> `All` = 针对所有的存储选项（包括报表服务器数据库或文件系统）压缩快照。|  
|EnableClientPrinting|确定是否可从报表服务器下载 RSClientPrint ActiveX 控件。 有效值为 `true` 和 `false` 。 默认值为 `true`。 有关此控件所需的其他设置的详细信息，请参阅 [启用和禁用 Reporting Services 的客户端打印](../../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。|  
|EnableIntegratedSecurity|确定报表数据源连接是否支持集成安全性。 默认值为 `True`。 有效值如下：<br /><br /> `True` = 启用集成安全性。<br /><br /> `False` = 不启用集成安全性。 将不运行配置为使用集成安全性的报表数据源。|  
|EnableRemoteErrors|包括外部错误信息（例如，有关报表数据源的错误信息），其中包含针对从远程计算机请求报表的用户返回的错误消息。 有效值为 `true` 和 `false`。 默认值为 `false`。 有关详细信息，请参阅[启用远程错误 (Reporting Services)](../../report-server/enable-remote-errors-reporting-services.md)。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [使用 Web 服务和 .NET Framework 生成应用程序](building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
