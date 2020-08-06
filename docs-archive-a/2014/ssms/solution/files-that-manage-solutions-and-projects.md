---
title: 用于管理解决方案和项目的文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c94f1f853263c3969961de91ec95b921f5d78ead
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689698"
---
# <a name="files-that-manage-solutions-and-projects"></a>用于管理解决方案和项目的文件
  本主题介绍了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 专用文件类型。 默认情况下，所有的解决方案及其项目均创建于 \My Documents\SQL Server Management Studio Projects 中。  
  
## <a name="management-studio-solution-files"></a>Management Studio 解决方案文件  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用的文件类型不同于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio。 这意味着无法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Visual Studio 中打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 解决方案。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 解决方案文件使解决方案资源管理器可以显示一个图形界面，以便管理文件。  
  
|分机|文件类型|说明|创建者|  
|---------------|---------------|-----------------|----------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 解决方案对象|为环境提供对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 项目、项目项和解决方案在磁盘上的位置的引用|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio 项目文件  
 解决方案包含用于管理解决方案中对象的解决方案文件，同样，项目包含项目文件。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为项目所创建的项目文件类型取决于创建项目时使用的模板。 下表介绍了为每个项目所创建的文件类型。  
  
|分机|项目模板|  
|---------------|----------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本项目|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 脚本项目|  
  
## <a name="location-of-solution-level-files"></a>解决方案级文件的位置  
 默认情况下，解决方案级文件创建于使用该解决方案创建的第一个项目的物理目录中。 可以通过创建解决方案指定解决方案的目录，也可以在创建新项目时指定该目录。  
  
 如果目录结构与解决方案资源管理器中显示的逻辑结构相似，则更容易找到项目文件和解决方案文件并与工作组中的其他开发人员共享。  
  
## <a name="see-also"></a>另请参阅  
 [用编码管理文件](manage-files-with-encoding.md)   
 [杂项文件](miscellaneous-files.md)   
 [解决方案资源管理器](solution-explorer.md)   
 [SQL Server Management Studio 的解决方案 &#40;&#41;](solutions-sql-server-management-studio.md)   
 [项目 &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)   
 [解决方案资源管理器源代码管理](../../database-engine/solution-explorer-source-control.md)  
  
  
