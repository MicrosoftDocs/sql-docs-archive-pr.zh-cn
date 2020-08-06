---
title: 创建表别名 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8f9e6269fe6e24e8d98922094e799fbf4b5af584
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587690"
---
# <a name="create-table-aliases-visual-database-tools"></a>创建表别名 (Visual Database Tools)
  别名可使表名的使用更为方便。 在以下情况下，使用别名很有帮助：  
  
-   希望使 [SQL](visual-database-tools.md) 窗格中的语句更简短、更容易阅读。  
  
-   经常在查询中引用表名（如在限定列名时），并希望确保查询不超过特定的字符长度限制。 （一些数据库对查询进行了最大长度限制。）  
  
-   使用同一个表的多个实例（如在自联接中），并需要一种引用其中的一个实例或其他实例的方法。  
  
 例如，可以为表名 `"e"` _ `employee`创建别名`information`，然后在查询的其余部分使用 `"e"` 引用该表。  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>为表或表值对象创建别名  
  
1.  将表或表值对象添加到查询中。  
  
2.  在“关系图”  窗格中，右键单击要为其创建别名的对象，然后从快捷菜单中选择“属性”  。  
  
3.  在“属性”  窗口的“别名”  字段中输入别名。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Database Tools &#40;向查询中添加表&#41;](add-tables-to-queries-visual-database-tools.md)   
 [对查询结果进行排序和分组 &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [&#40;Visual Database Tools&#41;汇总查询结果](summarize-query-results-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
