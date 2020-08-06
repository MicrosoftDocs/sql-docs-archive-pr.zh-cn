---
title: 挖掘模型查看器 (数据挖掘模型设计器) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.viewers.f1
ms.assetid: 4ba391d5-c97b-4848-ba7c-7d096fa4b7dd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4cc1c9d72a08ef49ed2f4f466953d2ba61394178
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693134"
---
# <a name="mining-model-viewers-data-mining-model-designer"></a>挖掘模型查看器（数据挖掘模型设计器）
  可以使用 **“挖掘模型查看器”** 选项卡浏览挖掘结构包含的挖掘模型。

 首先选择挖掘模型，然后选择查看器。 每个模型始终提供两个查看器：自定义查看器，此查看器可以包括多个选项卡，以及一般查看器。

 有关如何使用各查看器的演练，请参阅 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)。

## <a name="common-options"></a>常用选项
 **刷新查看器内容** 在查看器中重新加载挖掘模型。

 **挖掘模型** 选择一个包含在当前挖掘结构中的挖掘模型以进行查看。 挖掘模型将首先在其关联的自定义查看器中打开。

 **查看器** 选择用于浏览所选挖掘模型的查看器。 此列表包括 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 为每个挖掘模型提供的查看器、 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器以及所有插件查看器。

 下列关系图显示相同模型的自定义查看器和一般查看器。

-   此关系图的上半部分显示基于 Microsoft 时序算法的挖掘模型的查看器。 此特定自定义查看器自动创建时序图形，并提供五个预测。

-   此关系图的下半部分显示使用 **“Microsoft 一般内容树查看器”** 显示的相同模型。 此查看器根据标准化架构显示挖掘模型的内容。 有关详细信息，请参阅 [Microsoft 一般内容树查看器（数据挖掘）](microsoft-generic-content-tree-viewer-data-mining.md)。

 ![挖掘模型设计器概述](media/generic-mining-model-tab1.gif "挖掘模型设计器概述")

## <a name="viewers-and-their-components"></a>各种查看器及其组件
 根据您选择的模型以及用于创建所选数据挖掘模型的算法，您将看到不同的自定义查看器。 每个自定义查看器包含多种工具和对话框，有助于您浏览统计信息和模型中的模式。

 下面的列表介绍各自定义查看器中的选项。

### <a name="microsoft-association-rules-algorithm"></a>Microsoft 关联规则算法

-   [使用 Microsoft 关联规则查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)

    -   [挖掘模型查看器 &#40;项集选项卡&#41;](itemsets-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的 "规则" 选项卡&#41;](rules-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](dependency-network-tab-mining-model-viewer.md)

### <a name="microsoft-clustering-algorithm"></a>Microsoft Clustering Algorithm

-   [使用 Microsoft 分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)

    -   [&#40;挖掘模型查看器的 "分类关系图" 选项卡&#41;](cluster-diagram-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的 "分类配置文件" 选项卡&#41;](cluster-profiles-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "分类特征" 选项卡&#41;](cluster-characteristics-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "分类对比" 选项卡&#41;](cluster-discrimination-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "挖掘图例" 对话框&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-decision-tree-algorithm"></a>Microsoft 决策树算法

-   [使用 Microsoft 树查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)

    -   [挖掘模型查看器 &#40;的决策树选项卡&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "挖掘图例" 对话框&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-linear-regression-algorithm"></a>Microsoft 线性回归算法

-   [使用 Microsoft 神经网络查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [挖掘模型查看器 &#40;的决策树选项卡&#41;](decision-tree-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "挖掘图例" 对话框&#41;](mining-legend-dialog-box-mining-model-viewer.md)

### <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 逻辑回归算法

-   [使用 Microsoft 神经网络查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

### <a name="microsoft-nave-bayes-algorithm"></a>Microsoft Naive Bayes 算法

-   [使用 Microsoft Naive Bayes 查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)

    -   [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;"属性配置文件" 选项卡&#41;](attribute-profiles-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;"属性特征" 选项卡&#41;](attribute-characteristics-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;的属性对比选项卡&#41;](attribute-discrimination-tab-mining-model-viewer.md)

### <a name="microsoft-neural-network-algorithm"></a>Microsoft Neural Network Algorithm

-   [使用 Microsoft 神经网络查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)

    -   [挖掘模型查看器 &#40;的 "依赖关系网络" 选项卡&#41;](dependency-network-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的神经网络&#41;](neural-network-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的 "查找节点" 对话框&#41;](find-node-dialog-box-mining-model-viewer.md)

### <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 顺序分析和聚类分析算法

-   [使用 Microsoft 序列分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)

    -   [&#40;挖掘模型查看器的顺序分析和聚类分析](sequence-clustering-cluster-diagram-tab-mining-model-viewer.md)

    -   [挖掘模型查看器 &#40;顺序分析群集配置文件选项卡](sequence-clustering-cluster-profiles-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的顺序分析群集 "特性" 选项卡&#41;](sequence-clustering-cluster-characteristics-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的顺序分析和聚类分析&#41;](sequence-clustering-cluster-discrimination-tab-mining-model-viewer.md)

    -   [&#40;挖掘模型查看器的顺序分析群集 "转换" 选项卡&#41;](sequence-clustering-cluster-transition-tab-mining-model-viewer.md)

### <a name="microsoft-time-series-algorithm"></a>Microsoft 时序算法

-   [使用 Microsoft 时序查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)

    -   [挖掘模型查看器 &#40;模型选项卡&#41;](model-tab-mining-model-viewers.md)

    -   [挖掘模型查看器 &#40;的图表选项卡&#41;](chart-tab-mining-model-viewers.md)

    -   [&#40;挖掘模型查看器的 "挖掘图例" 对话框&#41;](mining-legend-dialog-box-mining-model-viewer.md)

## <a name="see-also"></a>另请参阅
 [挖掘模型视图 &#40;数据挖掘模型设计器&#41;](mining-models-view-data-mining-model-designer.md) [挖掘结构视图 &#40;数据挖掘模型设计器&#41;](mining-structure-view-data-mining-model-designer.md) [挖掘准确性图表设计器 &#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md) [预测查询生成器 &#40;数据挖掘&#41;](prediction-query-builder-data-mining.md)


