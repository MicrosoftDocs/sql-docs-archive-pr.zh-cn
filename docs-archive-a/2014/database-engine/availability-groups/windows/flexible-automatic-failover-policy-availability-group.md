---
title: 用于 (SQL Server) 的可用性组的自动故障转移的灵活的故障转移策略 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cd4dd62d8b30e2041415e0b9be5682ce4b01d1f6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585973"
---
# <a name="flexible-failover-policy-for-automatic-failover-of-an-availability-group-sql-server"></a>针对可用性组的自动故障转移的灵活的故障转移策略 (SQL Server)
  灵活的故障转移策略提供了对导致可用性组[自动故障转移](failover-and-failover-modes-always-on-availability-groups.md)的条件的精确控制。 通过更改触发自动故障转移的失败条件和运行状况检查的频率，可增大或减小自动进行故障转移来支持高可用性 SLA 的可能性。  
  
 可用性组的灵活的故障转移策略是由其失败条件级别和运行状况检查超时阈值定义的。 在检测到某个可用性组已超出其失败条件级别或其运行状况检查超时阈值时，该可用性组的资源 DLL 会响应 Windows Server 故障转移群集 (WSFC) 群集。 之后，WSFC 群集会启动到辅助副本的自动故障转移。  
  
> [!IMPORTANT]  
>  如果某个可用性组超过其 WSFC 故障阈值，则该 WSFC 群集不会尝试为该可用性组执行自动故障转移。 此外，该可用性组的 WSFC 资源组始终保持失败状态，直到群集管理员手动将该失败的资源组联机，或是数据库管理员对该可用性组执行手动故障转移。 WSFC 故障阈值 ** 定义为给定时间段中可用性组所支持的最大故障数。 默认时间段为六个小时，此时间段中最大故障数的默认值为 *n*-1，其中 *n* 是 WSFC 节点的数目。 若要更改给定的可用性组的故障阈值，请使用 WSFC 故障转移管理器控制台。  
  
  
  
##  <a name="health-check-timeout-threshold"></a><a name="HCtimeout"></a> 运行状况检查超时阈值  
 可用性组的 WSFC 资源 DLL 将通过在承载主副本的 SQL Server 实例上调用 *sp_server_diagnostics* 存储过程来对主副本执行 [运行状况检查](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 。 **sp_server_diagnostics** 按等于可用性组的运行状况检查超时阈值的 1/3 的时间间隔返回结果。 默认的运行状况检查超时阈值为 30 秒，这将导致 **sp_server_diagnostics** 按 10 秒的时间间隔返回结果。 如果 **sp_server_diagnostics** 的运行速度较慢且未返回信息，则资源 DLL 将在等待运行状况检查超时阈值的完全时间间隔后确定主副本已停止响应。 如果主副本停止响应，则启动自动故障转移（如果当前受支持）。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 在数据库级别不执行运行状况检查。  
  
##  <a name="failure-condition-level"></a><a name="FClevel"></a> 故障条件级别  
 由 **sp_server_diagnostics** 返回的诊断数据和运行状况信息是否保证触发自动故障转移取决于可用性组的失败条件级别。 *失败条件级别* 指定触发自动故障转移的失败条件。 有 5 个失败条件级别，其范围从最少限制（级别 1）到最多限制（级别 5）。 给定级别包含限制较少的级别。 因此，最严格的级别 5 包含四个限制更少的条件，依此类推。  
  
> [!IMPORTANT]  
>  任何级别的故障条件均不检测已损坏的数据库和可疑数据库。 因此，已损坏的或可疑的数据库（无论是由于硬件故障、数据损坏还是其他问题导致）从不触发自动故障转移。  
  
 下表介绍了与各级别相对应的失败条件。  
  
|级别|失败条件|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 值|PowerShell 值|  
|-----------|-----------------------|------------------------------|----------------------|  
|一个|当服务器关闭时。 这是限制最少的级别。 指定在发生以下任何情况时启动自动故障转移：<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务停止。<br /><br /> 因为没有从服务器实例接收到 ACK，连接到 WSFC 群集的可用性组的租期到期。 有关详细信息，请参阅 [工作方式：SQL Server AlwaysOn 租约超时](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)。|1|`OnServerDown`|  
|两个|当服务器无响应时。 指定在发生以下任何情况时启动自动故障转移：<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例未连接到群集，并且超出了可用性组的用户指定的运行状况检查超时阈值。<br /><br /> 可用性副本处于失败状态。|2|`OnServerUnresponsive`|  
|三级|出现严重服务器错误时。 指定在发生了严重的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部错误（例如孤立的自旋锁、严重的写访问冲突或过多的转储）时启动自动故障转移。 这是默认级别。|3|`OnCriticalServerError`|  
|四级|出现严重服务器错误时。 指定在发生了中等 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部错误（在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部资源池中出现持久的内存不足情况）时启动自动故障转移。|4|`OnModerateServerError`|  
|五级|在出现任何限定的失败条件时。 这是限制最多的级别。 指定在出现任何符合的失败条件时启动自动故障转移，这些失败条件包括：<br /><br /> SQL 引擎的工作线程耗尽。<br /><br /> 检测到无法解决的死锁。|5|`OnAnyQualifiedFailureConditions`|  
  
> [!NOTE]  
>  缺少 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例对客户端请求的响应与可用性组无关。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **配置自动故障转移**  
  
-   [更改可用性副本的可用性模式 (SQL Server) ](change-the-availability-mode-of-an-availability-replica-sql-server.md)（自动故障转移要求同步提交可用性模式）  
  
-   [更改可用性副本的故障转移模式 (SQL Server)](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [配置灵活的故障转移策略以控制自动故障转移的条件（AlwaysOn 可用性组）](configure-flexible-automatic-failover-policy.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相关内容  
  
-   [工作方式：SQL Server AlwaysOn 租约超时](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式 (AlwaysOn 可用性组) ](availability-modes-always-on-availability-groups.md)   
 [故障转移和故障转移模式 &#40;AlwaysOn 可用性组&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [故障转移群集实例的故障转移策略](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
  
  
