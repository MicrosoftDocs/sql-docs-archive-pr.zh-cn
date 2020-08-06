---
title: 索引 DDL 操作的磁盘空间要求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- index disk space [SQL Server]
- space [SQL Server], indexes
- indexes [SQL Server], disk space requirements
- temporary disk space [SQL Server]
ms.assetid: 35930826-c870-44c1-a966-a6a4638f62ef
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ac25fc1555d6b6cfd8ee97b50d261cf5788f587
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590806"
---
# <a name="disk-space-requirements-for-index-ddl-operations"></a>Disk Space Requirements for Index DDL Operations
  磁盘空间是创建、重新生成或删除索引时所需考虑的重要因素。 磁盘空间不足会降低性能，甚至导致索引操作失败。 本主题提供了有助于确定索引数据定义语言 (DDL) 操作所需的磁盘空间量的一般信息。  
  
## <a name="index-operations-that-require-no-additional-disk-space"></a>不需要额外的磁盘空间的索引操作  
 以下索引操作不需要额外的磁盘空间：  
  
-   ALTER INDEX REORGANIZE（但是需要日志空间）。  
  
-   DROP INDEX（当删除非聚集索引时）。  
  
-   DROP INDEX（当删除脱机聚集索引而没有指定 MOVE TO 子句并且不存在非聚集索引时）。  
  
-   CREATE TABLE（PRIMARY KEY 或 UNIQUE 约束）  
  
## <a name="index-operations-that-require-additional-disk-space"></a>需要额外的磁盘空间的索引操作  
 其他所有 DDL 操作都需要在操作期间使用额外的临时磁盘空间，并需要永久磁盘空间来存储新的索引结构。  
  
 创建新的索引结构后，旧（源）结构和新（目标）结构在其相应的文件或文件组中都需要一定的磁盘空间。 旧的结构只有在提交索引创建事务后才会释放。  
  
 以下索引 DDL 操作将创建新的索引结构并需要额外的磁盘空间：  
  
-   CREATE INDEX  
  
-   CREATE INDEX WITH DROP_EXISTING  
  
-   ALTER INDEX REBUILD  
  
-   ALTER TABLE ADD CONSTRAINT（PRIMARY KEY 或 UNIQUE 约束）  
  
-   ALTER TABLE DROP CONSTRAINT（PRIMARY KEY 或 UNIQUE）（当约束基于聚集索引时）  
  
-   DROP INDEX MOVE TO（仅适用于聚集索引。）  
  
## <a name="temporary-disk-space-for-sorting"></a>进行排序所需的临时磁盘空间  
 除了源结构和目标结构所需的磁盘空间以外，还需要一定的临时磁盘空间以进行排序，除非查询优化器找到了不需要进行排序的执行计划。  
  
 如果需要进行排序，则每次创建一个新索引时都要进行排序。 例如，在单个语句中重新生成聚集索引和相关联的非聚集索引时，将逐个对索引进行排序。 因此，进行排序所需的额外的临时磁盘空间只需与操作中最大的索引一样大。 这个最大索引几乎总是聚集索引。  
  
 如果将 SORT_IN_TEMPDB 选项设置为 ON，则最大索引必须可由 **tempdb**容纳。 虽然此选项会增加用于创建索引的临时磁盘空间量，但是如果 **tempdb** 与用户数据库位于不同的磁盘集上时，此选项可减少创建索引所需的时间。  
  
 如果 SORT_IN_TEMPDB 设置为 OFF（默认值），则每个索引（包括已分区索引）都将在其目标磁盘空间中进行排序；只有新的索引结构需要占用磁盘空间。  
  
 有关计算磁盘空间的示例，请参阅 [Index Disk Space Example](index-disk-space-example.md)。  
  
## <a name="temporary-disk-space-for-online-index-operations"></a>联机索引操作所需的临时磁盘空间  
 执行联机索引操作时，需要额外的临时磁盘空间。  
  
 如果联机创建、重新生成或删除了聚集索引，将创建临时非聚集索引以便把旧书签映射到新书签。 如果将 SORT_IN_TEMPDB 选项设置为 ON，则将在 **tempdb**中创建此临时索引。 如果 SORT_IN_TEMPDB 设置为 OFF，将使用与目标索引相同的文件组或分区方案。 临时映射索引针对表中的每行包含一个记录，其内容为新旧书签列，其中包括 uniqueifier 和记录标识符，并且仅包括两种书签中使用的任何列的单个副本。 有关联机索引操作的详细信息，请参阅 [联机执行索引操作](perform-index-operations-online.md)。  
  
> [!NOTE]  
>  不能为 DROP INDEX 语句设置 SORT_IN_TEMPDB 选项。 临时映射索引始终与目标索引创建在同一文件组或分区方案中。  
  
 联机索引操作使用行版本控制来使索引操作不受其他事务所做的修改的影响。 这就不需要对已经读取的行请求共享锁。 在联机索引操作期间，并发的用户更新和删除操作需要一定的空间以用于 **tempdb**中的版本记录。 有关详细信息，请参阅 [联机索引操作](perform-index-operations-online.md) 。  
  
## <a name="related-tasks"></a>Related Tasks  
 [索引磁盘空间示例](index-disk-space-example.md)  
  
 [索引操作的事务日志磁盘空间](transaction-log-disk-space-for-index-operations.md)  
  
 [估计表的大小](../databases/estimate-the-size-of-a-table.md)  
  
 [估计聚集索引的大小](../databases/estimate-the-size-of-a-clustered-index.md)  
  
 [估计非聚集索引的大小](../databases/estimate-the-size-of-a-nonclustered-index.md)  
  
 [估计堆的大小](../databases/estimate-the-size-of-a-heap.md)  
  
## <a name="related-content"></a>相关内容  
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)  
  
 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [为索引指定填充因子](specify-fill-factor-for-an-index.md)  
  
 [重新组织和重新生成索引](indexes.md)  
  
  
