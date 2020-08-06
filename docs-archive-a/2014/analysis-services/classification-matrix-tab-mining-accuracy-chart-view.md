---
title: "\"分类矩阵\" 选项卡 (挖掘准确性图表视图) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
ms.openlocfilehash: d202d552b25095d0d0845ff64f9c0e289f7bba0e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579267"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>“分类矩阵”选项卡（“挖掘准确性图表”视图）
  "**分类矩阵**" 选项卡为在 "**列映射**" 选项卡上的 "模型" 网格中选择的每个模型显示分类矩阵。仅当在 "**列映射**" 选项卡中选择的可预测列不连续时，分类矩阵才可用。 有关 "**分类矩阵**" 选项卡的详细说明，请参阅[测试和验证 &#40;数据挖掘&#41;](data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="options"></a>选项  
 **复制**  
 将每个分类矩阵的内容复制到剪贴板。  
  
 **\<model>的计数\< predictable column>**  
 显示挖掘结构中每个挖掘模型的分类矩阵。 该矩阵包含以下列：  
  
|值|说明|  
|-----------|-----------------|  
|**预测**|对于可预测列的每一个状态包含一行。|  
|**\<states> (实际) **|可预测列中与每个状态对应的列。 如果行的状态与列的状态相对应，则单元显示数据库中该状态发生的实际次数。 如果行的状态与列的状态不对应，则单元显示预测错误。|  
  
## <a name="see-also"></a>另请参阅  
 [挖掘准确性图表设计器 &#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [测试和验证任务以及操作方法 &#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)  
  
  
