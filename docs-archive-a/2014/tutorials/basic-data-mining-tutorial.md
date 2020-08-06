---
title: 数据挖掘基础教程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 6602edb6-d160-43fb-83c8-9df5dddfeb9c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ed557ffb5b8592be4d4375aca40e461d699d6ba7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691405"
---
# <a name="basic-data-mining-tutorial"></a>数据挖掘基础教程
  欢迎使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据挖掘基础教程。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]提供用于创建数据挖掘模型和进行预测的集成环境。 在本教程中，您将完成一个用于目标邮递活动的方案，在此方案中您使用计算机学习来分析和预测客户购买行为。 本教程说明了如何使用三种最重要的数据挖掘算法：聚类、决策树和 Naive Bayes。 您还将学习如何使用挖掘模型查看器分析您的发现，以及如何使用中包含的数据挖掘工具创建预测和准确性图表 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 虚构公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 用于所有的示例。  
  
 当您使用数据挖掘工具时，我们建议您同时完成数据[挖掘的中间教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)。 这些课演示如何使用预测、市场篮分析、时序、关联模型、嵌套表、顺序分析和聚类分析。  
  
## <a name="tutorial-scenario"></a>教程方案  
 在本教程中，您是谁已经 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 过了了解有关公司客户的详细信息的员工，这些人员基于历史购买情况，然后使用该历史数据进行营销。 公司以前从未进行过数据挖掘，因此您必须创建一个专门用于数据挖掘的新数据库并建立几个数据挖掘模型。  
  
## <a name="what-you-will-learn"></a>学习内容  
 本教程将讲述如何创建和使用数种不同类型的计算机学习方法。 您还将学习如何创建挖掘模型的副本以及如何将筛选器应用到输入数据以获得不同结果。 之后，您可以使用提升图比较两个模型的结果。 最后，您将使用钻取功能从基础挖掘结构检索其他数据。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据挖掘包括以下功能，可帮助您轻松地开发和比较多个预测模型，然后对结果采取操作：  
  
-   *维持测试集-* 在创建挖掘结构时，您现在可以将挖掘结构中的数据划分为定型集和测试集。 这让您能够在类似的数据集上测试模型，以及比较相关模型的准确性。  
  
-   *挖掘模型筛选器-* 你现在可以将筛选器附加到挖掘模型，并在定型和测试期间应用筛选器。 这让您能够轻松地在不同的数据子集上生成相关模型。  
  
-   *钻取到结构事例和结构列-* 你现在可以从挖掘模型中的常规模式轻松移到数据源中可操作的详细信息。  
  
 本教程分为以下几课：  
  
 [第1课：准备 Analysis Services 数据库 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/lesson-1-preparing-the-analysis-services-database-basic-data-mining-tutorial.md)  
 在本课程中，您将学习如何创建新的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，添加数据源和数据源视图，以及准备将用于数据挖掘的新数据库。  
  
 [第2课： &#40;基本数据挖掘教程生成目标邮件结构&#41;](../../2014/tutorials/lesson-2-building-a-targeted-mailing-structure-basic-data-mining-tutorial.md)  
 在本课中，您将学习如何创建可用作目标邮寄方案一部分的挖掘模型结构。  
  
 [第 3 课：添加和处理模型](../../2014/tutorials/lesson-3-adding-and-processing-models.md)  
 在本课中，您将学习如何向结构中添加模型。 您创建的模型是用如下算法生成的：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 决策树  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] 聚类分析  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes  
  
 [第4课：浏览目标邮件模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/lesson-4-exploring-the-targeted-mailing-models-basic-data-mining-tutorial.md)  
 在本课中，您将学习如何使用查看器浏览和解释在每个模型中发现的内容。  
  
 [第5课：测试模型 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
 在本课中，您将创建某个 Targeted Mailing 模型的副本，添加一个挖掘模型筛选器以将定型数据限制在特定客户集，然后评估该模型的可行性。  
  
 [第 6 课：创建和使用预测（数据挖掘基础教程）](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
 在本数据挖掘基础教程的最后一课中，您将使用该模型预测哪些客户最有可能购买自行车。 随后，您将钻取到基础事例以获取联系信息。  
  
## <a name="requirements"></a>要求  
 请确保已安装下列软件：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在多维模式下  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据库。  
  
 为了增强安全性，示例数据库不随 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 一起安装。 若要安装的正式数据库 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，请访问[Microsoft SQL 示例数据库](https://go.microsoft.com/fwlink/?LinkId=88417)页，并选择 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 。  
  
> [!NOTE]  
>  当您完成教程时，您可能会发现，如果您向文档查看器工具栏添加了 "**下一主题**" 和 "**上一个主题**" 按钮，在各个步骤间来回移动会更容易。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘解决方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)   
 [挖掘模型任务和操作指南](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [使用 DMX 创建和查询数据挖掘模型：教程（Analysis Services - 数据挖掘）](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)  
  
  
