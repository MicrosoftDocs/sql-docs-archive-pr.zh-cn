---
title: 分析) Excel (表分析工具的关键影响因素 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
author: minewiskan
ms.author: owend
ms.openlocfilehash: f60eb5144059b0976d52eec2329f27553132146c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579377"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>分析关键影响因素（Excel 表分析工具）
  ![功能区中的“分析关键影响因素”按钮](media/tat-aki.gif "功能区中的“分析关键影响因素”按钮")  
  
 使用 "**分析关键影响因素**" 工具，可以选择包含目标结果的列，而算法将确定哪些因素对结果的影响最强。  
  
 该工具可创建若干新数据表，这些表将报告与每个结果相关联的因素，并以图形方式显示它们之间存在关系的概率。 可以基于不同因素和结果对这些表进行筛选，以更深入地研究结果。  
  
 还可选择可能得到的一对结果并对它们进行比较。 例如，您可以比较不同的使用者组来确定可能影响决策的因素。  
  
## <a name="using-the-analyze-key-influencers-tool"></a>使用“分析关键影响因素”工具  
  
1.  打开 Excel 数据表。  
  
2.  在 "**表工具**" 中的 "**分析**" 功能区上，单击 "**分析关键影响因素"。**  
  
3.  选择单个列作为分析目标。  
  
4.  （可选）单击 "**选择要用于分析的列**"。 在 "**高级列选择**" 对话框中，选择最有可能包含相关数据的列。 若要改进性能和精确性，请取消选择诸如 ID 或名称等对模式分析不重要的列。 单击 **"确定"** 关闭 "**高级列选择**" 对话框。  
  
5.  单击 **“运行”** 。  
  
     "**分析关键影响因素**" 工具可对数据进行分析，以确定最佳设置，并自动设置所有参数。  
  
6.  如果未检测到模式，该向导会创建一个新工作表，该表含有对问题的说明。  
  
7.  如果检测到模式，则向导将在新的工作表中创建一个报表以显示这些模式。 报表为**的 \<column> 关键影响因素**。 可以按照以下步骤所述自定义该报表。  
  
#### <a name="create-a-custom-report"></a>创建自定义报表  
  
1.  在 "**基于关键影响因素的对比**" 对话框中，从 "**值 1** " 和 "**值 2** " 下拉列表中选择要进行比较的两个值。 例如，您可以将购买者与非购买者进行比较。  
  
2.  单击 "**添加报表**"。  
  
     该向导将创建新工作表，并为每对关键因素比较添加一个表。  
  
3.  完成比较后，请单击 "**关闭**"。  
  
## <a name="understanding-the-key-influencers-report"></a>了解关键影响因素报表  
 创建数据模型后，"**分析关键影响因素**" 工具会创建帮助您探索和比较关键影响因素的报表。  
  
-   左侧的报表是默认情况下生成的一个报表。 其中显示对于结果列（因变量）影响最大的预测因子。  
  
-   右侧的报表是可选报表，可通过比较两个特定的结果值创建该报表。 此报表将比较购买者与非购买者。  
  
-   注意，对于所创建的每个报表都会添加一个新的工作表。 在创建表后，可移动这些表；我们将这些表并行放在一起进行比较。  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **相对影响**  
 第一个报表中的阴影条指示此属性与结果的关联强度。  
  
 色条长度指示该因素影响结果的概率；因此，阴影条越长，关联性越强。  
  
 **倾向于**  
 第二个报表中，在两列中列出所比较的目标值，其中按置信度降序列出相关因素。  
  
-   **蓝**条显示了导致结果的属性 "No" (= 未) 购买。  
  
-   **红色**条显示了导致结果的属性 "是" (= 购买自行车) 。  
  
 阴影条的颜色是任意的， 在 Excel 中设置表设计选项即可更改这些颜色。  
  
 在比较两个值的报表中，第二个报表根据对目标值的影响程度为关键影响因素排名。  
  
 由于所有图表都基于 Excel 表，因此可进行筛选和排序，重点关注特定的因素或结果。  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>有关“分析关键影响因素”工具的详细信息  
 当 "**分析关键影响因素**" 工具分析你的数据时，它会执行以下操作：  
  
-   创建一个数据结构，其中存储有关数据分布的关键信息。  
  
-   使用 Microsoft Naïve Bayes 算法创建一个模型。  
  
-   创建将每列数据与指定结果关联起来的预测。  
  
-   使用每个预测的置信度分数找出对产生目标结果影响最大的因素。  
  
-   创建一个报表，其中描述按置信度得分排序的关键影响因素。  
  
### <a name="requirements"></a>要求  
 如果目标列包含连续数值，该工具会自动将这些数值分组。 这些分组表示具有相似特征的事例的分类。 但该工具可能不会将这些数值分成用户友好组。 例如，报表可能包含诸如 "12.85701" 之类的分组 \< ，而报表用户通常想要查看使用整数的分组，如10-19、20-29 等。  
  
 如果希望以其他方式对数值数据分组，必须在创建分析之前以希望的方式拆分这些数据。 例如，您可以使用 Excel 数据挖掘客户端中的 "重新[标记](relabel-sql-server-data-mining-add-ins.md)" 工具在单独的列中创建新的分组标签，然后仅在分析中使用这一新列。  
  
### <a name="related-tools"></a>相关工具  
 "**数据挖掘**" 功能区提供了更高级的工具，包括自定义数据挖掘模型的功能  
  
 如果使用 "**分析关键影响因素**" 工具保存模型，则可以使用数据挖掘客户端浏览模型并更详细地浏览关系。 有关信息，请参阅[在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)。 还可以使用 Microsoft Office Visio 创建图表和关系图，将关系显示为分类或依赖关系网络。 有关详细信息，请参阅[解决 Visio 数据挖掘关系图 &#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)。  
  
> [!NOTE]  
>  在关闭工作表或终止与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接时，将删除使用表分析工具创建的模型。 因此，只有在连接处于打开状态时才能浏览模型。 如果关闭连接或关闭工作表，则无法在 Visio 中呈现模型。  
  
 有关 "**分析关键影响因素**" 工具使用的算法的详细信息，请参阅 SQL Server 联机丛书中的 "Microsoft Bayes 算法"。  
  
## <a name="see-also"></a>另请参阅  
 [用于 Excel 的表分析工具](table-analysis-tools-for-excel.md)   
 [创建数据挖掘模型](creating-a-data-mining-model.md)  
  
  
