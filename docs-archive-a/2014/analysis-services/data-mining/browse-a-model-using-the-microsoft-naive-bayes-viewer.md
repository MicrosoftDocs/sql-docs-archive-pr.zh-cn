---
title: 使用 Microsoft Naive Bayes 查看器浏览模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03469e73d82a389426f91d8757630f50fe78fc55
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591683"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>使用 Microsoft Naive Bayes 查看器浏览模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]中的 Naive Bayes 查看器 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 显示通过 Naive Bayes 算法生成的挖掘模型 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 算法是一种非常适合于针对预测性建模任务进行改编的分类算法。 有关此算法的详细信息，请参阅 [Microsoft Naive Bayes Algorithm](microsoft-naive-bayes-algorithm.md)。  
  
 由于 Naive Bayes 模型的主要用途之一是提供一种快速浏览数据集内数据的方法，因此， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 查看器提供了多种方法来显示可预测属性与输入属性之间的交互。  
  
> [!NOTE]  
>  如果您想要查看有关模型中使用的公式以及所发现的模式的详细信息，可切换到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般内容树查看器。 有关详细信息，请参阅[使用 Microsoft 一般内容树查看器浏览模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般内容树查看器（数据挖掘）](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>查看器选项卡  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中浏览挖掘模型时，该模型会显示在其相应查看器的数据挖掘设计器的 **“挖掘模型查看器”** 选项卡上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes 查看器提供了以下用于浏览数据的选项卡：  
  
-   [依赖关系网络](#BKMK_Dependency)  
  
-   [属性配置文件](#BKMK_Profiles)  
  
-   [属性特征](#BKMK_Characteristics)  
  
-   [属性对比](#BKMK_Discrimination)  
  
##  <a name="dependency-network"></a><a name="BKMK_Dependency"></a>依赖关系网络  
 **“依赖关系网络”** 选项卡显示模型中的输入属性与可预测属性之间的依赖关系。 查看器左侧的滑块可起到与依赖关系强度相联系的筛选器的作用。 降低滑块将只显示最强链接。  
  
 选择一个节点后，查看器将突出显示该节点特定的依赖项。 例如，如果选择一个可预测节点，查看器也将突出显示有助于预测该可预测节点的各个节点。  
  
 查看器底部的图例说明了图表中不同颜色代码所代表的依赖关系类型。 例如，如果选择一个可预测节点，该节点将呈青绿色，而预测所选节点的节点呈橙色。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
##  <a name="attribute-profiles"></a><a name="BKMK_Profiles"></a>属性配置文件  
 **“属性配置文件”** 选项卡在网格中显示直方图。 可以使用此网格将在 **“可预测”** 框中选择的可预测属性与模型中的所有其他属性进行比较。 该选项卡中的每一列表示可预测属性的一种状态。 如果可预测属性有很多状态，则可以通过调整 **“直方图条”** 来更改直方图中显示的状态数。 如果选择的数字小于属性的状态总数，则这些状态按支持顺序列出，且剩余状态收集到一个灰色存储桶中。  
  
 若要显示一个将直方图的颜色关联到属性状态的挖掘图例，请单击 **“显示图例”** 复选框。 该挖掘图例还显示所选择的每个属性-值对的事例分布情况。  
  
 若要将网格内容作为 HTML 表复制到剪贴板，请右键单击“属性配置文件”**** 选项卡并选择“复制”****。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
##  <a name="attribute-characteristics"></a><a name="BKMK_Characteristics"></a>属性特征  
 若要使用 **“属性特征”** 选项卡，请从 **“属性”** 列表中选择一个可预测属性，然后从 **“值”** 列表中选择所选属性的状态。 设置这些变量时， **“属性特征”** 选项卡将显示与所选属性的选定事例相关联的属性的状态。 属性按重要性进行排序。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
##  <a name="attribute-discrimination"></a><a name="BKMK_Discrimination"></a>属性对比  
 若要使用 **“属性对比”** 选项卡，请从 **“属性”**、 **“值 1”** 和 **“值 2”** 列表中选择一个可预测属性以及它的两个状态。 然后， **“属性对比”** 选项卡上的网格将在列中显示以下信息：  
  
 **特性**  
 列出数据集内的其他属性，这些属性包含一个高度倾向于可预测属性某个状态的状态。  
  
 **值**  
 显示“属性”**** 列中某属性的值。  
  
 **有利\<value 1>**  
 显示一个彩色条，以指示属性值倾向于“值 1”**** 中显示的可预测属性值的程度。  
  
 **有利\<value 2>**  
 显示一个彩色条，以指示属性值倾向于“值 2”**** 中显示的可预测属性值的程度。  
  
 [返回页首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft Naive Bayes 算法](microsoft-naive-bayes-algorithm.md)   
 [挖掘模型查看器任务和操作指南](mining-model-viewer-tasks-and-how-tos.md)   
 [数据挖掘工具](data-mining-tools.md)   
 [数据挖掘模型查看器](data-mining-model-viewers.md)  
  
  
