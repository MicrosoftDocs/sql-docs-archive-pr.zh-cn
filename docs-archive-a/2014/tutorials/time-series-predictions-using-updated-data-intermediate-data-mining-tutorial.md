---
title: 使用更新的数据 (中级数据挖掘教程) 的时序预测 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2017defaba74071b1a12bee14a5d8907e4c71cda
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577118"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>使用更新数据进行时序预测（数据挖掘中级教程）
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>使用扩展的销售额数据创建预测  
 在本课中，您将创建一个预测查询，该查询将新的销售额数据添加到模型。 通过使用新数据扩展模型，您可以获得最新预测，其中包括最新的数据点。  
  
 创建使用新数据的时序预测非常简单：只需将参数 EXTEND_MODEL_CASES 添加到[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)函数，指定新数据的源，并指定要获取的预测数。  
  
> [!WARNING]  
>  参数 EXTEND_MODEL_CASES 是可选的；默认情况下，通过联接新数据作为输入将该模型扩展您创建时序预测查询的任意时间。  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>生成预测查询和添加新数据  
  
1.  如果模型尚未打开，请双击预测结构，并在数据挖掘设计器中单击 "**挖掘模型预测**" 选项卡。  
  
2.  在 "**挖掘模型**" 窗格中，应该已选择模型预测。 如果未选择此选项，请单击 "**选择模型**"，然后选择模型 "预测"。  
  
3.  在 "**选择输入表 (s) **窗格中，单击"**选择事例表**"。  
  
4.  在 "**选择表**" 对话框中，选择数据源 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 。  
  
     从数据源视图列表中，选择 "NewSalesData"，然后单击 **"确定"**。  
  
5.  右键单击设计区域的图面，然后选择 "**修改连接**"。  
  
6.  使用 "**修改映射**" 对话框，将模型中的列映射到外部数据中的列，如下所示：  
  
    -   将挖掘模型中的 ReportingDate 列映射到输入数据中的 NewDate 列。  
  
    -   将挖掘模型中的量列映射到输入数据中的 NewAmount 列。  
  
    -   将挖掘模型中的 "数量" 列映射到输入数据中的 NewQty 列。  
  
    -   将挖掘模型中的 ModelRegion 列映射到输入数据中的序列列。  
  
7.  现在，您将生成预测查询。  
  
     首先，将一个列添加到预测查询来输出预测应用到的序列。  
  
    1.  在网格中，单击 "**源**" 下的第一个空行，然后选择 "预测"。  
  
    2.  在 "**字段**" 列中，选择 "模型区域"，为 "**别名**" 键入 `Model Region` 。  
  
8.  接下来，添加和编辑预测函数。  
  
    1.  单击一个空行，然后在 "**源**" 下，选择 "**预测函数**"。  
  
    2.  对于 "**字段**"，请选择**PredictTimeSeries**。  
  
    3.  对于 "**别名**"，键入**预测值**。  
  
    4.  从 "**挖掘模型**" 窗格中将字段数量拖到 "**条件/参数**" 列中。  
  
    5.  在 "**条件/参数**" 列中的字段名称后，键入以下文本： **5，EXTEND_MODEL_CASES**  
  
         "**条件/参数**" 文本框的完整文本应该如下所示：`[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. 单击 "**结果**" 并查看结果。  
  
     预测从 7 月（原始数据结束后的第一个时间段）开始，到 11 月结束（原始数据结束后的第 5 个时间段）。  
  
 您可以看到，要高效使用此预测查询类型，您需要知道旧数据何时结束以及新数据中有多少时间段。  
  
 例如，在此模型中，原始数据序列 6 月结束，并且数据针对 7 月、 8 月和 9 月。  
  
 使用 EXTEND_MODEL_CASES 的预测始终在原始数据序列结束时开始。 因此，如果您只想获取未知月份的预测，则需要指定预测的起点和终点。 这两个值被指定为从旧数据结束时开始的一些时间段。  
  
 下面的过程演示如何做到这点。  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>更改预测的起点和终点  
  
1.  在预测查询生成器中，单击 "**查询**" 以切换到 DMX 视图。  
  
2.  找到包含 PredictTimeSeries 函数的 DMX 语句并按以下方式更改它：  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  单击 "**结果**" 并查看结果。  
  
     现在预测从 10 月开始（原始数据结束后的第四个时间段），到 12 月结束（原始数据结束后的第六个时间段）。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [使用替换数据 &#40;中级数据挖掘教程的时序预测&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [时序模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
