---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 439d282f18490a4353d6528276eaf7e4231c503b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689421"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10535|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_PLAN|  
|消息正文|由于在计划缓存中找不到与指定计划句柄对应的计划，因此无法创建计划指南 '%.*ls'。 请指定已缓存的计划句柄。 有关已缓存的计划句柄的列表，请查询 sys.dm_exec_query_stats 动态管理视图。|  
  
## <a name="explanation"></a>说明  
 未在与指定的计划句柄相对应的计划缓存中找到计划。  
  
## <a name="user-action"></a>用户操作  
 请指定已缓存的计划句柄。 有关已缓存的计划句柄的列表，请查询 sys.dm_exec_query_stats 动态管理视图。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
