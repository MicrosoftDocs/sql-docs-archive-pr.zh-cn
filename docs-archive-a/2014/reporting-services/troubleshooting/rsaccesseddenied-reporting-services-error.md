---
title: rsAccessedDenied - Reporting Services 错误 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 194006c2ef6f22b9bc27e9e8cbe1eebd027ed6b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587157"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Reporting Services 错误
  当用户没有权限进行操作时，会出现 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 错误 **rsAccessedDenied** 。 例如，用户没有允许他们打开报表的角色分配，或者没有用所需的权限打开其浏览器。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | SharePoint 模式|  
  
-   如果通过 URL 直接访问报表服务器时发生这种错误，则该例外情况将映射到 HTTP 401 错误。  
  
-   如果使用报表管理器或其他工具时发生这种错误，则该错误会显示在错误页中。  
  
-   如果计划操作、订阅或传递时发生这种错误，则该错误仅显示在报表服务器日志文件中。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|**产品名称**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**事件 ID**|rsAccessedDenied|  
|**事件源**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|组件 |[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**消息正文**|为用户“mydomain\myAccount”授予的权限不足，无法执行此操作。 (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>用户操作  
 通过角色分配授予访问报表服务器内容和操作的权限。 在新安装中，只有本地管理员才拥有访问报表服务器的权限。 若要向其他用户授予访问权限，本地管理员必须创建指定域用户帐户或组帐户的角色分配、一个或多个定义用户可以执行的任务的角色，以及作用域（通常是主文件夹或报表服务器文件夹层次结构的根节点）。 可以使用报表管理器创建角色分配。 有关详细信息，请在 SQL Server 联机丛书中搜索“角色分配”。  
  
 此错误也由报表服务器的本地管理引起的。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [角色分配](../security/role-assignments.md)   
 [授予对本机模式报表服务器的权限](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [角色和权限 (Reporting Services)](../security/roles-and-permissions-reporting-services.md)  
  
  
