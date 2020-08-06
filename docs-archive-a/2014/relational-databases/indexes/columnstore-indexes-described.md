---
title: 描述的列存储索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexes creation, columnstore
- indexes [SQL Server], columnstore
- columnstore index
- columnstore index, described
- xVelocity, columnstore indexes
ms.assetid: f98af4a5-4523-43b1-be8d-1b03c3217839
author: mikeraymsft
ms.author: mikeray
ms.openlocfilehash: 80a29b8e8cc5b53c09369156a5cf5f717e9447a0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693318"
---
# <a name="columnstore-indexes-described"></a>Columnstore Indexes Described
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]*内存中*列存储索引通过使用基于列的数据存储和基于列的查询处理来存储和管理数据。 列存储索引适合于主要执行大容量加载和只读查询的数据仓库工作负荷。 与传统面向行的存储方式相比，使用列存储索引存档可最多提高 **10 倍查询性能** ，与使用非压缩数据大小相比，可提供多达 **7 倍数据压缩率** 。

> [!NOTE]
>  我们将聚集列存储索引视为存储大型数据仓库事实表的标准，希望它可在大多数数据仓库方案中使用。 由于聚集列存储索引是可更新的，因此工作负荷可执行大量插入、更新和删除操作。

## <a name="contents"></a>目录

