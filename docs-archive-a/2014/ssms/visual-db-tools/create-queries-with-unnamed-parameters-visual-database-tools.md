---
title: 使用未命名参数创建查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0ea53afd1fa4d44390f5805d6b28494428608b90
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577192"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>使用未命名参数创建查询 (Visual Database Tools)
  可通过将问号 (?) 指定为文字值的占位符来使用未命名参数创建查询。 查询和视图设计器将为未命名参数指定临时名称。 可根据需要在查询中指定任意数目的未命名参数。  
  
 在查询和视图设计器中运行查询时，将显示“查询参数”对话框，同时显示临时名称。  
  
### <a name="to-specify-an-unnamed-parameter"></a>指定未命名参数  
  
1.  将要搜索的列或表达式添加到 [“条件”窗格](visual-database-tools.md)中。 如果不希望搜索列或表达式出现在查询输出中，则将其从输出列中移除。  
  
2.  找到包含要搜索的数据列或表达式的行，然后在“筛选器”  网格列中输入一个问号 (?)。  
  
     默认情况下，查询和视图设计器将添加“=”运算符。 不过，您可以对该单元格进行编辑，以替换“>”、“<”或任何其他 SQL 比较运算符。  
  
## <a name="see-also"></a>另请参阅  
 [使用参数进行查询 (Visual Database Tools)](query-with-parameters-visual-database-tools.md)  
  
  
