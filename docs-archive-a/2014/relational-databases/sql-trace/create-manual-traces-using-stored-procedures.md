---
title: 使用存储过程创建手动跟踪 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e2840dced22ccdba8fe71cc87c05d7fd6fb4be58
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587747"
---
# <a name="create-manual-traces-using-stored-procedures"></a>使用存储过程创建手动跟踪
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系统存储过程来创建对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的跟踪。 可以不使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，而使用这些系统存储过程从您自己的应用程序中手动创建跟踪。 这样，您就可以针对企业的特定需求编写自定义应用程序。  
  
## <a name="in-this-section"></a>本节内容  
 下表列出了用于跟踪 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的系统存储过程。  
  
|存储过程|执行的任务|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql)|返回跟踪中包含的事件的相关信息。|  
|[sys.fn_trace_getinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)|返回有关指定跟踪或所有现有跟踪的信息。|  
|[sp_trace_create (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)|创建跟踪定义。 新的跟踪将处于停止状态。|  
|[sp_trace_generateevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)|创建用户定义事件。|  
|[sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)|将事件类或数据列添加到跟踪，或从跟踪中删除事件类或数据列。|  
|[sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|启动、停止或关闭跟踪。|  
|[sys.fn_trace_getfilterinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)|返回有关应用于跟踪的筛选器的信息。|  
|[sp_trace_setfilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|将新的或已修改的筛选器应用于跟踪。|  
  
 **使用存储过程定义自己的跟踪**  
  
1.  使用 **sp_trace_setevent**指定要捕获的事件。  
  
2.  指定任何事件筛选器。 有关详细信息，请参阅[设置跟踪筛选器 (Transact SQL)](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)。  
  
3.  使用 **sp_trace_create** 为捕获的事件数据指定目的。  
  
 有关使用跟踪存储过程的示例，请参阅[创建跟踪 (Transact-SQL)](../sql-trace/create-a-trace-transact-sql.md)。  
  
 **设置跟踪定义默认值**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
 **设置跟踪显示默认值**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **创建跟踪**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../sql-trace/create-a-trace-transact-sql.md)  
  
 **向跟踪模板添加或从中删除事件**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
