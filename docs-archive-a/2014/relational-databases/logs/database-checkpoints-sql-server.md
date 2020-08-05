---
title: 数据库检查点 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/13/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5776d4a23223637c50ac40098fa44342d5cd94a9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580736"
---
# <a name="database-checkpoints-sql-server"></a>数据库检查点 (SQL Server)
  本节提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库检查点的概述。  “检查点”会创建一个已知的正常点，在意外关闭或崩溃后进行恢复的过程中， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 可以从该点开始应用日志中所包含的更改。  
  
  
##  <a name="overview-of-checkpoints"></a><a name="Overview"></a>检查点概述  
 出于性能方面的考虑，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 对内存（缓冲区缓存）中的数据库页进行修改，但在每次更改后不将这些页写入磁盘。 相反， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 定期发出对每个数据库的检查点命令。 ** “检查点”将当前内存中已修改的页（称为“脏页” **）和事务日志信息从内存写入磁盘，并记录有关事务日志的信息。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 支持几种类型的检查点：自动、间接、手动和内部。 下表总结了检查点类型。  
  
|名称|[!INCLUDE[tsql](../../includes/tsql-md.md)] 接口|说明|  
|----------|----------------------------------|-----------------|  
|自动|EXEC sp_configure **" `recovery interval` "、" *`seconds`* "**|自动在后台发出，以满足服务器配置选项建议的时间上限 `recovery interval` 。 运行自动检查点直到完成。  基于未完成的写操作数和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是否检测到写入滞后时间超过 20 毫秒的写操作增加，来调控自动检查点。<br /><br /> 有关详细信息，请参阅 [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)。|  
|间接|更改数据库 .。。将 TARGET_RECOVERY_TIME **=** _target_recovery_time_设置为 {秒 &#124; 分钟}|在后台发出，以满足给定数据库的用户指定的目标恢复时间要求。 默认目标恢复时间为 0，这将导致对数据库使用自动检查点试探方法。 如果您使用 ALTER DATABASE 并将 TARGET_RECOVERY_TIME 设置为 >0，则将使用此值替代为服务器实例指定的恢复间隔。<br /><br /> 有关详细信息，请参阅 [更改数据库的目标恢复时间 (SQL Server)](change-the-target-recovery-time-of-a-database-sql-server.md)服务器配置选项。|  
|手动|CHECKPOINT [ *checkpoint_duration* ]|执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] CHECKPOINT 命令时发出。 在连接的当前数据库中执行手动检查点操作。 默认情况下，手动检查点运行至完成。 调控方式与自动检查点的调控方式相同。  （可选） *checkpoint_duration* 参数指定完成检查点所需的时间（秒）。<br /><br /> 有关详细信息，请参阅 [检查点 (Transact-SQL)](/sql/t-sql/language-elements/checkpoint-transact-sql)。|  
|内部|无。|由各种服务器操作（如备份和数据库快照创建）发出，以确保磁盘映像与日志的当前状态匹配。|  
  
> [!NOTE]  
>  `-k`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高级设置选项允许数据库管理员基于某些检查点类型 I/O 子系统的吞吐量来调控检查点 I/O 行为。 `-k`设置选项适用于自动检查点和任何其他调控的手动和内部检查点。  
  
 对于自动、手动和内部检查点，在数据库恢复期间只有在最新检查点后所做的修改需要前滚。 这将减少恢复数据库所需的时间。  
  
> [!IMPORTANT]  
>  长时间运行的未提交的事务会增加所有类型的检查点的恢复时间。  
  
  
  
###  <a name="interaction-of-the-target_recovery_time-and-recovery-interval-options"></a><a name="InteractionBwnSettings"></a> TARGET_RECOVERY_TIME 和“recovery interval”选项的相互影响  
 下表总结了服务器范围**sp_configure " `recovery interval` "** 设置和数据库特定的 ALTER database .。。TARGET_RECOVERY_TIME 设置。  
  
|target_recovery_time|'recovery interval'|使用的检查点类型|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|目标恢复间隔为 1 分钟的自动检查点。|  
|0|>0|自动检查点，其目标恢复间隔由 **sp_configurerecovery interval** 选项的用户定义的设置指定。|  
|>0|不适用。|间接检查点，其目标恢复时间由 TARGET_RECOVERY_TIME 设置确定，以秒为单位。|  
  
###  <a name="automatic-checkpoints"></a><a name="AutomaticChkpt"></a>自动检查点  
 每当日志记录数达到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 其可以在服务器配置选项指定的时间内处理的估计值时，将发生自动检查点 `recovery interval` 。 在没有用户定义的目标恢复时间的每个数据库中， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 生成自动检查点。 自动检查点的频率取决于 `recovery interval` advanced server 配置选项，该选项指定给定的服务器实例在系统重新启动期间用于恢复数据库的最长时间。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将估计它可在恢复间隔内处理的最大日志记录数。 使用自动检查点的数据库达到此最大日志记录数后， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将对该数据库发出一个检查点命令。 自动检查点之间的时间间隔可以变化很大。 具有大量事务工作负荷的数据库的检查点生成频率将高于主要用于只读操作的数据库的检查点生成频率。  
  
 此外，在简单恢复模式下，如果日志填充 70％，则自动检查点还将排队。  
  
 在简单恢复模式下，除非某些因素延迟了日志截断，否则自动检查点将截断事务日志中没有使用的部分。 相反，在完整恢复模式或大容量日志恢复模式下，一旦建立了日志备份链，自动检查点将不导致日志截断。 有关详细信息，请参阅 [事务日志 (SQL Server)](the-transaction-log-sql-server.md)。  
  
 在系统崩溃后恢复给定数据库所需的时间主要取决于重做崩溃时的脏页所需的随机 I/O 量。 这意味着该 `recovery interval` 设置是不可靠的。 它不能确定准确的恢复持续时间。 此外，正在执行自动检查点操作时，数据的常规 I/O 活动显著增加并且无法预测。  
  
  
