---
title: 增强合并复制性能 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 41dc258e9b45e9839ad142e73cb145999d02986c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693778"
---
# <a name="enhance-merge-replication-performance"></a>增强合并复制性能
  在考虑 [增强事务复制性能](enhance-general-replication-performance.md)中介绍的常规性能提示后，还需要考虑特定于合并复制的其他几个方面。  
  
## <a name="database-design"></a>数据库设计  
  
-   对行筛选器和联接筛选器中使用的列建立索引。  
  
     在发布的项目上使用行筛选器时，则对筛选器的 WHERE 子句中使用的每一列创建索引。 如果不创建索引，[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 必须先读取表中的每一行来确定该行是否应包含在分区中。 使用索引， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可快速找到要包括的行。 如果复制只根据索引就能完全解析筛选器的 WHERE 子句，处理速度将最快。  
  
     对联接筛选器中使用的所有列进行索引也很重要。 每当合并代理运行时，它都会搜索基表来确定父表中及相关表中的哪些行包括在分区中。 对联接的列创建索引可避免每当合并代理运行时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 都读取表中的每一行。  
  
     有关筛选的详细信息，请参阅[为合并复制筛选已发布数据](../merge/filter-published-data-for-merge-replication.md)。  
  
-   考虑过度规范包括大型对象 (LOB) 数据类型的表。  
  
     发生同步时，合并代理可能需要从分发服务器或订阅服务器读取和传输整个数据行。 如果该行包含使用 LOB 的列，即使这些列可能尚未更新，此过程也会要求增加内存分配并可能对性能产生负面影响。 为减少对性能产生负面影响的可能性，可考虑将 LOB 列放在一个单独的表中并对其余的行数据采用一对一关系。 不推荐使用数据类型 `text`、`ntext` 和 `image`。 如果确实要包括 LOB，建议分别使用数据类型 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)`。  
  
## <a name="publication-design"></a>发布设计  
  
-   使用发布兼容级别 90RTM（[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本）。  
  
     除非有一台或多台订阅服务器使用不同版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，否则指定发布必须仅支持 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本。 这使发布可以利用新功能和性能优化。  
  
-   使用适当的发布保持期设置。  
  
     发布保持期是必须同步订阅之前等待的最长时间，用来确定存储跟踪元数据的时间。 较高的值可能会影响存储和处理性能。 有关如何设置发布保持期的详细信息，请参阅 [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md)。  
  
-   对仅在发布服务器上更改的那些表使用仅下载项目。 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](../merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
### <a name="filter-design-and-use"></a>筛选器设计和用法  
  
-   限制行筛选器子句的复杂性。  
  
     限制筛选条件的复杂性有助于提高合并代理评估要发送给订阅服务器的行更改时的性能。 避免在合并行筛选器子句中使用嵌套的 SELECT 语句。 应考虑使用联接筛选器，它在根据一个表中的行筛选器子句分区另一个表中的数据时通常更为有效。 有关筛选的详细信息，请参阅[为合并复制筛选已发布数据](../merge/filter-published-data-for-merge-replication.md)。  
  
-   通过参数化筛选器使用预计算分区（默认情况下使用此功能）。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
     预计算分区会对筛选行为施加许多限制。 如果您的应用程序无法遵守这些限制，请将 **keep_partition_changes** 选项设置为 **True**，这样设置对性能有利。 有关详细信息，请参阅 [参数化行筛选器](../merge/parameterized-filters-parameterized-row-filters.md)。  
  
-   如果数据已经筛选但未在用户之间共享，请使用不重叠的分区。  
  
     复制可优化未在分区或订阅之间共享的数据的性能。 有关详细信息，请参阅 [参数化行筛选器](../merge/parameterized-filters-parameterized-row-filters.md)。  
  
-   不要创建复杂的联接筛选器层次结构。  
  
     包含五个或更多表的联接筛选器在合并处理过程中会极大地影响性能。 如果要生成包含五个或更多表的联接筛选器，建议最好考虑其他解决方案：  
  
    -   避免筛选的表主要有：查找表、较小的表以及未经更改的表。 使这些表整个作为发布的组成部分。 建议仅在那些必须在订阅服务器之中对其进行分区的表之间使用联接筛选器。 有关详细信息，请参阅 [Join Filters](../merge/join-filters.md)。  
  
    -   如果一个联接中存在大量的表，则考虑反规范数据库设计或使用映射表。 例如，如果一个销售人员只需要其客户的数据，但需要六个联接来将客户与销售人员相关联，则考虑向此客户表中添加一个用于标识该销售人员的列。 该销售人员的数据是多余的，但反规范表的开销与复制分区的性能收益比较而言，可能有点过高。  
  
    -   若要在批处理包含大量数据更改时提供预计算分区的性能，请谨慎设计您的应用程序。 请确保联接筛选器父表中的数据更改在子表中的对应更改之前进行。  
  
-   如果逻辑上允许，请将 **join_unique_key** 选项设置为 **1** 。  
  
     将此参数设置为 **1** 表明联接筛选器中子表和父表之间的关系是一对一或一对多。 仅当子表的联接列上有保证唯一性的约束时才将此参数设置为 **1** 。 如果该参数错误地设置为 **1** ，数据可能无法收敛。 有关详细信息，请参阅 [Join Filters](../merge/join-filters.md)。  
  
-   使用预计算分区时，请避免执行包含大量更改的批处理。  
  
     如果在运行了包含大量数据更改的批处理后运行合并代理，则代理会尝试将大型批处理分解为较小的批处理。 在此期间，其他合并代理进程可能会被阻止。 请考虑减少单个批处理中的更改数量并在批处理之间运行合并代理。 如果无法执行此操作，请增加发布的 **generation_leveling_threshold** 值。  
  
## <a name="subscription-considerations"></a>订阅注意事项  
  
-   交错订阅同步计划。  
  
     如果大量订阅服务器需要与发布服务器同步，则考虑将计划交错开，以便合并代理在不同时间运行。 有关详细信息，请参阅 [Specify Synchronization Schedules](../specify-synchronization-schedules.md)。  
  
## <a name="merge-agent-parameters"></a>合并代理参数  
 有关合并代理及其参数的详细信息，请参阅 [Replication Merge Agent](../agents/replication-merge-agent.md)。  
  
-   将请求订阅的所有订阅服务器升级到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本。  
  
     将订阅服务器升级到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本，即可升级订阅服务器上的订阅所用的合并代理。 若要利用众多新功能和性能优化，则需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的合并代理。  
  
-   如果通过快速连接来同步订阅，并通过发布服务器和订阅服务器发送更改，请为合并代理使用 ParallelUploadDownload 参数****。  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引入了一个新的合并代理参数：-ParallelUploadDownload****。 设置此参数能够使合并代理并行处理上载到发布服务器和下载到订阅服务器的更改。 这对于使用高速网络带宽的大容量环境非常有用。 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
    -   [处理复制代理配置文件](../agents/replication-agent-profiles.md)  
  
    -   [查看和修改复制代理命令提示符参数 (SQL Server Management Studio)](../agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
-   考虑提高 **-MakeGenerationInterval** 参数的值，特别是当同步所包含的订阅服务器上载多于订阅服务器下载时。  
  
-   当同步具有大量数据的数据行时，例如具有 LOB 列的行，Web 同步会要求增加内存分配并可能降低性能。 这发生在合并代理生成的 XML 消息包含太多具有大量数据的数据行时。 如果合并代理在 Web 同步期间使用的资源太多，则可以按下列方式之一减少单条消息中发送的行数。  
  
    -   对合并代理使用慢速链接代理配置文件。 有关详细信息，请参阅 [Replication Agent Profiles](../agents/replication-agent-profiles.md)。  
  
    -   将合并代理的 **-DownloadGenerationsPerBatch** 和 **-UploadGenerationsPerBatch** 参数减小为一个小于或等于 10 的值。 这些参数的默认值为 50。  
  
## <a name="snapshot-considerations"></a>快照注意事项  
  
-   在生成初始快照之前，在大型表上创建 ROWGUIDCOL 列。  
  
     合并复制要求每个发布的表都具有 ROWGUIDCOL 列。 如果在快照代理创建初始快照文件之前表中不存在 ROWGUIDCOL 列，那么此代理必须首先添加并填充 ROWGUIDCOL 列。 为了在合并复制期间生成快照时提高性能，请于发布前在每个表上创建 ROWGUIDCOL 列。 该列可以使用任何名称（默认情况下，快照代理使用**rowguid** ），但必须包含下列数据类型特征：  
  
    -   UNIQUEIDENTIFIER 数据类型。  
  
    -   NEWSEQUENTIALID() 或 NEWID() 的默认值。 建议使用 NEWSEQUENTIALID()，因为在进行更改和跟踪更改时，它可以提高性能。  
  
    -   ROWGUIDCOL 属性集。  
  
    -   列的唯一索引。  
  
-   预先生成快照和/或允许订阅服务器在第一次同步时请求生成快照和应用快照。  
  
     使用以上选项中的一个或两个可以为使用参数化筛选器的发布提供快照。 如果未指定任一选项，将使用一系列的 SELECT 和 INSERT 语句初始化订阅，而不是使用 **bcp** 实用工具；此过程的速度将更慢。 有关详细信息，请参阅 [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
## <a name="maintenance-and-monitoring-considerations"></a>维护与监视注意事项  
  
-   不定期地重新对合并复制系统表建立索引。  
  
     在合并复制维护过程中，应不定期检查以下与合并复制相关联的系统表的增长情况： **MSmerge_contents**、 **MSmerge_genhistory**、 **MSmerge_tombstone**、 **MSmerge_current_partition_mappings**、 **MSmerge_past_partition_mappings**。 定期对这些表重建索引。 有关详细信息，请参阅 [重新组织和重新生成索引](../../indexes/reorganize-and-rebuild-indexes.md)。  
  
-   使用复制监视器中的 **“同步历史记录”** 选项卡监视同步性能。  
  
     对于合并复制，复制监视器会在 **“同步历史记录”** 选项卡中显示同步过程中所处理的每个项目的详细统计信息，其中包括每个处理阶段（如上载更改、下载更改等）所用的时间。 它可帮助查明导致速度降低的特定表，是用来解决合并订阅性能问题的最佳途径。 有关查看详细统计信息详细信息，请参阅[使用复制监视器查看信息和执行任务](../monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
  
