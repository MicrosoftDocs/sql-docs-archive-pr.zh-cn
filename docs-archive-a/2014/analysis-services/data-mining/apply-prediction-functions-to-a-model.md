---
title: 将预测函数应用于模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
author: minewiskan
ms.author: owend
ms.openlocfilehash: fde9de00adaa1712a9db6e18aabc6a83dd660efb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577924"
---
# <a name="apply-prediction-functions-to-a-model"></a>将预测函数应用于模型
  若要创建预测查询，必须先选择查询基于的挖掘模型。 可以选择当前项目中存在的任何挖掘模型。  
  
 选择模型后，可向查询添加 *预测函数* 。 导入是为了理解预测函数用于许多用途-是的，你可以预测值，但也可以获取相关的统计信息，以及在生成预测时使用的信息。 预测函数可返回以下类型的值：  
  
-   可预测属性的名称和预测到的值。  
  
-   有关预测值的分布和方差的统计信息。  
  
-   指定结果或所有可能结果的概率。  
  
-   探顶分数或探底分数，探顶值或探底值。  
  
-   与指定节点、对象或属性关联的值。  
  
 虽然有多种预测函数可供您使用，但您必须选择适用于您创建的模型类型的函数。 此选择一般取决于创建模型所用的算法。  
  
-   有关几乎所有模型类型都支持的预测函数的列表，请参阅[通用预测函数 (DMX)](/sql/dmx/general-prediction-functions-dmx)。  
  
-   此外，各算法还支持多种专用函数。 例如，如果基于 Microsoft 聚类分析算法创建了挖掘模型，则可以使用专门的预测函数来查找有关群集的信息，如从数据值到群集形心的距离。  
  
     有关如何查询特定类型的挖掘模型的示例，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)中的算法参考主题。  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>选择用于预测的挖掘模型  
  
1.  从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击模型，然后选择“生成预测查询”****。  
  
     -- 或者 --  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击选项卡 **“挖掘模型预测”**，然后单击 **“挖掘模型”** 表中的  **“选择模型”** 。  
  
2.  在 **“选择挖掘模型”** 对话框中，选择挖掘模型，然后单击 **“确定”**。  
  
     您可以选择当前 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的任何模型。 若要使用其他数据库中的模型创建查询，则必须在该数据库的上下文中打开新查询窗口，或打开包含该模型的解决方案文件。  
  
### <a name="add-prediction-functions-to-a-query"></a>向查询添加预测函数  
  
1.  在 **“预测查询生成器”** 中，通过在 **“单独查询输入”** 对话框中提供值或将模型映射到外部数据源来配置用于预测的输入数据。  
  
     有关详细信息，请参阅 [为预测查询选择和映射输入数据](choose-and-map-input-data-for-a-prediction-query.md)。  
  
    > [!WARNING]  
    >  无需提供用于生成预测的输入。 当没有输入时，算法通常将返回所有可能的输入中可能性最大的预测值。  
  
2.  单击 **“源”** 列，然后从列表中选择一个值：  
  
    |||  
    |-|-|  
    |**\<model name>**|选择此选项将在输出中包含挖掘模型的值。 只能添加可预测的列。<br /><br /> 从模型添加列时，返回的结果是该列中值的重复列表。<br /><br /> 使用此选项添加的列将包含在生成的 DMX 语句的 SELECT 部分。|  
    |**Prediction Function**|选择此选项将浏览预测函数的列表。<br /><br /> 您选择的值或函数将添加到生成的 DMX 语句的 SELECT 部分。<br /><br /> 已选择的模型的类型不会筛选或约束预测函数的列表。 因此，如果对当前模型类型是否支持该函数有任何疑问，则可以只将函数添加到列表并查看是否出错。<br /><br /> 前置有 $ 的列表项（如 $AdjustedProbability）表示您使用函数 `PredictHistogram` 时输出的嵌套表中的列。 这些是可用于返回单个列而不返回嵌套表的快捷方式。|  
    |**自定义表达式**|选择此选项将键入自定义表达式然后向输出分配别名。<br /><br /> 自定义表达式将添加到生成的 DMX 预测查询的 SELECT 部分。<br /><br /> 如果要为每行的输出添加文本、调用 VB 函数或调用自定义存储过程，则此选项会很有用。<br /><br /> 有关使用 DMX 中的 VBA 和 Excel 函数的信息，请参阅 [MDX 和 DAX 中的 VBA 函数](/sql/mdx/vba-functions-in-mdx-and-dax)。|  
  
3.  在添加每个函数或表达式后，切换到 DMX 视图可查看该函数在 DMX 语句中的添加方式。  
  
    > [!WARNING]  
    >  在您单击 **“结果”** 之前，预测查询生成器不会验证 DMX。 通常，您会发现查询生成器所生成的表达式不是有效 DMX。 典型的原因是，引用的列与可预测列不相关或尝试预测嵌套表中的列（这需要嵌套 SELECT 语句）。 此时，您可以切换到 DMX 视图并继续编辑该语句。  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>示例：创建对聚类分析模型的查询  
  
1.  如果没有可用于生成此示例查询的聚类分析模型，请使用 [数据挖掘基础教程](../../tutorials/basic-data-mining-tutorial.md)创建 [TM_Clustering] 模型。  
  
2.  从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击模型 [TM_Clustering]，然后选择“生成预测查询”****。  
  
3.  从 **“挖掘模型”** 菜单中选择 **“单独查询”**。  
  
4.  在 **“单独查询输入”** 对话框中，将以下值设置为输入：  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  在查询网格中，为“源”**** 选择 TM_Clustering 挖掘模型并添加列 [Bike Buyer]。  
  
6.  对于 "**源**"，选择 "**预测函数**" 并添加函数 `Cluster` 。  
  
7.  对于 "**源**"，选择 "**预测函数**"，添加函数， `PredictSupport` 并将 "模型" 列 [自行车买家] 拖到 "**条件/参数**" 框中。 在“别名”列中键入 **Support** 。 ****  
  
     从“条件/参数”**** 框复制表示预测函数和列引用的表达式。  
  
8.  为 **“源”** 选择 **“自定义表达式”**，键入别名，然后使用以下语法引用 Excel CEILING 函数：  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     将列引用作为该函数的参数粘贴。  
  
     例如，下面的表达式返回支持值的 CEILING：  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     在 **“别名”** 列中键入 CEILING。  
  
9. 单击 **“切换到查询文本视图”** 检查生成的 DMX 语句，然后单击 **“切换到查询结果视图”** 查看预测查询输出的列。  
  
     下表显示了预期的结果：  
  
    |Bike Buyer|$Cluster|Support|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|群集 8|954|953.948638926372|  
  
 如果要在语句中的其他位置添加其他子句（例如，如果要添加 WHERE 子句），则无法使用网格添加该子句;必须先切换到 DMX 视图。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘查询](data-mining-queries.md)  
  
  
