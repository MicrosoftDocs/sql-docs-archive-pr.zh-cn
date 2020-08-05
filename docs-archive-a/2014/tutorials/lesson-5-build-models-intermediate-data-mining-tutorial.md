---
title: 第5课：生成神经网络和逻辑回归模型 (中级数据挖掘教程) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- data mining [Analysis Services], tutorials
- neural networks
- tutorials [Data Mining]
- neural network model [Analysis Services]
ms.assetid: 42c3701a-1fd2-44ff-b7de-377345bbbd6b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a8c9fcf0380582f15fa2bf30d6fdeb97bb2ab1fe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581059"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>第 5 课：生成神经网络模型和逻辑回归模型（数据挖掘中级教程）
  
  
 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 业务部门正在开展旨在提高客户对呼叫中心满意度的计划。 他们雇用了一位供应商来管理呼叫中心并报告有关呼叫中心工作效率的指标，同时请您分析该供应商提供的一些初步数据。 他们想知道是否会有任何值得关注的发现。 特别是，他们想知道这些数据是否间接显示了人员配备的任何问题或改进客户满意度的方式。  
  
 该数据集很小，只包括 30 天内呼叫中心的运转情况。 数据跟踪每个班次的操作员新手和有经验操作员的人数、来电数、订单数以及必须解决的问题数、客户等待某人回电话的平均时间。 数据还包含基于“挂断率” ** 的服务质量指标，它反映客户不满意的程度。  
  
 因为您事先对将显示的数据没有任何期望，您决定使用神经网络模型来探查可能的相关性。 神经网络模型通常用于探查，因为该模型能够分析多个输入和输出之间的复杂关系。  
  
## <a name="what-you-will-learn"></a>学习内容  
 在本课中，您将使用神经网络算法生成一个模型，使您和业务团队可以用来理解数据中的趋势。 作为本课的一部分，您将尝试回答下列问题：  
  
-   哪些因素会影响客户满意度？  
  
-   呼叫中心如何能够改进服务质量？  
  
 根据结果，您将生成可用于预测的逻辑回归模型。 业务团队将使用该预测来帮助规划呼叫中心的运营。  
  
 本课程包含以下主题：  
  
-   [为呼叫中心数据添加数据源视图 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [创建神经网络结构和模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [探索呼叫中心模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [向呼叫中心结构中添加逻辑回归模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [&#40;中级数据挖掘教程为呼叫中心模型创建预测&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [为呼叫中心数据添加数据源视图 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>所有课程  
 [第1课：创建中级数据挖掘解决方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [第2课： &#40;中级数据挖掘教程构建预测方案&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [第 3 课：生成市场篮方案（数据挖掘中级教程）](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [第4课：生成顺序分析和聚类分析方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 第 5 课：神经网络和逻辑回归方案（数据挖掘中级教程）  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘基础教程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [中级数据挖掘教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
