---
title: 管理可用性组数据库的登录名和作业 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: d7da14d3-848c-44d4-8e49-d536a1158a61
author: rothja
ms.author: jroth
ms.openlocfilehash: 457f3ef946b5cfaf86a4a19774af63c5d7635882
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591523"
---
# <a name="management-of-logins-and-jobs-for-the-databases-of-an-availability-group-sql-server"></a>管理可用性组中数据库的登录名和作业 (SQL Server)
  您应当定期维护 AlwaysOn 可用性组的每个主数据库及其相应的辅助数据库上的同一组用户登录名和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 代理作业。 在为可用性组承载可用性副本的每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上，必须重新生成这些登录名和作业。  
  
-   **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理作业**  
  
     您需要手动将相关作业从承载原始主副本的服务器实例复制到承载原始辅助副本的服务器实例上。 对于所有数据库，您需要在每个相关作业开始时添加逻辑，以使该作业仅在主数据库上执行，也就是说，仅在逻辑副本是数据库的主副本时执行。  
  
     承载可用性组的可用性副本的服务器实例的配置可能有所不同，如具有不同的磁带机号等。 每个可用性副本的作业必须允许可能存在的此类差异。  
  
     请注意，备份作业可以使用 [sys.fn_hadr_is_preferred_backup_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 函数根据可用性组备份首选项，标识本地副本是否为用于备份的首选副本。 使用 [维护计划向导](../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md) 创建的备份作业默认使用此函数。 对于其他备份作业，我们建议您将此函数用作您的备份作业中的一个条件，以便仅在首选副本上执行它们。 有关详细信息，请参阅[活动辅助副本：辅助副本上的备份 (AlwaysOn 可用性组) ](availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。  
  
-   **登录名**  
  
     如果使用的是包含数据库，您可以配置数据库中的包含用户，对于这些用户，您不必在承载辅助副本的服务器实例上创建登录名。 对于非包含可用性数据库，您需要在承载可用性副本的服务器实例上为这些登录名创建用户。 有关详细信息，请参阅 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)。  
  
     如果您的任何应用程序使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证或本地 Windows 登录名，请参阅本主题后面的 [使用 SQL Server 身份验证或本地 Windows 登录名的应用程序的登录名](../../2014/database-engine/logins-and-jobs-for-availability-group-databases.md#SSauthentication)。  
  
    > [!NOTE]  
    >  在服务器实例上未定义或错误定义了其相应 SQL Server 登录名的数据库用户无法登录到实例。 这样的用户被称为此服务器实例上的数据库的“孤立用户” ** 。 如果给定服务器实例上存在孤立用户，您可以随时设置用户登录名。 有关详细信息，请参阅 [孤立用户故障排除 (SQL Server)](../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)。  
  
-   **其他元数据**  
  
     在承载某一给定可用性组的辅助副本的各服务器实例上，登录名和作业不是需要重新创建的唯一信息。 例如，您可能需要重新创建服务器配置设置、凭据、加密的数据、权限、复制设置、Service Broker 应用程序、触发器（在服务器级别）等。 有关详细信息，请参阅 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
##  <a name="logins-of-applications-that-use-sql-server-authentication-or-a-local-windows-login"></a><a name="SSauthentication"></a> 使用 SQL Server 身份验证或本地 Windows 登录名的应用程序的登录名  
 如果某一应用程序使用 SQL Server 身份验证或本地 Windows 登录名，则不匹配的 SID 可能会阻止该应用程序的登录名在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的远程实例上解析。 不匹配的 SID 将导致该登录名成为远程服务器实例上的孤立用户。 当应用程序连接到发生故障转移后的镜像数据库或日志传送数据库，或是连接到从备份初始化的复制订阅服务器数据库时，就可能会发生此问题。  
  
 为了避免此问题，我们建议您在设置此类应用程序时采取预防措施，以便使用由 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的远程实例承载的数据库。 预防措施包括将登录名和密码从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的本地实例传输到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的远程实例。 有关如何避免此问题的详细信息，请参阅知识库文章 918992（[如何在 SQL Server 实例间传输登录名和密码](https://support.microsoft.com/kb/918992/)）。  
  
> [!NOTE]  
>  这个问题会影响不同计算机上的 Windows 本地帐户。 但是，这个问题不会在域帐户上发生，因为 SID 在每台计算机上都是相同的。  
  
 有关详细信息，请参阅 [与数据库镜像和日志传送有关的孤立用户](https://blogs.msdn.com/b/sqlserverfaq/archive/2009/04/13/orphaned-users-with-database-mirroring-and-log-shipping.aspx) （数据库引擎博客）。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [创建登录名](../relational-databases/security/authentication-access/create-a-login.md)  
  
-   [创建数据库用户](../relational-databases/security/authentication-access/create-a-database-user.md)。  
  
-   [创建作业](../ssms/agent/create-a-job.md)  
  
-   [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [包含的数据库](../relational-databases/databases/contained-databases.md)   
 [创建作业](../ssms/agent/create-jobs.md)  
  
  
