---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 25b5a037012a6d6b47b91e763a49cfb67b89f43c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586723"
---
# <a name="mssqlserver_3156"></a>MSSQLSERVER_3156
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|3156|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LDDB_CANT_WRITE|  
|消息正文|文件 '%ls' 无法还原为 '%ls'。 请使用 WITH MOVE 选项来标识该文件的有效位置。|  
  
## <a name="explanation"></a>说明  
 此常规消息标识因指定位置错误而无法还原的文件的逻辑文件名或物理文件名。  
  
### <a name="possible-causes"></a>可能的原因  
 可能的原因包括：  
  
-   可能需要具备对指定 Windows 目录的访问权限。  
  
-   键入的路径可能有误或指定的路径不存在。  
  
-   某个无法覆盖的文件可能正在使用该文件名。  
  
## <a name="user-action"></a>用户操作  
 在错误日志中查找提供详细信息的其他消息。  
  
 更正指定位置的错误，例如，授予访问权限或使用 RESTORE 语句中的 WITH MOVE 选项重新定位文件。  
  
## <a name="see-also"></a>另请参阅  
 [将数据库还原到新位置 (SQL Server)](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [将文件还原到 &#40;SQL Server 的新位置&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
