---
title: 性能监视和优化工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tools [SQL Server], monitoring performance
- monitoring server performance [SQL Server], tools
- monitoring performance [SQL Server], tools
- database performance [SQL Server], tools
- tuning databases [SQL Server], tools
- database monitoring [SQL Server], tools
- performance [SQL Server], monitoring tools
- server performance [SQL Server], tools
ms.assetid: 31529dfe-68e7-49f7-b3c2-39fcecf33a95
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c9a1f262493b54c06e2bb9eb3d4d6d44bf60d52f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588486"
---
# <a name="performance-monitoring-and-tuning-tools"></a>性能监视和优化工具
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一套综合的工具，用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的事件和优化物理数据库的设计。 工具的选择取决于要执行的监视或优化类型和要监视的具体事件。  
  
 以下是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 监视和优化工具：  
  
|工具|说明|  
|----------|-----------------|  
|[sp_trace_setfilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 用于跟踪引擎进程事件（如批处理或事务的开始），使您能够监视服务器和数据库的活动（例如，死锁、错误或登录活动）。 您可以将 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 数据捕获到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表或文件中供以后分析，还可以逐步重播在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上捕获的事件以确切了解所发生的事件。|  
|[SQL Server 分布式重播](../../tools/distributed-replay/sql-server-distributed-replay.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分布式重播可以使用多台计算机重播跟踪数据，并模拟任务关键型工作负荷。|  
|[监视资源使用情况（系统监视器）](../performance-monitor/monitor-resource-usage-system-monitor.md)|系统监视器主要用于跟踪资源的使用情况（如正在使用的缓冲区管理器页请求数），使您能够使用预定义的对象和计数器或用户定义的计数器来监视事件，从而监视服务器的性能与活动。 系统监视器（Microsoft Windows NT 4.0 中的性能监视器）将收集计数和比率而不是与事件相关的数据（例如，内存使用量、活动的事务数、阻塞的锁数或 CPU 活动）。 您可以在特定的计数器上设置阈值以生成要发送给操作员的警告。<br /><br /> 系统监视器在 Microsoft Windows Server 和 Windows 操作系统上运行。 它可以从远程或本地监视 Windows NT 4.0 或更高版本上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。<br /><br /> [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 与系统监视器之间的主要差别在于 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 用于监视数据库引擎事件，而系统监视器用于监视与服务器进程相关的资源使用情况。|  
|[打开活动监视器 (SQL Server Management Studio)](../performance-monitor/open-activity-monitor-sql-server-management-studio.md)|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的活动监视器对于当前活动的特别视图很有用，并以图形方式显示有关信息︰<br /><br /> 在某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上运行的进程。<br /><br /> 被阻塞的进程。<br /><br /> 锁。<br /><br /> 用户活动。|  
|[SQL 跟踪](../sql-trace/sql-trace.md)|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 存储过程：<br /><br /> [sp_trace_create (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)<br /><br /> [sp_trace_generateevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)<br /><br /> [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)<br /><br /> [sp_trace_setfilter (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)<br /><br /> [sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|  
|错误日志|Windows 应用程序事件日志全面描述了 Windows Server 和 Windows 操作系统上发生的事件，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理和全文搜索中的事件。 它包含有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中独有的事件的信息。 您可以利用错误日志中的信息来解决与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有关的问题。|  
|[系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)|下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统存储过程可以作为许多监视任务的一种功能强大的备选方法：<br /><br /> [sp_who (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)： <br />                    报告有关当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户和进程的快照信息，包括当前正在执行的语句以及该语句是否被阻塞。<br /><br /> [sp_lock &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)：报告有关锁的快照信息，包括对象 ID、索引 ID、锁的类型以及锁应用于的类型或资源。<br /><br /> [&#40;transact-sql&#41;sp_spaceused ](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)：显示表 (或整个数据库) 使用的当前磁盘空间量的估计值。<br /><br /> [sp_monitor &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-monitor-transact-sql)：显示统计信息，包括 CPU 使用率、i/o 使用情况以及自上次执行**sp_monitor**以来的空闲时间量。|  
|[DBCC (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-transact-sql)|DBCC（数据库控制台命令）语句使您能够检查性能统计信息以及数据库的逻辑与物理一致性。|  
|[内置函数 (Transact-SQL)](/sql/t-sql/functions/functions)|内置函数可显示自启动服务器以来有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活动的快照统计信息，这些统计信息存储在预定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计数器中。 例如， **@ @CPU_BUSY **包含 CPU 执行代码所需的时间 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ;**@@CONNECTIONS**包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接或尝试连接的次数; ** @PACKET_ERRORS @** 包含连接上出现的网络数据包数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|[跟踪标志 (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)|跟踪标志可显示有关服务器内的特定活动的信息，用于诊断问题或性能问题（例如死锁链）。|  
|[Database Engine Tuning Advisor](database-engine-tuning-advisor.md)|数据库引擎优化顾问可分析所执行的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句对要优化的数据库性能的影响。 数据库引擎优化顾问提供了添加、删除或修改索引、索引视图及分区的建议。|  
  
## <a name="choosing-a-monitoring-tool"></a>选择监视工具  
 监视工具的选择取决于要监视的事件或活动。  
  
|事件或活动|SQL Server Profiler|分布式重播|系统监视器|活动监视器|Transact-SQL|错误日志|  
|-----------------------|-------------------------|------------------------|--------------------|----------------------|-------------------|----------------|  
|走向分析|是||是||||  
|重播捕获的事件|是（从单台计算机）|是（从多台计算机）|||||  
|临时监视|是|||是|是|是|  
|生成警报|||是||||  
|图形界面|是||是|是||是|  
|在自定义应用程序内使用|是 <sup>1</sup>||||是||  
  
 <sup>1</sup>使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 系统存储过程。  
  
## <a name="windows-monitoring-tools"></a>Windows 监视工具  
 Windows 操作系统和 Windows Server 2003 也提供这些监视工具。  
  
|工具|说明|  
|----------|-----------------|  
|任务管理器|显示在系统上运行的进程和应用程序的提要。|  
|网络监视器代理|用于监视网络流量。|  
  
 有关 Windows 操作系统或 Windows Server 工具的详细信息，请参阅 Windows 文档。  
  
  
