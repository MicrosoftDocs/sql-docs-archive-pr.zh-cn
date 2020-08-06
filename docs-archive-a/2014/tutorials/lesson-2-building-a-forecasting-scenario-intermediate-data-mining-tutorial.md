---
title: 第2课：生成预测方案 (中级数据挖掘教程) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time series [Analysis Services]
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 9a988156-c900-4c22-97fa-f6b0c1aea9e2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c81d5846df0a37c2b4182cb92fea86ce6f3417a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577167"
---
# <a name="lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial"></a>第 2 课：生成预测方案（数据挖掘中级教程）
  作为 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]的销售分析人员，您需要对下一年产品的销售量做出预测。 特别是已要求您比较不同区域和产品线的预测值。 此外，您还需要确定不同产品的销售量在一年中的不同时间是否有变化。  
  
 为了找到所需的信息，在本课程中您将按三个区域汇总公司每月的销售数据：欧洲、北美洲和太平洋地区。  
  
 完成本课程中的任务之后，您便能回答下列问题：  
  
-   不同型号自行车的销售量如何随时间变化？  
  
-   这三个区域的销售模式之间是否存在差异？  
  
-   我们能预测销售旺季吗？  
  
 本课程可以分两部分完成：  
  
-   第一部分引入如何创建和使用时序模型的基本知识。  
  
-   第二部分将指导您基于所有区域创建常规时序模型。 您可以将此常规模型用于*交叉预测*。  
  
 若要完成本课中的任务（如下所列），您将使用 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 您在[第1课：创建中级数据挖掘解决方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)中创建的数据源。  
  
> [!WARNING]  
>  对于此版本， [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 示例数据库中的日期已更新。 如果您使用 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]的早期版本，则可以在执行这些步骤后生成模型，但可能会看到不同的结果。  
  
 **创建简单预测模型**  
  
-   [添加数据源视图以便预测 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
-   [创建预测结构和模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中级数据挖掘教程修改预测结构&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
-   [自定义和处理预测模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [了解 &#40;中级数据挖掘教程的预测模型&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
-   [&#40;中级数据挖掘教程创建时序预测&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
 **创建用于交叉预测的常规预测模型**  
  
-   [&#40;中级数据挖掘教程的高级时序预测&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
-   [使用更新的数据 &#40;中级数据挖掘教程的时序预测&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
-   [使用替换数据 &#40;中级数据挖掘教程的时序预测&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
-   [&#40;中级数据挖掘教程比较预测模型的预测&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [添加数据源视图以便预测 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial.md)  
  
 [了解 &#40;中级数据挖掘教程的时序模型的要求&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>所有课程  
 [第1课：创建中级数据挖掘解决方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 第 2 课：预测方案（数据挖掘中级教程）  
  
 [第 3 课：生成市场篮方案（数据挖掘中级教程）](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [第4课：生成顺序分析和聚类分析方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [第 5 课：生成神经网络模型和逻辑回归模型（数据挖掘中级教程）](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中级数据挖掘教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
