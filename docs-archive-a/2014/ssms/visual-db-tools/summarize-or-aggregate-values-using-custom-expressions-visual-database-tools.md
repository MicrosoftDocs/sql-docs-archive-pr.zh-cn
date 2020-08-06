---
title: 使用自定义表达式汇总或聚合值 (Visual Database Tools) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- custom expressions to aggregate values [SQL Server]
ms.assetid: 34130ac1-0106-4766-b324-acb0b7bb6f6e
author: stevestein
ms.author: sstein
ms.openlocfilehash: b9f03f82842178a68c8a3d04ebc1bd738c0ab0b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691469"
---
# <a name="summarize-or-aggregate-values-using-custom-expressions-visual-database-tools"></a>使用自定义表达式汇总或聚合值 (Visual Database Tools)
  除了使用聚合函数来聚合数据之外，还可以创建自定义表达式来生成聚合值。 可在聚合查询中的任何位置使用自定义表达式来替代聚合函数。  
  
 例如，在 `titles` 表中，您可能希望创建一个查询，不仅显示平均价格，而且还显示打折时的平均价格。  
  
 所包括的表达式不能基于只涉及表中单个行的计算，表达式必须基于聚合值，因为在计算表达式时只有聚合值是可用的。  
  
### <a name="to-specify-a-custom-expression-for-a-summary-value"></a>为汇总值指定自定义表达式  
  
1.  为查询指定组。 有关详细信息，请参阅[对查询结果中的行进行分组 (Visual Database Tools)](visual-database-tools.md)。  
  
2.  移动到“条件”窗格中的空白行，然后在“列”  列中键入表达式。  
  
     [查询和视图设计器](query-and-view-designer-tools-visual-database-tools.md)将自动为表达式分配列别名，以在查询输出中创建有用的列标题。 有关详细信息，请参阅[创建列别名 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)。  
  
3.  在表达式的“分组依据”  列中，选择“表达式”  。  
  
4.  运行查询。  
  
## <a name="see-also"></a>另请参阅  
 [对查询结果进行排序和分组 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [汇总查询结果 (Visual Database Tools)](summarize-query-results-visual-database-tools.md)  
  
  
