---
title: SQL Server 2014 中不再使用的管理工具功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3ae7d4a708816c1b30a0b208bb422e0920b4c76c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690057"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 中不再使用的管理工具功能
  本主题介绍 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不再提供的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]管理工具功能。  
  
## <a name="features-removed-in-sscurrent"></a>在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中删除的功能  
 无  
  
## <a name="features-removed-in-sssql11"></a>在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中删除的功能  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 SQL Server Compact Edition 代码编辑器已从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中删除。 已从对象资源管理器、解决方案资源管理器和模板资源管理器中删除对 SQL Server Compact Editor 的支持。 在 Microsoft Visual Studio 2010 Service Pack 1 或 Webmatrix 中使用 Transact-SQL 编辑器。  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>SQL Server 代理的 ActiveX 子系统  
 在此版本中，SQL Server 代理的 ActiveX 子系统已被删除。 没有替代功能。  
  
### <a name="sp_addtask-sp_deletetask-sp_updatetask"></a>sp_addtask、sp_deletetask、sp_updatetask  
 在此版本中，已删除 Sp_addtask、sp_deletetask 和 sp_updatetask。 请勿在新应用程序或更新的应用程序中使用此功能。  
  
### <a name="net-send-and-pager-notification"></a>网络发送和寻呼通知  
 在此版本中，已删除网络发送和寻呼通知。 请勿在新应用程序或更新的应用程序中使用此功能。  
  
### <a name="data-tier-applications"></a>数据层应用程序  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中的某些数据层应用程序 (DAC) 功能已经在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]删除。 但是，随 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 发布的数据层应用程序框架（DACfx 版本 3.0）却能够兼容 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以及 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]。 早期版本的 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ，包括 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] （包含在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]中）不支持 DAC 版本 3.0。 Visual Studio 2010 数据库项目不支持使用 DACfx 版本 3.0 或更高版本生成的 DAC 3.0 DACPAC 包或 DAC Export (BACPAC) 包。  
  
 Microsoft 建议使用最新可用版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 数据库项目。  
  
 DACfx 3.0 API 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具的确支持读取使用早期版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 工具和 DACfx 版本创建的 DACPAC 和 BACPAC 文件：将数据库提取到这些版本的 DACPAC 文件，然后通过 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Data Tools 将数据库部署到支持的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。  
  
## <a name="see-also"></a>另请参阅  
 [向后兼容性](../../2014/getting-started/backward-compatibility.md)  
  
  
