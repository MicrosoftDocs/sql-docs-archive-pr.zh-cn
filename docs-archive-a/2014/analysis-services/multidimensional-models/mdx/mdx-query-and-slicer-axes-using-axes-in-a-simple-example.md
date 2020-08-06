---
title: 在简单示例中使用查询轴和切片器轴 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- query axis [MDX]
ms.assetid: 85bcb26f-5971-4153-b334-61f8d8b475b5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 324f082fd6659592e56af65680bd4aa623c625d9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588726"
---
# <a name="using-query-and-slicer-axes-in-a-simple-example-mdx"></a>在简单示例中使用查询轴和切片器轴 (MDX)
  本主题中提供的简单示例说明了指定和使用查询轴和切片器轴的基本操作。  
  
## <a name="the-cube"></a>多维数据集  
 名为 TestCube 的多维数据集有两个维度，分别为 Route 和 Time。 每个维度都只有一个用户层次结构，分别为 Route 和 Time。 因为多维数据集的度量值是 Measures 维度的一部分，所以此多维数据集总共有三个维度。  
  
## <a name="the-query"></a>查询  
 查询要提供一个矩阵，可以在该矩阵内跨路线和时间比较 Packages 度量值。  
  
 在下面的 MDX 查询示例中，Route 和 Time 层次结构为查询轴，Measures 维度为切片器轴。 [Members](/sql/mdx/members-set-mdx) 函数指明 MDX 将使用层次结构或级别的成员来构造一个集。 使用 `Members` 函数意味着不必在 MDX 查询中显式声明特定层次结构或级别的每个成员。  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>结果  
 结果是一个网格，标识 COLUMNS 和 ROWS 轴维度的每个交点处 Packages 度量值的值。 下表显示了此网格。  
  
||air|sea|  
|-|---------|---------|  
|第一季度|60|50|  
|第二季度|45|45|  
  
## <a name="see-also"></a>另请参阅  
 [&#40;MDX&#41;指定查询轴的内容](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [指定切片器轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
