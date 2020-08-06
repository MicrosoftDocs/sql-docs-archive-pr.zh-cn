---
title: 指定搜索条件 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: stevestein
ms.author: sstein
ms.openlocfilehash: aa5dab8326de079c385a3a508bc1b01b1ee1247d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586050"
---
# <a name="specify-search-conditions-visual-database-tools"></a>指定搜索条件 (Visual Database Tools)
  通过指定搜索条件可以指定在查询中出现的数据行。 例如，若要查询 `employee` 表，则可以指定仅查找在特定区域工作的雇员。  
  
 搜索添加是使用表达式来指定的。 表达式通常由运算符和搜索值组成。 例如，若要查找特定销售区域的雇员，可以为 `region` 列指定以下搜索条件：  
  
```  
='UK'  
```  
  
> [!NOTE]  
>  如果处理多个表，则查询和视图设计器将检查每个搜索条件以确定正在进行的比较是否将导致联接。 如果将导致联接，则查询和视图设计器会自动将搜索条件转换为联接。 有关详细信息，请参阅[自动联接表 (Visual Database Tools)](visual-database-tools.md)。  
  
### <a name="to-specify-search-conditions"></a>指定搜索条件  
  
1.  如果尚未指定搜索条件，请将要在搜索条件内使用的列或表达式添加到“条件”窗格中。  
  
     如果创建选择查询，并且不希望在查询输出中显示搜索列或表达式，请清除每个搜索列或表达式的“输出”  列，以将其从输出列中删除。  
  
2.  找到包含要搜索的数据列或表达式的行，然后在“筛选器”  列中输入搜索条件。  
  
    > [!NOTE]  
    >  如果不输入运算符，则查询和视图设计器将自动插入相等运算符“=”。  
  
 查询和视图设计器通过添加或修改 WHERE 子句来更新 [SQL 窗格](sql-pane-visual-database-tools.md) 中的 SQL 语句。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Visual Database Tools&#41;中输入搜索值的规则](rules-for-entering-search-values-visual-database-tools.md)   
 [指定搜索条件 (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
