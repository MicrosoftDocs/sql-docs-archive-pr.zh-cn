---
title: "\"分类对比\" 选项卡 (挖掘模型查看器) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 35435736bcdf1b1962de6babace2def953bbfff0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579883"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>“分类对比”选项卡（挖掘模型查看器）
  可以使用 **“分类对比”** 选项卡，对聚类分析模型中的两个现有分类进行比较。 可以查看属性和值的各种组合在分类中的显示方式。  
  
 **有关详细信息，请参阅 ** [Microsoft 聚类分析算法](data-mining/microsoft-clustering-algorithm.md)和[使用 Microsoft 分类查看器浏览模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>选项  
 **刷新查看器内容**  
 在查看器中重新加载挖掘模型。  
  
 **挖掘模型**  
 从当前挖掘结构的挖掘模型中选择一个挖掘模型。 挖掘模型将在其关联的查看器中打开。  
  
 **查看器**  
 选择用于浏览所选挖掘模型的查看器。 可以对分类模型使用自定义查看器，也可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 挖掘内容查看器。 还可以使用插件查看器（如果有）。  
  
 **分类 1**  
 选择一个分类，以便将其与其他分类进行比较。  
  
 **Cluster 2**  
 从挖掘模型的群集列表中选择第二个群集，与“群集 1”**** 进行比较。 还可以将分类与其补数进行比较，表示模型中的所有事例（选定分类中的事例除外）。  
  
 **和的歧视分数 \<cluster 1>\<cluster 2>**  
 图形中的列提供有关每个属性-值与两个选定分类之间的关系的信息。  
  
|||  
|-|-|  
|**变量**|挖掘模型中的属性。|  
|**值**|在 **“变量”** 中选择的属性的值。|  
|**有利\<cluster 1>**|左侧的条形图表示所选属性-值对代表“群集 1”**** 中的所选群集的概率。 可以将鼠标指针悬停在条形上方来查看以百分比表示的值。 请注意，即使值为零，它也不意味着群集中一定缺少属性值，只是分布在一个群集上具有更好的效果。|  
|**有利\<cluster 2>**|右侧的条形图表示所选属性-值对代表“群集 2”**** 中的所选群集的概率。|  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型查看器 &#40;数据挖掘模型设计器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [数据挖掘模型查看器](data-mining/data-mining-model-viewers.md)  
  
  
