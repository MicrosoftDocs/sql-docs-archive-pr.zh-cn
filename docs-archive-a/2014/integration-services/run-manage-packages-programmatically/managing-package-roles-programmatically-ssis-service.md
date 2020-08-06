---
title: 以编程方式管理包角色（SSIS 服务）| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dff54f3f90d9e008ae21c83c2a8fdc3f7440a5c3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692991"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>以编程方式管理包角色（SSIS 服务）
  以编程方式使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包时，您可能希望确定哪些角色可以应用于包，或确定或设置应用于各个包的角色。 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 命名空间的 <xref:Microsoft.SqlServer.Dts.Runtime> 类提供了多种满足这些要求的方法。

 角色仅适用于存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 数据库中的包  。 有关包角色的详细信息，请参阅 [Integration Services 角色（SSIS 服务）](../security/integration-services-roles-ssis-service.md)。

 本主题中讨论的所有方法都需要引用 `Microsoft.SqlServer.ManagedDTS` 程序集。 在新项目中添加引用后，请 <xref:Microsoft.SqlServer.Dts.Runtime> 使用或语句导入该命名 `using` 空间 `Imports` 。

> [!IMPORTANT]
>  <xref:Microsoft.SqlServer.Dts.Runtime.Application> 类中用于 SSIS 包存储的方法仅支持“.”、localhost 或本地服务器的服务器名称。 不能使用“(local)”。

## <a name="determining-which-roles-are-available"></a>确定哪些角色可用
 若要确定哪些角色可用于存储在特定服务器上的包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 类的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 方法。

## <a name="determining-which-roles-are-assigned"></a>确定哪些角色已分配
 若要确定哪些角色已经分配给了特定包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 方法。 若要将角色分配给包，可调用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 方法。

![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [Integration Services 角色（SSIS 服务）](../security/integration-services-roles-ssis-service.md)