####  <a name="impact-of-recovery-interval-on-recovery-performance"></a><a name="PerformanceImpact"></a>恢复间隔对恢复性能的影响  
 对于使用短事务 (OLTP) 系统进行联机事务处理， `recovery interval` 确定恢复时间的主要因素。 但是，该 `recovery interval` 选项不影响撤消长时间运行的事务所需的时间。 恢复具有长时间运行事务的数据库所需的时间可能比选项中指定的时间长得多 `recovery interval` 。 例如，如果长时间运行的事务在服务器实例禁用前花费了两个小时来执行更新，则实际恢复所需的时间比 `recovery interval` 恢复长事务的值长。 有关长时间运行的事务对恢复时间的影响的详细信息，请参阅 [事务日志 (SQL Server)](the-transaction-log-sql-server.md)。  
  
 通常情况下，默认值提供了最佳恢复性能。 但是，在以下情况下更改恢复间隔可能会提高性能：  
  
-   如果例行恢复所需的时间在长时间运行的事务未回滚时超过 1 分钟。  
  
-   如果您注意到频繁的检查点操作损害了数据库的性能。  
  
 如果您决定增大 `recovery interval` 设置，我们建议一点一点逐渐增大该值并评估每次增大对恢复性能的影响。 此方法非常重要，因为在 `recovery interval` 设置增加时，数据库恢复需要更长的时间来完成。 例如，如果更改 `recovery interval` 10，则完成恢复所用的时间大约比设置为零时长10倍 `recovery interval` 。  
  
  
###  <a name="indirect-checkpoints"></a><a name="IndirectChkpt"></a>间接检查点  
 间接检查点是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中引入的新检查点类型，它提供自动检查点的可配置数据库级替代方法。 在系统崩溃时，间接检查点与自动检查点相比，恢复时间可能更短更可预测。 间接检查点具有以下优点：  
  
-   为间接检查点配置的数据库上的联机事务工作负荷可能导致性能下降。 间接检查点确保损坏页的数量低于特定阙值，以便在目标恢复时间内完成数据库恢复。 与利用损坏页数量的间接检查点相反，恢复间隔配置选项使用事务数量来确定恢复时间。 当在接收大量 DML 操作的数据库上启用了间接检查点时，后台写入线程可以开始积极刷新磁盘的脏缓冲区，以确保执行恢复所需的时间在数据库所设目标恢复时间范围内。 这可能造成某些系统上出现额外的 I/O 活动，如果磁盘子系统在 I/O 阙值之上或附近运行，则这会导致性能瓶颈。  
  
-   间接检查点使您可以通过控制 REDO 期间随机 I/O 的开销来可靠控制数据库恢复时间。 这使服务器实例不超过给定数据库的恢复时间上限（长时间运行的事务导致过多 UNDO 时间时除外）。  
  
-   间接检查点通过在后台不断地将脏页写入磁盘来减小与检查点有关的 I/O 蜂值。  
  
 但是，为间接检查点配置的数据库上的联机事务工作负荷可能导致性能下降。 这是因为间接检查点使用的后台写入线程有时增加了服务器实例的总写入负荷。  
  
  
###  <a name="internal-checkpoints"></a><a name="EventsCausingChkpt"></a>内部检查点  
 内部检查点由各种服务器组件生成，以确保磁盘映像与日志的当前状态匹配。 生成内部检查点以响应下列事件：  
  
-   已经使用 ALTER DATABASE 添加或删除了数据库文件。  
  
-   进行了数据库备份。  
  
-   创建了数据库快照，不管 DBCC CHECK 是显式还是内部执行。  
  
-   执行了需要关闭数据库的活动。 例如，AUTO_CLOSE 设置为 ON 并且关闭了数据库的最后一个用户连接，或者执行了需要重新启动数据库的数据库选项更改。  
  
-   通过停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服务停止了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 任一操作都会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个数据库中生成一个检查点。  
  
-   使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例 (FCI) 脱机。  
  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **更改服务器实例的恢复间隔**  
  
-   [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **配置数据库的间接检查点**  
  
-   [更改数据库的目标恢复时间 (SQL Server)](change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **对数据库发出手动检查点命令**  
  
-   [检查点 (Transact-SQL)](/sql/t-sql/language-elements/checkpoint-transact-sql)  
  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相关内容  
  
-   [事务日志物理体系结构](https://technet.microsoft.com/library/ms179355.aspx) （ [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 联机丛书中）  
  
  
## <a name="see-also"></a>另请参阅  
 [事务日志 (SQL Server)](the-transaction-log-sql-server.md)  
  
  
