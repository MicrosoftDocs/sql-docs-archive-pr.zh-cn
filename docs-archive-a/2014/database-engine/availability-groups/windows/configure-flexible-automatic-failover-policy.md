---
title: 配置灵活的故障转移策略，以控制 Always On 可用性组的自动故障转移 (的条件) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c938624a3ed39fe2d41f21a21af5231aa76a8c17
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693114"
---
# <a name="configure-the-flexible-failover-policy-to-control-conditions-for-automatic-failover-always-on-availability-groups"></a>配置灵活的故障转移策略以控制自动故障转移的条件（Always On 可用性组）
  本主题介绍如何在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 为 AlwaysOn 可用性组配置灵活故障转移策略。 灵活的故障转移策略提供了对导致可用性组自动执行故障转移的条件的精确控制。 通过更改触发自动故障转移的失败条件和运行状况检查的频率，可增大或减小自动进行故障转移来支持高可用性 SLA 的可能性。  
  
  
  
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-on-automatic-failovers"></a><a name="Limitations"></a>自动故障转移的限制  
  
-   要执行自动故障转移，当前主副本和一个辅助副本必须配置为使用自动故障转移的同步提交可用性模式，而且辅助副本必须与主副本同步。  
  
-   如果某个可用性组超过其 WSFC 故障阈值，则该 WSFC 群集不会尝试为该可用性组执行自动故障转移。 此外，该可用性组的 WSFC 资源组始终保持失败状态，直到群集管理员手动将该失败的资源组联机，或是数据库管理员对该可用性组执行手动故障转移。 WSFC 故障阈值 ** 定义为给定时间段中可用性组所支持的最大故障数。 默认时间段为六个小时，此时间段中最大故障数的默认值为 *n*-1，其中 *n* 是 WSFC 节点的数目。 若要更改给定的可用性组的故障阈值，请使用 WSFC 故障转移管理器控制台。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   您必须连接到承载主副本的服务器实例。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
  
|任务|权限|  
|----------|-----------------|  
|为新的可用性组配置灵活故障转移策略|需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
|修改现有可用性组的策略|对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **配置灵活故障转移策略**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  对于新的可用性组，请使用[CREATE AVAILABILITY group](/sql/t-sql/statements/create-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。 如果要修改现有的可用性组，请使用[ALTER AVAILABILITY group](/sql/t-sql/statements/alter-availability-group-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。  
  
    -   若要设置故障转移条件级别，请使用 FAILURE_CONDITION_LEVEL = *n* 选项，其中， *n* 是 1 到 5 的整数。  
  
         例如，以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句将现有可用性组 `AG1`的故障条件级别更改为一级：  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         这些整数值与故障条件级别的关系如下：  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] 值|级别|当出现以下情况时，自动启动故障转移…|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|一个|当服务器关闭时。 SQL Server 服务因故障转移或重新启动而停止。|  
        |2|两个|当服务器无响应时。 满足任何下限值条件，SQL Server 服务连接到群集，超过运行状况检查超时阈值，或当前主副本处于失败状态。|  
        |3|三级|出现严重服务器错误时。 满足任何下限值条件或发生严重的内部服务器错误。<br /><br /> 这是默认级别。|  
        |4|四级|出现严重服务器错误时。 满足任何下限值条件或发生中度的服务器错误。|  
        |5|五级|在出现任何限定的失败条件时。 满足任何下限值条件或出现限定的失败条件。|  
  
         有关故障转移条件级别的更多信息，请参阅[针对可用性组的自动故障转移的灵活的故障转移策略 (SQL Server)](flexible-automatic-failover-policy-availability-group.md)。  
  
    -   若要配置运行状况检查超时阈值，请使用 HEALTH_CHECK_TIMEOUT = *n* 选项，其中， *n* 是一个从 15000 毫秒（15 秒）到 4294967295 毫秒的整数。 默认值为 30000 毫秒（30 秒）  
  
         例如，以下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句会将现有可用性组 `AG1`的运行状况检查超时阈值更改为 60,000 毫秒（1 分钟）。  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-configure-the-flexible-failover-policy"></a>配置灵活的故障转移策略 * *  
  
1.  将默认的 (`cd`) 设置为承载主副本的服务器实例。  
  
2.  在将可用性副本添加到可用性组中时，请使用 `New-SqlAvailabilityGroup` cmdlet。 在修改现有可用性副本时，请使用 `Set-SqlAvailabilityGroup` cmdlet。  
  
    -   若要设置故障转移条件级别，请使用 `FailureConditionLevel` *level*参数，其中， *level*是下列值之一：  
  
        |值|级别|当出现以下情况时，自动启动故障转移…|  
        |-----------|-----------|-------------------------------------------|  
        |`OnServerDown`|一个|当服务器关闭时。 SQL Server 服务因故障转移或重新启动而停止。|  
        |`OnServerUnresponsive`|两个|当服务器无响应时。 满足任何下限值条件，SQL Server 服务连接到群集，超过运行状况检查超时阈值，或当前主副本处于失败状态。|  
        |`OnCriticalServerError`|三级|出现严重服务器错误时。 满足任何下限值条件或发生严重的内部服务器错误。<br /><br /> 这是默认级别。|  
        |`OnModerateServerError`|四级|出现严重服务器错误时。 满足任何下限值条件或发生中度的服务器错误。|  
        |`OnAnyQualifiedFailureConditions`|五级|在出现任何限定的失败条件时。 满足任何下限值条件或出现限定的失败条件。|  
  
         有关故障转移条件级别的更多信息，请参阅[针对可用性组的自动故障转移的灵活的故障转移策略 (SQL Server)](flexible-automatic-failover-policy-availability-group.md)。  
  
         例如，以下命令会将现有可用性组 `AG1`的故障条件级别更改为一级。  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `
         -FailureConditionLevel OnServerDown  
        ```  
  
    -   若要设置运行状况检查超时阈值，请使用 `HealthCheckTimeout` *n*参数，其中*n*是15000毫秒 (15 秒) 到4294967295毫秒的整数。 默认值为 30000 毫秒（30 秒）。  
  
         例如，以下命令会将现有可用性组 `AG1`的运行状况检查超时阈值更改为 120,000 毫秒（2 分钟）。  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `
         -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性模式 (AlwaysOn 可用性组) ](availability-modes-always-on-availability-groups.md)   
 [故障转移和故障转移模式 &#40;AlwaysOn 可用性组&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server 故障转移群集 (WSFC) 与 SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [故障转移群集实例的故障转移策略](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
