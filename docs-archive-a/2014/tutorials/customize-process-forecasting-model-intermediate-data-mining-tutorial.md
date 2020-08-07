---
title: 自定义和处理预测模型 (中级数据挖掘教程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 03dc67907b22750eb1b8539feaddec58f61f702f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588784"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>自定义和处理预测模型（数据挖掘中级教程）
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 时序算法提供了多个参数，这些参数影响模型创建方式和时间数据分析方式。 更改这些属性可以极大地影响挖掘模型进行预测的方式。  
  
 对于教程中的此任务，您将执行以下任务来修改模型：  
  
1.  您将通过为*PERIODICITY_HINT*参数添加新值来自定义模型处理时间段的方式。  
  
2.  您将了解 Microsoft 时序算法的两个其他重要参数：FORECAST_METHOD 和 PREDICTION_SMOOTHING，前者用于控制预测使用的方法，后者则用于自定义长期预测和短期预测的组合。  
  
3.  您还可以告知算法要如何处理缺失值（可选）。  
  
4.  在进行所有更改后，您将部署和处理该模型。  
  
## <a name="setting-time-series-parameters"></a>设置时序参数  
 **周期提示**  
  
 *PERIODICITY_HINT*参数提供算法，其中包含有关你预计会在数据中看到的其他时间段的信息。 默认情况下，时序模型将尝试自动检测数据中的模式。 但是，如果您已经知道预期的时间周期，提供周期提示可能提高模型的准确性。 但是，如果您提供错误的周期提示，则会降低准确性；因此，如果不确定应该使用什么值，最好使用默认值。  
  
 例如，用于此模型的视图每月聚合 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 的销售数据。 因此，模型使用的每个时间段表示一个月，所有预测将根据月份给出。 由于一年有12个月的时间，并且你预计销售模式每年都重复一次，因此，你需要将*PERIODICITY_HINT*参数设置为 `12` ，以指示12个时间段 (月) 构成一个完整的销售周期。  
  
 **预测方法**  
  
 *FORECAST_METHOD*参数控制时序算法是否针对短期或长期预测进行了优化。 默认情况下， *FORECAST_METHOD*参数设置为 MIXED，这意味着将混合和平衡两个不同的算法，从而为短期预测和长期预测提供良好的结果。  
  
 但是，如果您知道要使用特殊算法，可以将值更改为 ARIMA 或 ARTXP。  
  
 **加权长期与短期预测**  
  
 还可以使用 PREDICTION_SMOOTHING 参数自定义组合长期预测和短期预测的方式。 默认情况下，此参数设置为 0.5，这通常会提供最佳平衡，从而实现总体准确性。  
  
#### <a name="to-change-the-algorithm-parameters"></a>更改算法参数  
  
1.  在 "**挖掘模型**" 选项卡上，右键单击 "**预测**"，然后选择 "**设置算法参数**"。  
  
2.  在 `PERIODICITY_HINT` "**算法参数**" 对话框的行中，单击 "**值**" 列，然后键入 `{12}` ，包括大括号。  
  
     默认情况下，该算法还将添加值 {1}。  
  
3.  在 `FORECAST_METHOD` 行中，验证 "**值**" 文本框是否为空或设置为 `MIXED` 。 如果输入了不同的值，则键入 `MIXED` 以将参数更改回默认值。  
  
4.  在 " **PREDICTION_SMOOTHING** " 行中，验证 "**值**" 文本框是否为空或设置为0.5。 如果输入了不同的值，请单击 "**值**" 并键入，将 `0.5` 参数更改回默认值。  
  
    > [!NOTE]  
    >  PREDICTION_SMOOTHING 参数仅在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 中可用。 因此，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard 中无法查看或更改 PREDICTION_SMOOTHING 参数的值。 但是，默认行为是使用两种算法并向它们分配相等的权重。  
  
5.  单击“确定”。  
  
## <a name="handling-missing-data-optional"></a>处理缺少的数据（可选）  
 在许多情况下，您的销售数据可能具有用 null 填充的空白，或者某个商店在报告期限之前没有完成报表，在序列末尾留有空白单元。 在这种情况下，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会引发以下错误，将不处理模型。  
  
 "数据挖掘)  (错误：不会从挖掘模型的序列开始同步时间戳 \<series name> \<model name> 。 所有时序必须以相同的时间标记结束，并且不能有随意缺失的数据点。 如果将 MISSING_VALUE_SUBSTITUTION 参数设置为 Previous 或一个数值常量，那么，只要有可能，就将自动修补缺失的数据点。”  
  
 为了避免出现此错误，可以指定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 通过使用以下方法之一自动提供新值以填充空白：  
  
-   使用平均值。 平均值是使用同一数据序列中的所有有效值来计算的。  
  
-   使用以前的值。 可以用以前的值替换多个缺少的单元格，但是不能填充起始值。  
  
-   使用您提供的常量值。  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>指定通过求平均值来填充空白  
  
1.  在 "**挖掘模型**" 选项卡上，右键单击 "**预测**" 列，然后选择 "**设置算法参数**"。  
  
2.  在 "**算法参数**" 对话框的 " **MISSING_VALUE_SUBSTITUTION** " 行中，单击 "**值**" 列，然后键入 `Mean` 。  
  
## <a name="build-the-model"></a>生成模型  
 要使用模型，必须将它部署到服务器，然后通过算法运行定型数据以便处理模型。  
  
#### <a name="to-process-the-forecasting-model"></a>处理预测模型  
  
1.  在的 "**挖掘模型**" 菜单上 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ，选择 "**处理挖掘结构和所有模型**"。  
  
2.  如果出现警告，询问您是否要生成和部署项目，请单击 **"是"**。  
  
3.  在 "**处理挖掘结构-预测**" 对话框中，单击 "**运行**"。  
  
     "**处理进度**" 对话框将打开以显示有关模型处理的信息。 模型处理可能需要一些时间。  
  
4.  处理完成后，单击 "**关闭**" 退出 "**处理进度**" 对话框。  
  
5.  再次单击 "**关闭**" 以退出 "**处理挖掘结构-预测**" 对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [了解 &#40;中级数据挖掘教程的预测模型&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [处理要求和注意事项（数据挖掘）](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
