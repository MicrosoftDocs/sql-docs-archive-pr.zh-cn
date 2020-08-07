---
title: 统计信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0f0950e48245bed53581d2f91b120ab9555aa562
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590110"
---
# <a name="statistics"></a>统计信息
  查询优化器使用统计信息来创建可提高查询性能的查询计划。 对于大多数查询，查询优化器已为高质量查询计划生成必要的统计信息；但在少数一些情况下，您需要创建附加的统计信息或修改查询设计以得到最佳结果。 本主题讨论用于高效使用查询优化统计信息的统计信息概念并提供指南。  
  
##  <a name="components-and-concepts"></a><a name="DefinitionQOStatistics"></a> 组件和概念  
 统计信息  
 查询优化的统计信息是一些对象，这些对象包含与值在表或索引视图的一列或多列中的分布有关的统计信息。 查询优化器使用这些统计信息来估计查询结果中的*基数*或行数。 通过这些*基数估计*，查询优化器可以创建高质量的查询计划。 例如，查询优化器可以使用基数估计选择索引查找运算符而不是耗费更多资源的索引扫描运算符，从而提高查询性能。  
  
 每个统计信息对象都在包含一个或多个表列的列表上创建，并且包括显示值在第一列中的分布的直方图。 在多列上的统计信息对象也存储与各列中的值的相关性有关的统计信息。 这些相关性统计信息（或 *密度*）根据列值的不同行的数目派生。 有关统计信息对象的详细信息，请参阅 [DBCC SHOW_STATISTICS (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)。  
  
 筛选的统计信息  
 筛选统计信息可以提高以下从定义完善的数据子集选择数据的查询的查询性能。 筛选统计信息使用筛选器谓词来选择统计信息中包括的数据子集。 与全表统计信息相比，设计完美的筛选统计信息可以改进查询执行计划。 有关筛选器谓词的详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。 有关何时创建筛选的统计信息的详细信息，请参阅本主题中的 [何时创建统计信息](#UpdateStatistics) 部分。 有关案例研究，请参阅 SQLCAT 网站上的博客文章 [Using Filtered Statistics with Partitioned Tables](https://go.microsoft.com/fwlink/?LinkId=178505)（将筛选的统计信息用于分区表）。  
  
 统计信息选项  
 可以设置三个选项来影响何时以及如何创建和更新统计信息。 这些选项仅在数据库级别设置。  
  
 AUTO_CREATE_STATISTICS 选项  
 在自动创建统计信息选项 AUTO_CREATE_STATISTICS 为 ON 时，查询优化器将根据需要在查询谓词中的单独列上创建统计信息，以便改进查询计划的基数估计。 这些单列统计信息在现有统计信息对象中尚未具有直方图的列上创建。 AUTO_CREATE_STATISTICS 选项不确定是否为索引创建了统计信息。 此选项也不生成筛选统计信息。 它严格应用于全表的单列统计信息。  
  
 查询优化器通过使用 AUTO_CREATE_STATISTICS 选项创建统计信息时，统计信息名称以 `_WA`开头。 可以使用下面的查询来确定查询优化器是否为查询谓词列创建了统计信息。  
  
```  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
 AUTO_UPDATE_STATISTICS 选项  
 在自动更新统计信息选项 AUTO_UPDATE_STATISTICS 为 ON 时，查询优化器将确定统计信息何时可能过期，然后在查询使用这些统计信息时更新它们。 统计信息将在插入、更新、删除或合并操作更改表或索引视图中的数据分布后过期。 查询优化器通过计算自最后统计信息更新后数据修改的次数并且将这一修改次数与某一阈值进行比较，确定统计信息何时可能过期。 该阈值基于表中或索引视图中的行数。  
  
 查询优化器在编译查询和执行缓存查询计划前，检查是否存在过期的统计信息。 在编译某一查询前，查询优化器使用查询谓词中的列、表和索引视图确定哪些统计信息可能过期。 在执行缓存查询计划前， [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 确认该查询计划引用最新的统计信息。  
  
 AUTO_UPDATE_STATISTICS 选项适用于为索引创建的统计信息对象、查询谓词中的单列以及使用 [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) 语句创建的统计信息。 此选项也适用于筛选的统计信息。  
  
 AUTO_UPDATE_STATISTICS_ASYNC  
 异步统计信息更新选项 AUTO_UPDATE_STATISTICS_ASYNC 将确定查询优化器是使用同步统计信息更新还是异步统计信息更新。 默认情况下，异步统计信息更新选项被关闭，并且查询优化器以同步方式更新统计信息。 AUTO_UPDATE_STATISTICS_ASYNC 选项适用于为索引创建的统计信息对象、查询谓词中的单列以及使用 [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) 语句创建的统计信息。  
  
 统计信息更新可以是同步（默认设置）或异步的。 对于同步统计信息更新，查询将始终用最新的统计信息编译和执行；在统计信息过期时，查询优化器将在编译和执行查询前等待更新的统计信息。 对于异步统计信息更新，查询将用现有的统计信息编译，即使现有统计信息已过期。如果在查询编译时统计信息过期，查询优化器可以选择非最优查询计划。 在异步更新完成后编译的查询将从使用更新的统计信息中受益。  
  
 执行更改数据分布的操作（例如截断表或对很大百分比的行执行大容量更新）时，考虑使用同步统计信息。 如果您在完成该操作后未更新统计信息，则使用同步统计信息将确保对更改的数据执行查询前统计信息是最新的。  
  
 在以下情况下，考虑使用异步统计信息来实现可预测性更高的查询响应时间：  
  
-   您的应用程序频繁执行相同的查询、类似的查询或类似的缓存查询计划。 与同步统计信息更新相比，使用异步统计信息更新时您的查询响应时间可能具有更高的可预测性，因为查询优化器可以执行传入的查询而不必等待最新的统计信息。 这避免延迟某些查询，而不延迟其他查询。  
  
-   您的应用程序遇到了客户端请求超时，这些超时是由于一个或多个查询正在等待更新后的统计信息所导致的。 在某些情况下，等待同步统计信息可能会导致应用程序因过长超时而失败。  
  
 INCREMENTAL STATS  
 为 ON 时，根据分区统计信息创建统计信息。 为 OFF 时，删除统计信息树并且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 重新计算统计信息。 默认为 OFF。 此设置覆盖数据库级别 INCREMENTAL 属性。  
  
 在将新分区添加到某个大型表时，应更新统计信息以便包括这些新分区。 但是，浏览整个表（FULLSCAN 或 SAMPLE 选项）所需的时间可能会相当长。 此外，因为可能只需针对新分区的统计信息，所以，扫描整个表不是必需的。 该增量选项将在每个分区的基础上创建和存储统计信息，并且在更新时，只刷新需要新统计信息的那些分区上的统计信息  
  
 如果不支持每个分区统计信息，将忽略该选项并生成警告。 对于以下统计信息类型，不支持增量统计信息：  
  
-   使用未与基表的分区对齐的索引创建的统计信息。  
  
-   对 AlwaysOn 可读辅助数据库创建的统计信息。  
  
-   对只读数据库创建的统计信息。  
  
-   对筛选的索引创建的统计信息。  
  
-   对视图创建的统计信息。  
  
-   对内部表创建的统计信息。  
  
-   使用空间索引或 XML 索引创建的统计信息。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
##  <a name="when-to-create-statistics"></a><a name="CreateStatistics"></a>何时创建统计信息  
 查询优化器已通过以下方式创建统计信息：  
  
1.  在创建索引时，查询优化器为表或视图上的索引创建统计信息。 这些统计信息将创建在索引的键列上。 如果索引是一个筛选索引，则查询优化器将在为该筛选索引指定的行的同一子集上创建筛选统计信息。 有关筛选索引的详细信息，请参阅[创建筛选索引](../indexes/create-filtered-indexes.md)和 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)。  
  
2.  在 AUTO_CREATE_STATISTICS 为 ON 时，查询优化器为查询谓词中的单列创建统计信息。  
  
 对于大多数查询，用于创建统计信息的这两个方法就可以确保高质量的查询计划；但在很少的情况下，可以通过使用 [CREATE STATISTICS](/sql/t-sql/statements/create-statistics-transact-sql) 语句创建附加的统计信息来改进查询计划。 这些附加的统计信息可以捕获查询优化器在为索引或单列创建统计信息时并未考虑的统计关联。 您的应用程序可能在表数据中具有附加的统计关联，如果在统计信息对象中计入这些关联，可能会令查询优化器改进查询计划。 例如，针对数据行子集的筛选统计信息或针对查询谓词列的多列统计信息可改进查询计划。  
  
 在使用 CREATE STATISTICS 语句创建统计信息时，我们建议保持 AUTO_CREATE_STATISTICS 选项为 ON，以便查询优化器继续为查询谓词列定期创建单列统计信息。 有关查询谓词的详细信息，请参阅[搜索条件 (Transact-SQL)](/sql/t-sql/queries/search-condition-transact-sql)。  
  
 在以下任何情况适用时，考虑使用 CREATE STATISTICS 语句创建统计信息：  
  
-   [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 优化顾问建议创建统计信息。  
  
-   查询谓词包含尚不位于相同索引中的多个相关列。  
  
-   查询从数据的子集中选择数据。  
  
-   查询缺少统计信息。  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>查询谓词包含多个相关列  
 在某一查询谓词包含具有跨列关系和相关性的多列时，针对多列的统计信息可能会改进查询计划。 针对多列的统计信息包含称作密度的跨列相关统计信息，这些统计信息不可用于单列统计信息。 在查询结果依赖于多列之间的数据关系时，密度可以改进基数估计。  
  
 如果多个列已处于同一索引中，则多列统计信息对象已存在并且不必手动创建它。 如果这些列尚未处于同一索引中，则可以通过对多个列创建索引或通过使用 CREATE STATISTICS 语句，创建多列统计信息。 与统计信息对象相比，它要求更多的系统资源来维护索引。 如果应用程序不要求多列索引，您可以通过创建统计信息对象但不创建索引，有效地利用系统资源。  
  
 在创建多列统计信息时，统计信息对象定义中列的顺序将影响生成基数估计的密度的效率。 统计信息对象在统计信息对象定义中存储键列的每个前缀的密度。 有关密度的详细信息，请参阅 [DBCC SHOW_STATISTICS (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)。  
  
 为了创建用于基数估计的密度，查询谓词中的列必须匹配统计信息对象定义中列的前缀之一。 例如，以下内容在列 `LastName`、 `MiddleName`和 `FirstName`上创建多列统计信息对象。  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 在此示例中，统计信息对象 `LastFirst` 具有以下列前缀的密度：(`LastName`)、(`LastName, MiddleName`) 和 (`LastName, MiddleName, FirstName`)。 密度不可用于 (`LastName, FirstName`)。 如果查询使用 `LastName` 和 `FirstName` ，并且没有使用 `MiddleName`，则密度不可用于基数估计。  
  
### <a name="query-selects-from-a-subset-of-data"></a>查询从数据的子集中选择数据  
 在查询优化器为单个列和索引创建统计信息时，它为所有行中的值创建统计信息。 在查询从行的某一子集中选择数据时，这一行子集具有唯一的数据分布，筛选统计信息可以改进查询计划。 可以通过使用 CREATE STATISTICS 语句并在此语句中用 WHERE 子句定义筛选器谓词表达式来创建筛选统计信息。  
  
 例如，使用 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]时，Production.Product 表中的每种产品属于 Production.ProductCategory 表中的以下四种类别之一：Bikes、Components、Clothing 和 Accessories。 上述每个类别在重量方面的数据分布均不同：自行车的重量范围为 13.77 到 30.0，部件的重量范围为 2.12 到 1050.00 且有些部件的重量为 NULL 值，服装的重量全部为 NULL，附件的重量也为 NULL。  
  
 使用自行车为例，针对所有自行车重量的筛选统计信息将向查询优化器提供更精确的统计信息，并且与全表统计信息或者针对 Weight 列的不存在的统计信息相比，可以改进查询计划质量。 该自行车重量列很适合于筛选统计信息，但如果重量查找的数目相对较少，则不见得适合于筛选索引。 筛选索引所提供的在查找方面的性能提升可能抵不上将筛选索引添加到数据库所导致的额外维护和存储成本。  
  
 以下语句对自行车的所有子类别创建 `BikeWeights` 筛选统计信息。 筛选的谓词表达式通过使用比较 `Production.ProductSubcategoryID IN (1,2,3)`枚举所有自行车子类别，对自行车进行定义。 该谓词无法使用“自行车”类别名称，因为它存储于 Production.ProductCategory 表中，并且筛选表达式中的所有列都必须位于相同的表中。  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../snippets/tsql/SQL14/tsql/statisticsddl/transact-sql/filteredstats.sql#filteredstats2)]  
  
 查询优化器可使用 `BikeWeights` 筛选的统计信息来改进下面这个查询的查询计划，此查询选择重量超过 `25`的所有自行车。  
  
```  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>查询识别缺少的统计信息  
 如果错误或其他事件阻止查询优化器创建统计信息，则查询优化器将不使用统计信息创建查询计划。 查询优化器将统计信息标记为缺失，并且在下次执行查询时尝试重新生成统计信息。  
  
 在使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]以图形方式显示查询的执行计划时，缺少的统计信息将予以警告显示（表名称以红色文本显示）。 另外，使用 **监视** Missing Column Statistics [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 事件类可以指明何时缺少统计信息。 有关详细信息，请参阅 [Errors and Warnings 事件类别（数据库引擎）](../event-classes/errors-and-warnings-event-category-database-engine.md)。  
  
 如果缺少统计信息，则执行以下步骤：  
  
-   确认 AUTO_CREATE_STATISTICS 和 AUTO_UPDATE_STATISTICS 为 ON。  
  
-   请确保数据库不是只读的。 如果数据库是只读的，则查询优化器无法保存统计信息。  
  
-   通过使用 CREATE STATISTICS 语句创建缺少的统计信息。  
  
 当有关只读数据库或只读快照的统计信息丢失或变得陈旧时，[!INCLUDE[ssDE](../../../includes/ssde-md.md)]将创建临时统计信息并在 `tempdb` 中进行维护。 当 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 创建临时统计信息时，将在统计信息名称后追加后缀 _readonly_database_statistic，以便将临时统计信息与永久统计信息加以区分。 后缀 suffix _readonly_database_statistic 是为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]生成的统计信息预留的。 可以在读写数据库上创建和重新生成临时统计信息的脚本。 编写脚本时， [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 将统计信息名称的后缀从 _readonly_database_statistic 更改为 _readonly_database_statistic_scripted。  
  
 只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以创建和更新临时统计信息。 但是，您可以使用用于永久统计信息的相同工具来删除临时统计信息和监视统计信息属性：  
  
-   使用 [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) 语句创建的统计信息。  
  
-   使用 **sys.stats** 和 **sys.stats_columns** 目录视图监视统计信息。 **sys_stats** 包含 **is_temporary** 列，用于指示哪些统计信息是永久的，哪些统计信息是临时的。  
  
 因为临时统计信息存储在 `tempdb` 中，所以，重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务将导致所有临时统计信息消失。  
  
##  <a name="when-to-update-statistics"></a><a name="UpdateStatistics"></a>更新统计信息的时间  
 查询优化器确定统计信息何时可能过期，然后在查询计划需要统计信息时更新它们。 在某些情况下，将 AUTO_UPDATE_STATISTICS 设置为 ON 时，可以通过频繁更新统计信息来优化查询计划，并因此提高查询性能。 可以使用 UPDATE STATISTICS 语句或存储过程 sp_updatestats 来更新统计信息。  
  
 更新统计信息可确保查询使用最新的统计信息进行编译。 不过，更新统计信息会导致查询重新编译。 我们建议不要太频繁地更新统计信息，因为需要在改进查询计划和重新编译查询所用时间之间权衡性能。 具体的折衷方案取决于你的应用程序。  
  
 在使用 UPDATE STATISTICS 或 sp_updatestats 更新统计信息时，我们建议保持将 AUTO_UPDATE_STATISTICS 设置为 ON，以便查询优化器继续定期更新统计信息。 有关如何更新列、索引、表或索引视图的统计信息的详细信息，请参阅 [UPDATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/update-statistics-transact-sql)。 有关如何为数据库中的所有用户定义表和内部表更新统计信息的信息，请参阅存储过程 [sp_updatestats (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)。  
  
 若要确定最近一次更新统计信息的时间，请使用 [STATS_DATE](/sql/t-sql/functions/stats-date-transact-sql) 函数。  
  
 在以下情况下考虑更新统计信息：  
  
-   查询执行时间很长。  
  
-   在升序或降序键列上发生插入操作。  
  
-   在维护操作后。  
  
### <a name="query-execution-times-are-slow"></a>查询执行时间很长  
 如果查询响应时间很长或不可预知，则在执行其他故障排除步骤前，确保查询具有最新的统计信息。  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>在升序或降序键列上发生插入操作  
 与查询优化器执行的统计信息更新相比，升序或降序键列（例如 IDENTITY 或实时时间戳列）上的统计信息可能要求更频繁地更新。 插入操作将新值追加到升序或降序键列上。 添加的行的数目可能过小，以致无法触发统计信息更新。 如果统计信息不是最新的并且查询从最频繁添加的行中选择数据，则当前统计信息将没有这些新值的基数估计。 这可能导致不精确的基数估计和查询性能低下。  
  
 例如，如果统计信息未更新以包括最近销售订单日期的基数估计，则从最近销售订单日期选择的查询将具有不精确的基数估计。  
  
### <a name="after-maintenance-operations"></a>在维护操作后  
 考虑在执行维护过程（例如截断表或对很大百分比的行执行大容量插入）后更新统计信息。 这可以避免在将来查询等待自动统计信息更新时在查询处理中出现延迟。  
  
 索引的重新生成、碎片整理或重新组织之类的操作不会更改数据的分布。 因此，在执行 ALTER INDEX REBUILD、DBCC REINDEX、DBCC INDEXDEFRAG 或 ALTER INDEX REORGANIZE 操作后，您无需更新统计信息。 查询优化器将在您使用 ALTER INDEX REBUILD 或 DBCC DBREINDEX 对表或视图重新生成索引时更新统计信息，但是，此统计信息更新是重新创建索引的副产品。 在 DBCC INDEXDEFRAG 或 ALTER INDEX REORGANIZE 操作后，查询优化器并不更新统计信息。  
  
##  <a name="queries-that-use-statistics-effectively"></a><a name="DesignStatistics"></a>有效使用统计信息的查询  
 某些查询实现（如查询谓词中的局部变量和复杂的表达式）可能导致查询计划不是最佳的。 遵循有关高效使用统计信息的查询设计指导原则可以避免这种情况。 有关查询谓词的详细信息，请参阅[搜索条件 (Transact-SQL)](/sql/t-sql/queries/search-condition-transact-sql)。  
  
 您可以通过应用查询设计指导原则来改进查询计划，这些查询设计指导原则高效地使用统计信息，以便改进在查询谓词中使用的表达式、变量和函数的 *基数估计* 。 在查询优化器不知道表达式、变量或函数的值时，它并不知道在直方图中要查找的值，因此无法从直方图检索最佳的基数估计。 查询优化器而是为直方图中所有取样行，在每个不同值的平均行数的基础上执行基数估计。 这将导致不是最佳的基数估计并且可能影响查询性能。  
  
 下面的指导原则描述如何编写查询以便通过改进基数估计来改进查询计划。  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>改进表达式的基数估计  
 要改进表达式的基数估计，请遵循以下指导原则：  
  
-   只要可能，应简化其中含常量的表达式。 查询优化器在确定基数估计前并不对包含常量的所有函数和表达式进行求值。 例如，简化表达式 ABS(`-100) to 100`。  
  
-   如果表达式使用多个变量，则考虑为表达式创建一个计算列，然后对该计算列创建统计信息或索引。 例如，如果您为表达式 `WHERE PRICE + Tax > 100` 创建计算列，则查询谓词 `Price + Tax`可能会具有更好的基数估计。  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>改进变量和函数的基数估计  
 要改进变量和函数的基数估计，请遵循以下指导原则：  
  
-   如果查询谓词使用局部变量，则考虑重新编写查询以使用参数，而非局部变量。 在查询优化器创建查询执行计划时，局部变量的值未知。 在查询使用某一参数时，查询优化器将基数估计用于传递到存储过程的第一个实际参数值。  
  
-   考虑使用标准表或临时表来保存多语句表值函数的结果。 查询优化器并不为多语句表值函数创建统计信息。 使用此方法，查询优化器可对表列创建统计信息并使用它们创建更好的查询计划。  
  
-   考虑使用标准表或临时表来代替表变量。 查询优化器不会为表变量创建统计信息。 使用此方法，查询优化器可对表列创建统计信息并使用它们创建更好的查询计划。 在确定是使用临时表还是表变量时需要进行一些权衡，与临时表相比，在存储过程中使用的表变量会导致更少的存储过程的重新编译。 根据应用程序，使用临时表来代替表变量可能不会改进性能。  
  
-   如果某一存储过程包含使用某一传入的参数的查询，则在查询中使用该参数值之前，应避免在该存储过程内更改该参数值。 查询的基数估计基于传入的参数值，而非更新的值。 为了避免更改参数值，您可以重新编写查询以使用两个存储过程。  
  
     例如，以下存储过程 `Sales.GetRecentSales` 将在 `@date` 时更改参数 `@date is NULL`的值。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     如果对存储过程 `Sales.GetRecentSales` 的首次调用为 `@date` 参数传递了 NULL，则查询优化器将使用针对 `@date = NULL` 的基数估计编译存储过程，即使查询谓词不是使用 `@date = NULL`调用的。 此基数估计可能与实际查询结果中的行数差别很大。 因此，查询优化器可能会选择非最佳查询计划。 若要避免此情况发生，您可以按如下所示将存储过程重新编写成两个过程：  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>使用查询提示改进基数估计  
 为了改进局部变量的基数估计，您可以将 OPTIMIZE FOR 或 OPTIMIZE FOR UNKNOWN 查询提示与 RECOMPILE 一起使用。 有关详细信息，请参阅[查询提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)。  
  
 对于某些应用程序，每次执行查询时都重新编译查询可能会占用过多时间。 OPTIMIZER FOR 查询提示可对此给予帮助，即使您不使用 RECOMPILE 选项。 例如，您可以将 OPTIMIZER FOR 选项添加到存储过程 Sales.GetRecentSales，以便指定一个特定的日期。 以下示例将 OPTIMIZE FOR 选项添加到 Sales.GetRecentSales 过程。  
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>使用计划指南改进基数估计  
 对于某些应用程序，查询计划指南可能不适用，因为您无法更改查询，或者使用 RECOMPILE 查询提示可能导致过多的重新编译。 您可以使用计划指南来指定 USE PLAN 之类的其他提示，以便在向应用程序供应商调查应用程序变化的同时，控制查询的行为。 有关计划指南的详细信息，请参阅 [Plan Guides](../performance/plan-guides.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)   
 [UPDATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/update-statistics-transact-sql)   
 [sp_updatestats (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)   
 [DBCC SHOW_STATISTICS (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-show-statistics-transact-sql)   
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [DROP STATISTICS (Transact-SQL)](/sql/t-sql/statements/drop-statistics-transact-sql)   
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)   
 [创建筛选索引](../indexes/create-filtered-indexes.md)  
