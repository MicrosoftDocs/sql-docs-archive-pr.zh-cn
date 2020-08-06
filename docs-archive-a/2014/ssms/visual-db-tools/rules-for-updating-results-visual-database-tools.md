---
title: 用于更新结果的规则 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5cc6befc6571f29be95b176f8de6d7dcfaed9108
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691008"
---
# <a name="rules-for-updating-results-visual-database-tools"></a>更新结果的规则 (Visual Database Tools)
  在许多情况下，都可以更新显示在 [“结果”窗格](visual-database-tools.md)中的结果集。 不过，在某些情况下却不能这样做。  
  
 一般而言，若要更新结果， [查询和视图设计器](query-and-view-designer-tools-visual-database-tools.md) 必须具备足够的信息来唯一标识表中的行。 例如，查询在输出列表中包括主键。 此外，您还必须有足够的权限才能更新数据库。  
  
 如果查询是基于视图的，您也许可以对视图进行更新。 同样的原则不仅仅适用于视图本身，除非这些原则适用于视图中的基础表。  
  
> [!NOTE]  
>  查询和视图设计器无法事先确定您是否可更新基于某一视图的结果集。 因此，尽管您可能无法更新所有的视图，但查询设计器仍会把它们全部显示出来。  
  
 下表汇总了一些特定实例，在这些例子中您也许可以更新“结果”窗格中的查询结果，也许不能。 在许多情况下，所使用的数据库决定了您是否可以更新查询结果。  
  
|查询|结果是否可更新|  
|-----------|-----------------------------|  
|基于表并且输出列表中包含主键的查询|是（但下面列出的除外）。|  
|基于无唯一索引和主键的表的查询|取决于查询和数据库。 有些数据库在有足够的信息用于唯一地标识记录时才允许进行更新。|  
|基于未联接在一起的多个表的查询|不是。|  
|基于数据库中标记为只读数据的查询|不是。|  
|基于包含一个无约束表的视图的查询|是（但下面列出的除外）。|  
|基于用一对一关系联接的表的查询|是（但下面列出的除外）。|  
|基于用一对多关系联接的表的查询|通常是。|  
|基于有多对多关系的表（不少于三个）的查询|不是。|  
|基于未授予其更新权限的表的查询|可删除但不可更新。|  
|基于未授予其删除权限的表的查询|可更新但不可删除。|  
|聚合查询|不是。|  
|基于包含总计或聚合函数的子查询的查询|不是。|  
|包括 DISTINCT 关键字（用于排除重复的行）的查询|不是。|  
|FROM 子句包括用户定义函数的查询（查询返回一个表且用户定义函数包含多个 Select 语句）|不是。|  
|FROM 子句中包括内联用户定义函数的查询|是的。|  
  
 此外，您也许不能在查询结果中更新特定的列。 下面的列表汇总了不能在“结果”窗格中更新的特定类型的列。  
  
-   基于表达式的列  
  
-   基于用户定义的标量函数的列  
  
-   已由其他用户删除的行或列  
  
-   其他用户锁定的行或列（通常，锁定的行在解锁后就可更新）  
  
-   时间戳列或 BLOB 列  
  
## <a name="see-also"></a>另请参阅  
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
