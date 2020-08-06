---
title: 创建和应用初始快照 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b7ac008fe139adf55376bb50fbf60dddcd6b9ae5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578135"
---
# <a name="create-and-apply-the-initial-snapshot"></a>创建并应用初始快照
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建和应用初始快照。 使用参数化筛选器的合并发布需要由两部分组成的快照。 有关详细信息，请参阅 [为包含参数化筛选器的合并发布创建快照](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
 **本主题内容**  
  
-   **创建和应用初始快照，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 默认情况下，如果运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理，在使用新建发布向导创建发布后，快照代理将立即生成快照。 然后，默认情况下将由分发代理（对于快照复制和事务复制）或合并代理（对于合并订阅）把此快照应用于所有订阅。 还可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和复制监视器生成快照。 有关启动复制监视器的信息，请参阅[启动复制监视器](monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>在 Management Studio 中创建快照  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要为其创建快照的发布，然后单击 **“查看快照代理状态”** 。  
  
4.  在“查看快照代理状态 - \<Publication>”对话框中，单击“启动” 。  
  
 快照代理生成快照后，将显示一条消息，例如“[100%] 已生成 17 个项目的快照”。  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>在复制监视器中创建快照  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击要为其生成快照的发布，再单击 **“生成快照”** 。  
  
3.  若要查看快照代理的状态，请单击 **“代理”** 选项卡。有关更多详细信息，请右键单击网格中的快照代理，再单击 **“查看详细信息”** 。  
  
#### <a name="to-apply-a-snapshot"></a>应用快照  
  
1.  快照生成后，通过用分发代理或合并代理同步订阅来应用此快照：  
  
    -   如果代理设置为连续运行（事务复制下的默认设置），则快照生成后将自动应用。  
  
    -   如果代理设置为根据计划运行，则在安排代理下次运行时应用快照。  
  
    -   如果代理设置为按需运行，则在您下次运行代理时应用快照。  
  
     有关同步订阅的详细信息，请参阅 [Synchronize a Push Subscription](synchronize-a-push-subscription.md) 和 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)文件夹中打开。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可通过创建并运行快照代理作业或通过批处理文件运行快照代理可执行文件，以编程方式创建初始快照。 初始快照生成后，该快照将在订阅首次同步时传输并应用到订阅服务器。 如果您在命令提示符处或通过批处理文件运行快照代理，则只要现有快照变为无效，您就需要重新运行此代理。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>创建并运行快照代理作业以生成初始快照  
  
1.  创建快照发布、事务发布或合并发布。 有关详细信息，请参阅 [Create a Publication](publish/create-a-publication.md)。  
  
2.  执行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql)。 指定 **@publication** 和以下参数：  
  
    -   **@job_login，用于指定**快照代理在分发服务器上运行时所用的 Windows 身份验证凭据。  
  
    -   **@job_password**，为提供的 Windows 凭据的密码。  
  
    -   （可选）如果代理在连接到发布服务器时将使用 SQL Server 身份验证，则将 **@publisher_security_mode** 的值指定为 **@publisher_security_mode** 。 在这种情况下，你还必须为和指定 SQL Server 身份验证登录信息 **@publisher_login** **@publisher_password** 。  
  
    -   （可选）快照代理作业的同步计划。 有关详细信息，请参阅 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
3.  向发布添加项目。 有关详细信息，请参阅 [定义项目](publish/define-an-article.md)。  
  
4.  在发布服务器上，对发布数据库执行 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql)，并指定步骤 1 中 **@publication** 的值。  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>运行快照代理以生成初始快照  
  
1.  创建快照发布、事务发布或合并发布。 有关详细信息，请参阅 [Create a Publication](publish/create-a-publication.md)。  
  
2.  向发布添加项目。 有关详细信息，请参阅 [定义项目](publish/define-an-article.md)。  
  
