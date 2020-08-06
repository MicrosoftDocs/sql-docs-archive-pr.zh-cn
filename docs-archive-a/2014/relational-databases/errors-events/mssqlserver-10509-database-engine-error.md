---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 73194c7da553bf27acb78d8c4e7d71bc93f457d0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693368"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10509|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_STMT|  
|消息正文|无法创建计划指南 '%.\*ls'，因为 `@stmt` 或 `@statement_start_offset` 指定的语句包含语法错误或者无法在计划指南中使用。 请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。|  
  
## <a name="explanation"></a>说明  
 `@stmt` 或 `@statement_start_offset` 指定的语句包含语法错误或者无法在计划指南中使用。  
  
## <a name="user-action"></a>用户操作  
 请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sys. dm_exec_query_stats &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
