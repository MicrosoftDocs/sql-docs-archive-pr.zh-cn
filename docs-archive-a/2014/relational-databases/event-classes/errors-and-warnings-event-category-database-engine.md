---
title: “错误和警告”事件类别（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
ms.openlocfilehash: d55f37f5401f60ddfeec340af1ae6d532eb6ad01
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691190"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errors and Warnings 事件类别（数据库引擎）
  **Errors and Warnings** 事件类别包含常规错误和警告事件。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[Attention 事件类](attention-event-class.md)|指示出现了 **Attention** 事件。|  
|[Background Job Error 事件类](background-job-error-event-class.md)|指示后台作业异常终止。|  
|[Bitmap Warning 事件类](bitmap-warning-event-class.md)|指示已在查询中禁用位图筛选。|  
|[Blocked Process Report 事件类](blocked-process-report-event-class.md)|指示任务被阻塞的时间超过了指定的时间。|  
|[CPU Threshold Exceeded 事件类](cpu-threshold-exceeded-event-class.md)|指示资源调控器检测到超出指定 CPU 阈值的查询。|  
|[ErrorLog 事件类](errorlog-event-class.md)|指示已将错误事件记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中。|  
|[EventLog 事件类](eventlog-event-class.md)|指示已将事件记录到 Windows 事件日志中。|  
|[Exception 事件类](exception-event-class.md)|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中出现了异常。|  
|[Exchange Spill 事件类](exchange-spill-event-class.md)|指示并行查询计划中的通信缓冲区已写入 tempdb 数据库。|  
|[Execution Warnings 事件类](execution-warnings-event-class.md)|指示在执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句或存储过程期间出现了内存授予警告。|  
|[Hash Warning 事件类](hash-warning-event-class.md)|指示在哈希操作过程中发生哈希递归或哈希援助。|  
|[Missing Column Statistics 事件类](missing-column-statistics-event-class.md)|指示缺少可能对优化器有用的列统计信息。|  
|[Missing Join Predicate 事件类](missing-join-predicate-event-class.md)|指示正在执行没有联接谓词的查询。|  
|[Sort Warnings 事件类](sort-warnings-event-class.md)|指示不适合内存的排序操作。|  
|[User Error Message 事件类](user-error-message-event-class.md)|显示用户可见的错误消息。|  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