3.  在命令提示符处或批处理文件中，通过运行 [snapshot.exe](agents/replication-snapshot-agent.md) 并指定下列命令行参数，启动 **复制合并代理**：  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     如果您使用的是 SQL Server 身份验证，则还必须指定下列参数：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** =  **\@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** =  **\@publisher_security_mode**  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例演示如何创建事务发布，并为新的发布添加快照代理作业（使用 **sqlcmd** 脚本变量）。 此示例还启动该作业。  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubinitialsnapshot.sql#sp_trangenerate_snapshot)]  
  
 此示例创建一个合并发布，并为此发布添加一个快照代理作业（使用 **sqlcmd** 变量）。 此示例还启动该作业。  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubinitialsnapshot.sql#sp_mergegenerate_snapshot)]  
  
 以下命令行参数启动快照代理，以为合并发布生成快照。  
  
> [!NOTE]  
>  为便于阅读，添加了换行符。 但在批处理文件中，命令必须位于一行中。  
  
 [!code-sql[HowTo#startmergesnapshot_10](../../snippets/tsql/SQL15/replication/howto/tsql/createmergesnapshot_10.bat)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 快照代理将在创建发布后生成快照。 可以使用复制管理对象 (RMO) 和直接托管代码对复制代理功能的访问权限以编程的方式生成这些快照。 所使用的对象取决于复制的类型。 可以使用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 对象同步启动快照代理，也可以使用代理作业异步启动快照代理。 初始快照生成后，该快照将在订阅首次同步时传输并应用到订阅服务器。 只要现有快照不再包含有效的最新数据，您就需要重新运行代理。 有关详细信息，请参阅[维护发布](publish/maintain-publications.md)。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../includes/msconame-md.md)] （加密服务）。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>通过启动快照代理作业（异步）为快照发布或事务发布生成初始快照  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.TransPublication> 类的实例。 设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以加载该对象的其余属性。 如果此方法返回 `false`，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值为 `false`，请调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 为此发布创建快照代理作业。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法以启动为此发布生成快照的代理作业。  
  
6.  （可选）<xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> 的值为 `true` 时，订阅服务器具有快照。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>通过运行快照代理（同步）为快照发布或事务发布生成初始快照  
  
1.  创建 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 类的实例，并设置下列所需属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 发布服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 发布数据库的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 发布的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 分发服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 表示连接到发布服务器时使用 Windows 身份验证，值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 以及值为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 表示连接到发布服务器时使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 建议使用 Windows 身份验证。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 表示连接到分发服务器时使用 Windows 身份验证，值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 以及值为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 表示连接到分发服务器时使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 建议使用 Windows 身份验证。  
  
2.  将 <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> 的值设置为 <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> 或 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>通过启动快照代理作业（异步）为合并发布生成初始快照  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.MergePublication> 类的实例。 设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以加载该对象的其余属性。 如果此方法返回 `false`，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  如果 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> 的值为 `false`，请调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 为此发布创建快照代理作业。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> 方法以启动为此发布生成快照的代理作业。  
  
6.  （可选）<xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> 的值为 `true` 时，订阅服务器具有快照。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>通过运行快照代理（同步）为合并发布生成初始快照  
  
1.  创建 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> 类的实例，并设置下列所需属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - 发布服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - 发布数据库的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - 发布的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - 分发服务器的名称  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - 值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 表示连接到发布服务器时使用 Windows 身份验证，值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 以及值为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> 表示连接到发布服务器时使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 建议使用 Windows 身份验证。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - 值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> 表示连接到分发服务器时使用 Windows 身份验证，值为 <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 以及值为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> 表示连接到分发服务器时使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 建议使用 Windows 身份验证。  
  
2.  将 <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> 的值设置为 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> 方法。  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 示例 (RMO)  
 此示例同步运行快照代理，为事务发布生成初始快照。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 此示例异步启动代理作业，为事务发布生成初始快照。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](publish/create-a-publication.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [Specify Synchronization Schedules](specify-synchronization-schedules.md)   
 [创建并应用快照](create-and-apply-the-snapshot.md)   
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [将 sqlcmd 与脚本变量结合使用](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
