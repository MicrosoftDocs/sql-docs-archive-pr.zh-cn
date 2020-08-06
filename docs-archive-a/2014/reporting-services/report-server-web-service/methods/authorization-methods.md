---
title: 授权方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b04a21b5075e939a4732e2f8ec219e169f4ba440
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691595"
---
# <a name="authorization-methods"></a>授权方法
  可以使用这些方法管理报表服务器上的任务、角色和策略。  
  
|方法|操作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|将新的角色添加到报表服务器数据库。 此方法仅适用于本机模式。|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|从报表服务器数据库删除角色。 此方法仅适用于本机模式。|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|返回与报表服务器数据库或 SharePoint 库中特定项相关联的用户权限。|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|返回与报表服务器数据库或 SharePoint 库中特定项相关联的策略。|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|返回角色元数据属性和关联任务的集合。|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|返回用户的系统权限。 此方法仅适用于本机模式。|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|返回系统策略，包括这些策略与之关联的组和角色。 此方法仅适用于本机模式。|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|删除与报表服务器数据库中特定项相关联的策略，并将该项的安全策略设置为其父级的策略。|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|返回一个布尔值，指示是否需要安全套接字层 (SSL) 协议才能使用 <xref:ReportService2010> 端点。|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|返回报表服务器管理的角色的名称和说明。|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|返回在调用时需要安全连接的 <xref:ReportExecution2005> 端点中简单对象访问协议 (SOAP) 方法的列表。 报表服务器的 `SecureConnectionLevel` 设置用于确定返回的方法。|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|返回报表服务器管理的任务。|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|设置与指定的项关联的策略。|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|设置角色元数据属性并将一组任务与某一角色相关联。 此方法仅适用于本机模式。|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|设置定义组及其关联角色的系统策略。 此方法仅适用于本机模式。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [报表服务器 Web 服务](../report-server-web-service.md)   
 [报表服务器 Web 服务方法](report-server-web-service-methods.md)   
 [技术参考 (SSRS)](../../technical-reference-ssrs.md)  
  
  
