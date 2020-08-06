---
title: 配置“最大工作线程数”服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4881cefee350d34d93b539c56be6f43866d3ddfe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588042"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>配置 max worker threads 服务器配置选项
  本主题说明如何使用  或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中配置 max worker threads [!INCLUDE[tsql](../../includes/tsql-md.md)]服务器配置选项。 **max worker threads** 选项配置可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的工作线程数。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用操作系统的本机线程服务，以便使一个或多个线程支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同时支持的每一个网络，另一个线程处理数据库检查点，而线程池则处理所有用户。 **max worker threads** 的默认值为 0。 这使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在启动时自动配置工作线程数。 默认设置对于大多数系统为最佳设置。 不过，根据您的系统配置，有时将 **max worker threads** 设置为特定值会提高性能。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **配置 max worker threads 选项，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **跟进：** [在配置“最大工作线程”选项之后](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   当实际的查询请求数量少于 **max worker threads**中设置的数量时，每一个线程处理一个查询请求。 但是，如果实际的查询请求数超过**最大工作线程**数中设置的数量，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将工作线程汇集在一起，以便下一个可用的工作线程可以处理该请求。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
  
-   此选项是一个高级选项，仅应由有经验的数据库管理员或认证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技术人员更改。  
  
-   当服务器上连接有大量客户端时，线程池有助于优化性能。 一般情况下，会为每个查询请求创建一个单独的操作系统线程。 但是，当到服务器的连接达到数以百计时，为每个查询请求使用一个线程会占用大量的系统资源。 **max worker threads** 选项使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以为更大数量的查询请求创建一个工作线程池，这将提高性能。  
  
-   下表显示了针对各种 CPU 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的组合自动配置的最大工作线程数。  
  
    |CPU 数|32 位计算机|64 位计算机|  
    |--------------------|----------------------|----------------------|  
    |\<= 4 个处理器|256|512|  
    |8 个处理器|288|576|  
    |16 个处理器|352|704|  
    |32 个处理器|480|960|  
    |64 个处理器|736|1472|  
    |128 个处理器|4224|4480|  
    |256 个处理器|8320|8576|  
  
    > [!NOTE]  
    >  有关使用 64 个以上的 CPU 的建议，请参考 [在具有超过 64 个 CPU 的计算机上运行 SQL Server 的最佳做法](https://technet.microsoft.com/library/ee210547\(SQL.105\).aspx)。  
  
    > [!WARNING]  
    >  我们建议对于 32 位计算机上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，最大工作线程数为 1024。  
  
-   如果所有工作线程因为长时间运行的查询而处于活动状态， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能停止响应，直到一个工作线程完成并变成可用。 虽然这不是缺点，但有时用户可能并不希望如此。 如果进程显示为停止响应并且不再处理新查询，则将使用专用管理员连接 (DAC) 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并关闭此进程。 为避免此种情况发生，请增大最大工作线程数。  
  
 **max worker threads** 服务器配置选项不考虑所有系统任务（例如可用性组、Service Broker、锁管理器等）所需的线程。  如果超过了配置的线程数目，下列查询将提供有关生成了附加线程的系统任务的信息。  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNERJOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 默认情况下，所有用户都具备不带参数或仅带第一个参数的 **sp_configure** 的执行权限。 若要执行带两个参数的 **sp_configure** 以更改配置选项或运行 RECONFIGURE 语句，则用户必须具备 ALTER SETTINGS 服务器级别的权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>配置 max worker threads 选项  
  
1.  在对象资源管理器中，右键单击服务器并选择 **“属性”** 。  
  
2.  单击 **“处理器”** 节点。  
  
3.  在 "**最大工作线程数**" 框中，键入或选择一个介于128和32767之间的值。  
  
     使用 **max worker threads** 选项配置可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的工作线程数。 **max worker threads** 的默认设置适用于大多数系统。 不过，根据您的系统配置，有时将 **max worker threads** 设置为较小的值会提高性能。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>配置 max worker threads 选项  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例说明如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 将 `max worker threads` 选项的值配置为 `900`。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。  
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a> 跟进：在配置“最大工作线程数”选项后  
 此更改将立即生效，而无需重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [用于数据库管理员的诊断连接](diagnostic-connection-for-database-administrators.md)  
  
  