-   [基础知识](#basics)

-   [正在加载数据](#dataload)

-   [性能提示](#performance)

-   [相关任务和主题](#related)

##  <a name="basics"></a><a name="basics"></a>传授
 *columnstore index* 是使用列式数据格式（称为列存储）存储、检索和管理数据的技术。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持聚集列存储索引和非聚集列存储索引。 这两种索引都使用相同的内存中列存储技术，但它们在用途和支持的功能上存在差异。

###  <a name="benefits"></a><a name="benefits"></a> 优势
 列存储索引适合于对大型数据集执行分析的大多数只读查询。 通常，列存储索引是针对数据仓库工作负荷的查询。 列存储索引为使用全表扫描的查询带来很大的性能好处，但不适合于查找数据并且搜索特定值的查询。

 列存储索引的优点：

-   列通常具有相似的数据，这导致压缩率较高。

-   较高的压缩率通过使用更小的内存中空间提高查询性能。 反过来，因为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以在内存中执行更多查询和数据操作，因此可以提高查询性能。

-   一个称作批处理模式执行的新查询执行机制已添加到 SQL Server 中，它可以极大降低 CPU 使用率。 批处理模式执行与列存储存储格式紧密集成，并且围绕列存储存储格式进行了优化。 批处理模式执行有时候称作基于向量或向量化的执行。

-   查询通常仅从表中选择几列，这减少了从物理介质的总 I/O。

### <a name="columnstore-versions"></a>列存储版本
 SQL Server 2012、SQL Server 2012 并行数据仓库和 SQL Server 2014 全都使用列存储索引来加快常见数据仓库查询的执行速度。 SQL Server 2012 引入了两个新功能：非聚集列存储索引和基于向量的查询执行功能（处理称作“批处理”的单元中的数据）。 SQL Server 2014 除了具有 SQL Server 2012 中的功能之外，还新增了可更新聚集列存储索引。

### <a name="key-characteristics"></a>主要特征

||
|-|
|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。|

 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，聚集列存储索引：

-   在 Enterprise Edition、Developer Edition 和 Evaluation Edition 中提供。

-   可更新。

-   是针对整个表的主要存储方法。

-   没有键列。 所有列均为包含列。

-   是表的唯一索引。 不能与任何其他索引组合使用。

-   可配置为使用列存储或列存储存档压缩。

-   不以排序方式物理存储列。 相反，它存储数据以改进压缩和性能。

||
|-|
|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。|

 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中，非聚集列存储索引：

-   可对聚集索引或堆中列的子集建立索引。 例如，它可以对常用列建立索引。

-   需要附加的存储空间以存储索引中列的副本。

-   通过重新生成索引或切换入和移出分区来进行更新。不能使用 DML 操作（如 insert、update 和 delete）对其进行更新。

-   可以与表中的其他索引结合使用。

-   可配置为使用列存储或列存储存档压缩。

-   不以排序方式物理存储列。 相反，它存储数据以改进压缩和性能。 在创建列存储索引之前对数据预先进行排序不是必需的，但这样做可以改进列存储压缩。

###  <a name="key-concepts-and-terms"></a><a name="Concepts"></a>关键概念和术语
 以下关键概念和术语与列存储索引相关联。

 列存储索引*列存储索引*是一种使用列式数据格式（称为列存储）存储、检索和管理数据的技术。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持聚集列存储索引和非聚集列存储索引。 这两种索引都使用相同的内存中列存储技术，但它们在用途和支持的功能上存在差异。

 列存储：*列*存储是以逻辑方式组织为包含行和列的表，并以列数据格式物理存储的数据。

 行存储是*指*在逻辑上组织为包含行和列的表，然后以按行数据格式物理存储的数据。 这是存储关系表数据的传统方法。

 行组和列段：为了实现高性能和高压缩率，列存储索引将表分为多个行组（称为行组），然后以逐列方式压缩每个行组。 行组中的行数必须足够大，以便提高压缩率，并且足够小，以便从内存中操作中受益。

 行组行*组是同时压缩为列*存储格式的一组行。

 列段：*列段*是行组内的一列数据。

-   每个行组通常可包含的最大行数是 1,048,576 行。

-   每个行组包含表中每个列的一个列段。

-   每个列段一起压缩并且存储于物理介质上。

 ![列段](../../database-engine/media/sql-server-pdw-columnstore-columnsegment.gif "列段")

 非聚集列存储索引*非聚集列存储索引*是在现有聚集索引或堆表上创建的只读索引。 它包含列子集的副本，最高可包含表中的所有列。 如果表包含非聚集列存储索引，则该表为只读。

 借助于非聚集列存储索引，可具有在对原始表执行只读操作的同时运行分析查询的列存储索引。

 ![非聚集列存储索引](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage-nonclustered.gif "非聚集列存储索引")

 聚集列存储索引*聚集列存储索引*是整个表的物理存储，是该表的唯一索引。 聚集索引不可更新。 您可以对索引执行插入、删除和更新操作，并且可以将数据大容量加载到索引中。

 ![聚集列存储索引](../../database-engine/media/sql-server-pdw-columnstore-physicalstorage.gif "聚集列存储索引")

 若要减少列段的碎片和改进性能，列存储索引可能会将一些数据暂时存储于称作增量存储的行存储表中，同时还存储针对已删除行的 ID 的 B 树。 增量存储操作在后台处理。 若要返回正确的查询结果，聚集列存储索引将合并来自列存储和增量存储的查询结果。

 增量存储仅用于聚集列存储索引，*增量存储*是一个行存储表，用于存储行，直到行数足够大，才能移到列存储中。 增量存储用于聚集列存储索引，以便提高加载和其他 DML 操作的性能。

 在大容量加载期间，大多数行直接转到列存储，而不通过增量存储中转。 在大容量加载结束时，某些行的数量可能无法满足行组的最小大小要求（即 102,400 行）。 在发生这种情况时，将最后的这些行转到增量存储而非列存储中。 对于少于 102,400 行的较小的大容量加载，所有行都直接转到增量存储中。

 在增量存储达到最大行数后，它会关闭。 元组-移动过程检查已关闭的行组。 在它找到已关闭行组后，会对其进行压缩并且将其存储到列存储中。

##  <a name="loading-data"></a><a name="dataload"></a>正在加载数据

###  <a name="loading-data-into-a-nonclustered-columnstore-index"></a><a name="dataload_nci"></a>将数据加载到非聚集列存储索引
 若要将数据加载到非聚集列存储索引中，请首先将数据加载到作为堆或聚集索引存储的传统行存储表中，然后使用[CREATE 列存储索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql)创建非聚集列存储索引。

 ![将数据加载到列存储索引中](../../database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "将数据加载到列存储索引中")

 具有非聚集列存储索引的表在该索引被删除或禁用前是只读的。 若要更新表和非聚集列存储索引，您可以切换入和移出分区。您还可以禁用该索引，更新该表，然后重新生成索引。

 有关详细信息，请参阅 [Using Nonclustered Columnstore Indexes](indexes.md)。

###  <a name="loading-data-into-a-clustered-columnstore-index"></a><a name="dataload_cci"></a>将数据加载到聚集列存储索引
 ![加载到聚集列存储索引中](../../database-engine/media/sql-server-pdw-columnstore-loadprocess.gif "加载到聚集列存储索引中")

 按图中所建议的那样，为了将数据加载到聚集列存储索引， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：

1.  直接将最大大小的行组插入列存储。 加载数据时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 按先来先处理的顺序将数据行分配给一个打开的行组。

2.  对于每个行组，在达到最大大小后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：

    1.  将行组标记为“关闭”。

    2.  绕开增量存储。

    3.  使用列存储压缩方式压缩包含该行组的每个列段。

    4.  在物理上将每个压缩的列段存储到列存储中。

3.  按以下方式将其余行插入列存储或增量存储中：

    1.  如果行数满足每个行组的最小行数要求，则将这些行添加到列存储中。

    2.  如果行数小于每个行组的最小行数，则将这些行添加到增量存储中。

 有关增量存储任务和进程的详细信息，请参阅 [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)。

##  <a name="performance-tips"></a><a name="performance"></a>性能提示

### <a name="plan-for-enough-memory-to-create-columnstore-indexes-in-parallel"></a>计划足够的内存以便并行创建列存储索引
 创建列存储索引默认情况下是一种并行操作，除非内存受到约束。 并行创建索引要求比按顺序创建索引更多的内存。 在内存充足的情况下，创建列存储索引相当于在同一列上生成 B 树所用时间的 1.5 倍。

 创建列存储索引所需的内存取决于列数、字符串列的数目、并行度 (DOP) 和数据特性。 例如，如果您的表具有不到 10 亿行，SQL Server 将仅使用一个线程创建列存储索引。

 如果您的表具有超过 10 亿行，但 SQL Server 无法获得足够大的内存授予来使用 MAXDOP 创建索引，SQL Server 将根据需要自动减少 MAXDOP，以便适合可用内存授予。  在某些情况下，DOP 必须减小到一个以便在受到约束的内存下生成索引。

##  <a name="related-tasks-and-topics"></a><a name="related"></a>相关任务和主题

### <a name="nonclustered-columnstore-indexes"></a>非聚集列存储索引
 对于常见任务，请参阅 [Using Nonclustered Columnstore Indexes](../../database-engine/using-nonclustered-columnstore-indexes.md)。

-   [CREATE COLUMNSTORE INDEX (Transact-SQL)](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [ALTER INDEX &#40;](/sql/t-sql/statements/alter-index-transact-sql)具有 REBUILD 的 transact-sql&#41;。

-   [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)

### <a name="clustered-columnstore-indexes"></a>聚集列存储索引
 对于常见任务，请参阅 [Using Clustered Columnstore Indexes](../../database-engine/using-clustered-columnstore-indexes.md)。

-   [&#40;Transact-sql&#41;创建聚集列存储索引](/sql/t-sql/statements/create-columnstore-index-transact-sql)

-   [更改索引 &#40;](/sql/t-sql/statements/alter-index-transact-sql)包含重新生成或重新组织的 transact-sql&#41;。

-   [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)

-   [INSERT (Transact-SQL)](/sql/t-sql/statements/insert-transact-sql)

-   [UPDATE (Transact-SQL)](/sql/t-sql/queries/update-transact-sql)

-   [DELETE (Transact-SQL)](/sql/t-sql/statements/delete-transact-sql)

### <a name="metadata"></a>元数据
 列存储索引中的所有列在元数据中作为包含性列存储。 列存储索引中没有任何键列。

-   [sys.indexes (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)

-   [sys.index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)

-   [sys.partitions (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-partitions-transact-sql)

-   [sys.column_store_segments (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-column-store-segments-transact-sql)

-   [sys.column_store_dictionaries (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql)

-   [sys.column_store_row_groups (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-column-store-row-groups-transact-sql)


