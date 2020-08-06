---
title: 描述的聚集索引和非聚集索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- query optimizer [SQL Server], index usage
- index concepts [SQL Server]
ms.assetid: b7d6b323-728d-4763-a987-92e6292f6f7a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c9eb51a24000b8af4a466fe4330644a722ad325b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693322"
---
# <a name="clustered-and-nonclustered-indexes-described"></a>描述的聚集索引和非聚集索引
  索引是与表或视图关联的磁盘上结构，可以加快从表或视图中检索行的速度。 索引包含由表或视图中的一列或多列生成的键。 这些键存储在一个结构（B 树）中，使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以快速有效地查找与键值关联的行。  
  
 表或视图可以包含以下类型的索引：  
  
-   聚集  
  
    -   聚集索引根据数据行的键值在表或视图中排序和存储这些数据行。 索引定义中包含聚集索引列。 每个表只能有一个聚集索引，因为数据行本身只能按一个顺序排序。  
  
    -   只有当表包含聚集索引时，表中的数据行才按排序顺序存储。 如果表具有聚集索引，则该表称为聚集表。 如果表没有聚集索引，则其数据行存储在一个称为堆的无序结构中。  
  
-   非聚集  
  
    -   非聚集索引具有独立于数据行的结构。 非聚集索引包含非聚集索引键值，并且每个键值项都有指向包含该键值的数据行的指针。  
  
    -   从非聚集索引中的索引行指向数据行的指针称为行定位器。 行定位器的结构取决于数据页是存储在堆中还是聚集表中。 对于堆，行定位器是指向行的指针。 对于聚集表，行定位器是聚集索引键。  
  
    -   您可以向非聚集索引的叶级添加非键列以跳过现有的索引键限制（900 字节和 16 键列），并执行完整范围内的索引查询。 有关详细信息，请参阅 [Create Indexes with Included Columns](create-indexes-with-included-columns.md)。  
  
 聚集索引和非聚集索引都可以是唯一的。 这意味着任何两行都不能有相同的索引键值。 另外，索引也可以不是唯一的，即多行可以共享同一键值。 有关详细信息，请参阅 [创建唯一索引](create-unique-indexes.md)。  
  
 每当修改了表数据后，都会自动维护表或视图的索引。  
  
 有关其他类型的特殊用途索引，请参阅 [Indexes](indexes.md) 。  
  
## <a name="indexes-and-constraints"></a>索引和约束  
 对表列定义了 PRIMARY KEY 约束和 UNIQUE 约束时，会自动创建索引。 例如，如果创建了表并将一个特定列标识为主键，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 自动对该列创建 PRIMARY KEY 约束和索引。 有关详细信息，请参阅 [Create Primary Keys](../tables/create-primary-keys.md) 和 [Create Unique Constraints](../tables/create-unique-constraints.md)。  
  
## <a name="how-indexes-are-used-by-the-query-optimizer"></a>查询优化器如何使用索引  
 设计良好的索引可以减少磁盘 I/O 操作，并且消耗的系统资源也较少，从而可以提高查询性能。 对于包含 SELECT、UPDATE、DELETE 或 MERGE 语句的各种查询，索引会很有用。 例如，在 `SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250` 数据库中执行的查询 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 。 执行此查询时，查询优化器评估可用于检索数据的每个方法，然后选择最有效的方法。 可能采用的方法包括扫描表和扫描一个或多个索引（如果有）。  
  
 扫描表时，查询优化器读取表中的所有行，并提取满足查询条件的行。 扫描表会有许多磁盘 I/O 操作，并占用大量资源。 但是，如果查询的结果集是占表中较高百分比的行，扫描表会是最为有效的方法。  
  
 查询优化器使用索引时，搜索索引键列，查找到查询所需行的存储位置，然后从该位置提取匹配行。 通常，搜索索引比搜索表要快很多，因为索引与表不同，一般每行包含的列非常少，且行遵循排序顺序。  
  
 查询优化器在执行查询时通常会选择最有效的方法。 但如果没有索引，则查询优化器必须扫描表。 您的任务是设计并创建最适合您的环境的索引，以便查询优化器可以从多个有效的索引中选择。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供[数据库引擎优化顾问](../performance/database-engine-tuning-advisor.md)来帮助分析数据库环境以及选择适当的索引。  
  
## <a name="related-tasks"></a>Related Tasks  
 [创建聚集索引](create-clustered-indexes.md)  
  
 [创建非聚集索引](create-nonclustered-indexes.md)  
  
  
