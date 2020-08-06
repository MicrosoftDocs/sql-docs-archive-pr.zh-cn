---
title: 浏览顺序分析和聚类分析模型 (中级数据挖掘教程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bac603d2480ec1f344d14351757027de749f8c86
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691392"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>浏览顺序分析和聚类分析模型（数据挖掘中级教程）
  现在您已**使用区域**模型构建了序列群集，可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 数据挖掘设计器的 "**挖掘模型查看**器" 选项卡中的 "序列聚类分析" 查看器对其进行浏览。 [!INCLUDE[msCoName](../includes/msconame-md.md)]序列分类查看器包含五个选项卡：**群集图**、**群集配置文件**、**群集特征**、 **ClusterDiscrimination**和**状态转换**。 有关如何使用此查看器的详细信息，请参阅[使用 Microsoft 序列分类查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
-   [分类关系图选项卡](#bkmk_CDiagram)  
  
-   [群集配置文件选项卡](#bkmk_CProfiles)  
  
-   [分类特征选项卡](#bkmk_CChars)  
  
-   [分类对比选项卡](#bkmk_CDiscrim2)  
  
-   [“状态转换”选项卡](#bkmk_StateTran)  
  
-   [“一般内容”视图](#bkmk_Generic)  
  
##  <a name="cluster-diagram-tab"></a><a name="bkmk_CDiagram"></a>分类关系图选项卡  
 "**分类关系图**" 选项卡以图形方式显示算法在数据库中发现的分类。 关系图中的布局表示分类之间的关系，其中相似的分类分组在一起。 默认情况下，每个节点的明暗度表示分类中所有事例的密度，即节点越暗，它所包含的事例越多。 可以更改节点明暗度代表的含义，使其表示对每个分类内的属性或状态的支持。  
  
 也可以重命名分类，使其更加易于识别并与目标分类结合使用。 在本教程中，您将重命名太平洋地区客户百分比最高的分类，以及事例总数量最多的分类。  
  
> [!NOTE]  
>  在重新处理模型时，分配给特定分类的事例可能会发生更改，具体取决于数据和模型参数。 此外，如果对分类进行了重命名，则在重新处理挖掘模型时，这些名称将会丢失。  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>更改用于突出显示分类的属性  
  
1.  在 "**明暗度变量**" 列表中，选择 "**模型**"。  
  
2.  在 "**状态**" 列表中选择 "**循环 Cap** "。  
  
     该图会进行更新，以显示所选产品在每个分类中的集中度。 最暗的分类包含自行车帽的密度最大。 您可以将明暗度变量更改为使用任何输入列的任何状态。  
  
3.  在 "**明暗度变量**" 列表中，选择 "**填充**"。  
  
     将明暗度变量更改为客户群体时，该图将进行更新，按大小比较分类。 最暗的分类所包含的事例多于其他分类。  
  
#### <a name="to-rename-nodes-in-the-model"></a>重命名模型中的节点  
  
1.  将**明暗度变量**更改为 `Region` ，并将**状态**设置为 "**太平洋**"。  
  
2.  突出显示图形中最暗的节点。  
  
3.  右键单击此群集，然后选择 "**重命名群集"。**  
  
4.  键入 "**太平洋群集**名称"。  
  
5.  将 "明暗度**变量**" 的值更改为 "**总体**"。  
  
6.  在已更新的图形中，找到最暗的分类（应该是最大的分类）。 如果无法通过明暗度来判断哪个分类是最大的，请将鼠标悬停在每个分类上并查看工具提示，然后选择包含事例最多的分类。  
  
7.  右键单击此群集，然后选择 "**重命名群集**"。 键入新名称 `Largest Cluster` 。  
  
 可从表示该分类的节点进行钻取，以查看每个分类中事例的详细信息。 如果要对分析结果进行操作（例如发送电子邮件给客户），则此功能非常有用。 还可以浏览包括在结构中但未在模型中使用的其他一些事例属性，例如 Region 和 IncomeGroup。 有关从挖掘模型钻取到基础事例的详细信息，请参阅[钻取查询 &#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>从分类关系图钻取到详细信息  
  
1.  右键单击 `Pacific Cluster` ，选择 "**钻取**"，然后选择 "**模型和结构列**"。  
  
     "**钻取**" 对话框将打开。 未在模型中使用但可用于查询的列的前缀为 "**结构**"。  
  
     可以看到此分类包括的大多数客户都来自太平洋地区，只有少量客户来自其他地区。  
  
2.  单击嵌套列 v Assoc Seq Line Items 中的加号，可以查看特定客户订单中项的顺序。  
  
3.  关闭 "**钻取**" 对话框。  
  
    > [!NOTE]  
    >  利用 "**播放**" 按钮，您可以重新查询数据;但是，如果模型已由其他进程在后台动态更新，则重新查询不会更改显示的数据。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="cluster-profiles-tab"></a><a name="bkmk_CProfiles"></a>群集配置文件选项卡  
 "**分类配置文件**" 选项卡显示每个群集中的序列。 群集列在 "**状态**" 列右侧的各个列中。  
  
 在查看器中，"**模型**" 行描述了群集中各项的总体分布，而 "**模型**" 行包含各项的序列。 模型每个单元格中的颜色序列的每一行 **。 samples**行表示群集中随机选择的用户的行为。  
  
 单个序列直方图中的每一种颜色都代表一个产品型号。 挖掘图例使用颜色编码和产品型号名称来显示产品序列。 如果您已经将其他列添加到聚类分析模型中，例如 Region 或 Income Group，则查看器将包含每个列的附加行，显示这些值在每个分类中的分布。  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>查看分类中最常见的顺序  
  
1.  右键单击群集列中的 "**模型**" 行 `Largest Cluster` ，然后选择 "**显示图例**"。  
  
     **Color**列包含一个阴影条，用于指示在序列中找到的项的频率。 每个项以一种不同颜色表示。 "**含义**" 列列出每种颜色的产品型号名称。 "**分布**" 列告诉您序列中包含此项的事例的百分比。  
  
2.  关闭 "**挖掘图例**"。  
  
3.  右键单击包含 "标题" 和 "**填充**" 的列中的 "**示例**" 行，然后选择 "**显示图例**"。  
  
4.  扫描整个模型中的序列列表`.`  
  
     挖掘图例会首先列出最常见的序列，因此您可以看到 Mountain Tire Tube 是很多序列中的第一项。 这意味着客户很有可能首先将 Mountain Tire Tube 放入购物篮中。  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>从分类查看器钻取到事例  
  
1.  在 "属性" 窗格中向下滚动，直到找到属性所在的行 `Region` 。  
  
     该行包含模型中每个分类的直方图，以及一个用于**填充**的附加柱状图，即模型中使用的整个事例集。 直方图是一个带有不同颜色的条，每种颜色代表一个属性，该属性的彩色部分的大小代表了具有该属性的事例的百分比。  
  
2.  比较您重命名的分类和的直方图 `Pacific Cluster` `Largest Cluster` 。 每个分类显示在不同的列中。  
  
     这些颜色看起来都像是纯色，但却是不同的。  
  
3.  在行中，将鼠标悬停在的 `Region` 彩色直方图上 `Largest Cluster` 。  
  
     工具提示将显示一些值，这些值显示了来自每个区域的事例所占的实际百分比。  
  
4.  右键单击行中的彩色直方图 `Region` `Pacific Cluster` ，选择 "**钻取**"，然后选择 "**仅限模型列**"。  
  
5.  移动滚动条可以查看此分类中的所有客户。  
  
     通过再次钻取到详细信息，可以看到此分类包括的大多数订单都来自太平洋地区，但也有一些订单来自北美和欧洲地区。  
  
6.  关闭 "**钻取**" 对话框。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="cluster-characteristics-tab"></a><a name="bkmk_CChars"></a>分类特征选项卡  
 "**分类特征**" 选项卡通过显示直观地表示所选分类的属性值重要性的栏来汇总群集中各状态之间的转换。 "**变量**" 列告诉您哪个模型对于所选的分类或总体非常重要：特定值或值之间的关系（称为*转换*）。 "**值**" 列提供关于值或转换的更多详细信息，"**概率**" 列直观地表示此属性或转换的权重。  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>查看分类的重要属性  
  
1.  在 "**分类**" 下拉列表中，选择 `Pacific Cluster` 。  
  
     列表将更新以显示已重命名的分类的特征 `Pacific Cluster` 。 在此群集中，最重要的特征是 `Region` 。  
  
2.  将鼠标悬停在行中的阴影条上 `Region` 。  
  
     该值为“Pacific”的概率非常高。 有关如何解释这些值的详细信息，请参阅[Microsoft 顺序分析和聚类分析算法技术参考](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)。  
  
3.  仔细查看分类的特征列表，直至找到第一个转换行。  
  
4.  转换行包含**Variables**列中的文本转换，以及**值**列中的顺序属性值的一些组合。 该序列也可以包含起点和缺少值。  
  
     例如，假设过渡具有值 "[Start]-> 公路轮胎管"。 这意味着此分类中的客户通常首先将 Road Tire Tube 放入购物篮中。 这可能表示该产品是客户首先挑选出的受欢迎商品，或者只表示该产品在购物场所容易找到。  
  
5.  滚动列表，直到找到其中没有 **[开始]** 或**缺少**的第一个转换。  
  
     例如，假设您找到了过渡、**旅行轮胎、旅行轮胎管**。 这意味着此分类中的客户通常将这些项一起放入购物篮中，而且是严格按照这个顺序放入。  
  
6.  将鼠标悬停在此转换的阴影条上。  
  
     此转换的概率以百分比显示。  
  
7.  在 "**分类**" 下拉列表中，选择 "**总体 (所有) **"。  
  
     该属性列表会更新为显示用于创建模型的所有订单的特征。 在此挖掘模型中，区分分类的最重要的特征是 `Region` ，值为**北美**。  
  
 在查看这些任务后，您认识到两点。 第一点是您需要大量数据来获取有意义数量的组合。 例如，概率最高的序列可能包含 **[Start]** 或**缺少**状态。  
  
 第二种情况是，对的属性有一个强大的群集效果 `Region` ，这使得更难查看序列组。 因此，您决定创建另一个模型，该模型只使用序列，而且不包括区域或收入的列。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="cluster-discrimination-tab"></a><a name="bkmk_CDiscrim2"></a>分类对比选项卡  
 "**分类对比**" 选项卡可帮助你比较两个分类，以确定哪些属性区分不同的群集。 该选项卡包含四列：**变量**、**值**、**群集 1**和**分类 2**。  你可以选择要用作**群集 1**和**分类 2**的任何群集。  
  
 "**变量**" 列告诉您属性的名称，该名称可以是列名，也可以是列名称和 word**转换**的组合。 "**值**" 列显示属性或转换的确切值。 "**分类 1** " 和 "**分类 2** " 列中的阴影条指示要比较的分类中的属性的强度。 阴影条越长，分类包括具有该属性的事例的可能性越大。  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>使用“分类对比”选项卡比较两个分类  
  
1.  在 "**分类对比**" 选项卡中，为 "**分类 1**" 选择 `Pacific Cluster` 。  
  
     默认情况下，**群集 2**的选择将更改为**太平洋群集的补充**。  
  
     与所有其他情况区分开来的顶级属性 `Pacific Cluster` 是区域。 Region 是聚类分析的一个强属性，以至于它掩盖了其他属性。 为了避免这种效果，请尝试相互比较几个较小的分类。 在进行比较时，属性列表会发生变化，可能包括模型之间的更多转换。  
  
2.  找到转换行，将鼠标悬停在阴影条上。  
  
     "**值**" 列中的项可以包括状态和转换。 各项的明暗度指示对比分数。 若要详细了解不同分数的含义，请参阅[顺序分析和聚类分析模型的挖掘模型内容 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="state-transitions-tab"></a><a name="bkmk_StateTran"></a>"状态转换" 选项卡  
 在 "**状态转换**" 选项卡上，可以选择一个群集并浏览其状态转换。 如果从 "分类" 下拉列表中选择 "**总体" (所有) ** ，则关系图将显示整个挖掘模型的状态分布。  
  
 图中的每个节点都表示一个状态，或您试图分析的序列的可能值。 节点的背景色表示该状态的频率。 一些状态之间用线条连接，指示这些状态之间的转换。 可以上下移动滑块，以更改转换的概率阈值。 数字与某些节点相关联，指示该状态的概率。  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>在“状态转换”选项卡中浏览关系  
  
1.  在挖掘模型查看器的 "**状态转换**" 选项卡中， `Pacific Cluster` 从分类列表中选择。 确保选中 "**显示边缘标签**" 选项。  
  
     该图会更新为显示此分类中最常见的转换。  
  
2.  单击通过线条连接到另一个节点的任何节点。  
  
     该图进行了更新，并且突出显示相关的节点。 线条旁的数值指示转换的概率。  
  
3.  将滑块向上提升到**所有链接**，以增加图形中包含的转换数。  
  
4.  选择 "填充" (**分类**中的**所有) ** 。  
  
     请注意，在加载另一个分类时，该图会重置为默认显示设置，因此滑块控件也会重置到中间位置。  
  
5.  单击关系图中最暗的节点，应为 "**运动-100**"。  
  
     请注意，产品之间没有线条相互连接。  
  
6.  将滑块向上提升一级，以增加图中包括的转换的数量。 目前尚无所有**链接**。  
  
     该图会添加更多的转换，从而进行更新，但这些转换都没有包括 Sport-100 型号。  
  
7.  将滑块控件一直移动到**所有链接**。 如果尚未选择 Sport-100 节点，请单击该节点。  
  
     该图会更新为显示包括 Sport-100 产品的很多转换。 连接线条的箭头的方向指示 Sport-100 项是作为配对中的第一项还是第二项选择的。  
  
8.  单击 Touring Tire 的节点，将滑块控件向下移回至中间位置。  
  
     首先，有许多将旅行轮胎连接到其他产品的转换线路，但当您提高概率阈值时，从图形中消除的转换可能性越小，只留下过渡，旅行轮胎 > 旅行轮胎管。 此转换的含义是如果客户将 Touring Tire 放入购物篮，则该客户接下来将 Touring Tire Tube 也放入购物篮的概率非常高。  
  
 [返回页首](#bkmk_CDiagram)  
  
##  <a name="generic-content-tree-viewer"></a><a name="bkmk_Generic"></a>一般内容树查看器  
 此查看器可用于所有模型，无论算法和模型类型为何均为如此。 "**查看器**" 下拉列表中提供了**MicrosoftGeneric 内容树查看器**。  
  
 内容树是任何挖掘模型的表示形式，由一系列节点组成，其中每个节点都表示关于定型数据的已了解的知识。 节点可以包含一种模式、一组规则、一个分类或共享某些属性的日期范围的定义。 根据算法和可预测属性的不同，节点的具体内容会有所不同，但内容的通用表示形式是相同的。  
  
 您可以展开每个节点以查看详细信息的递增级别，并可以将任何节点的内容复制到剪贴板。 有关详细信息，请参阅 [使用 Microsoft 一般内容树查看器浏览模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>使用一般内容树查看器查看顺序分析和聚类分析模型的详细信息  
  
1.  在 "**挖掘模型查看器**" 选项卡中，单击 "**查看器**" 列表，然后选择 " **Microsoft 一般内容树查看器**"。  
  
2.  在 "**节点标题**" 窗格中，单击 "" `Pacific Cluster (1)` 。  
  
     此节点的名称同时包含为分类指定的友好名称和基础节点 ID。 可以使用节点 ID 来深化到模型中的其他详细信息。  
  
3.  展开 "分类 1" 的第一个子节点，名为 "**序列级别**"。  
  
     分类的序列级别节点包含了关于该分类中的状态和转换的详细信息。 可以使用 NODE_DISTRIBUTION 列中的这些详细信息，浏览每个节点或模型的序列和状态。  
  
4.  继续展开节点并在 HTML 查看器窗格中查看详细信息。  
  
 有关挖掘模型内容以及如何使用查看器中的详细信息的详细信息，请参阅[顺序分析和聚类分析模型的挖掘模型内容 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [返回页首](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [&#40;中级数据挖掘教程创建相关的顺序分析和聚类分析模型&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 顺序分析和聚类分析算法](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [顺序分析和聚类分析模型查询示例](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
