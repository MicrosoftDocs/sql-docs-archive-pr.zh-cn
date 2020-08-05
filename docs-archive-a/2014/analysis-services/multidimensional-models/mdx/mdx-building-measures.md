---
title: 在 MDX 中生成度量值 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0347835-4983-4d26-acbb-6c8fae7992bd
author: minewiskan
ms.author: owend
ms.openlocfilehash: ac49d37f11584bfbc5d372241056da39e7dd8c93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580934"
---
# <a name="building-measures-in-mdx"></a>在 MDX 中生成度量值
  在多维表达式 (MDX) 中，度量值是名为 DAX 的表达式，通过计算该表达式来解析它以返回表格模型中的值。 这种泛泛的定义所包括的范围十分惊人。 由于能在 MDX 查询中构造和使用度量值，使得人们能够更有力地驾驭表格数据。  
  
> [!WARNING]  
>  只能在表格模型中定义度量值；如果在多维模式下设置数据库，创建度量值将导致错误。  
  
 若要创建一个度量值，该度量值被定义为 MDX 查询的一部分并且其作用域因此被限制在该查询内，请使用 WITH 关键字。 然后，就可以在 MDX SELECT 语句中使用该度量值。 通过这种方法，更改用 WITH 关键字创建的计算成员时就不会打乱 SELECT 语句。 但是，在 MDX 中您引用度量值的方式不用于在 DAX 表达式中引用它的方式；为了引用度量值，您将它命名为 [度量值] 维度的成员，请参阅以下 MDX 示例：  
  
```  
with measure  'Sales Territory'[Total Sales Amount] = SUM('Internet Sales'[Sales Amount]) + SUM('Reseller Sales'[Sales Amount])  
select measures.[Total Sales Amount] on columns  
     ,NON EMPTY [Date].[Calendar Year].children on rows  
from [Model]  
  
```  
  
 执行时将返回以下数据：  
  
||总销售额||  
|-|------------------------|-|  
|2001|11331808.96||  
|2002|30674773.18||  
|2003|41993729.72||  
|2004|25808962.34||  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MEMBER 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Mdx 函数引用 &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)  
  
  
