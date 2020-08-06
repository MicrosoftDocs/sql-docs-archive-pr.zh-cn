---
title: 已分类的列 (数据挖掘) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5c264dfb6a97b8b8f576966e8929f6b0dc51e4ed
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589377"
---
# <a name="classified-columns-data-mining"></a>已分类列（数据挖掘）
  定义已分类列时，在挖掘结构中创建当前列和另一个列之间的关系。 指定为已分类列的挖掘结构列中的数据包含描述挖掘结构中另一个列的值的分类信息。  
  
 例如，假定有两个包含数值数据的列：其中 [Yearly Purchases] 列包含特定日历年每个客户每年的总购买量，[Standard Deviations] 列则包含这些值的标准偏差。 在此例中，可以指定 [Yearly Purchases] 列为已分类列，模型将在分析中使用此关系。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中提供的算法不支持使用已分类列，此功能用于创建自定义算法中。  
  
## <a name="defining-a-classified-column"></a>定义已分类列  
 已分类列的数据类型必须为 `Long` 或 `Double`。  
  
 以下列表说明 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持的已分类列内容类型。  
  
 **发生**  
 列内的值是相关值的概率，是介于 0 和 1 之间的数字。  
  
 **变动**  
 列内的值是相关值的方差。  
  
 **STDEV**  
 列内的值是相关值的标准偏差。  
  
 **PROBABILITY_VARIANCE**  
 列内的值是相关值概率的方差。  
  
 **PROBABILITY_STDEV**  
 列内的值是相关值概率的标准偏差。  
  
 **支持**  
 列内的值是相关值的权重或事例复制因子。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 &#40;数据挖掘&#41;](content-types-data-mining.md)   
 [挖掘结构 &#40;Analysis Services 数据挖掘&#41;](mining-structures-analysis-services-data-mining.md)   
 [数据类型（数据挖掘）](data-types-data-mining.md)  
  
  
