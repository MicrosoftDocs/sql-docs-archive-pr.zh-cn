---
title: 了解 (中级数据挖掘教程) 的时序模型的要求 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cf92effaabb38a93a294bdf194025a524ad601f3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577121"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>了解时序模型的要求（数据挖掘中级教程）
  准备要在预测模型中使用的数据时，必须确保数据包含可用于标识时序中的步长的列。 该列将被指定为 `Key Time` 列。 由于这是一个键列，所以列中必须包含唯一数值。  
  
 为 `Key Time` 列选择正确的单位是分析中的一个重要部分。 例如，假设您的销售数据每分钟刷新一次。 您不必以分钟作为时序单位；按天、周甚至是月来汇总销售数据可能更有意义。 如果您对要使用的时间单位没有把握，则可为每个聚合都创建一个新的数据源视图，并且生成相关模型，以便查看在聚合的每个级别是否会显现不同的趋势。  
  
 对于本教程，每天都在销售事务数据库中收集销售数据；但对于数据挖掘，则使用一个视图按月预先聚合数据。  
  
 另外，为提高分析的准确性，数据中的空白越少越好。 如果计划分析多个数据序列，所有序列的开始和结束日期应尽量保持相同。 如果序列在其起始位置和结束位置之外的地方存在空白，则可以使用 MISSING_VALUE_SUBSTITUTION 参数来填充该序列。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 还提供了多个选项，用来以均值或常量之类的值来替换缺失数据。  
  
> [!WARNING]  
>  PivotChart 和 PivotTable 工具原来包括在较早版本的数据源视图设计器中，现已不再提供。 我们建议您事先使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中附带的数据事件探查器之类的工具标识时序数据中的空白。  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>标识预测模型的时间键  
  
1.  在 " **salesbyregion.dsv [设计]**" 窗格中，右键单击表 "vTimeSeries"，然后选择 "**浏览数据**"。  
  
     此时将打开一个新的选项卡，标题为 "**浏览 VTimeSeries 表**"。  
  
2.  在 "**表**" 选项卡上，查看在 "TimeIndex" 和 "报告日期" 列中使用的数据。  
  
     两列都是具有唯一值的序列并且都可用作时序键；但是，这两列的数据类型不同。 Microsoft 时序算法不需要 `datetime` 数据类型，只是这些值必须是非重复的且有序的。 因此，这两个列均可用作预测模型的时间键。  
  
3.  在数据源视图设计图面中，选择 "报表日期" 列，然后选择 "**属性**"。 接下来，单击 "TimeIndex" 列，然后选择 "**属性**"。  
  
     字段 TimeIndex 的数据类型为 System.object，而字段报表日期的数据类型为 system.string。 很多数据仓库都将日期/时间值转换为整数，并将整数列用作键，以提高索引性能。 但是，如果您使用此列，Microsoft 时序算法将使用未来值（如 201014、201014，依此类推）进行预测。 由于您想要使用日历日期来表示您的销售数据预测，因此您将使用 "报告日期" 列作为唯一的序列标识符。  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>在数据源视图中设置键  
  
1.  在 " **salesbyregion.dsv**" 窗格中，选择 "vTimeSeries" 表。  
  
2.  右键单击 "报告日期" 列，然后选择 "**设置逻辑主键**"。  
  
## <a name="handling-missing-data-optional"></a>处理缺少的数据（可选）  
 如果任何序列有缺失数据，则您尝试处理模型时可能会遇到错误。 您可以通过以下多种方法来处理缺失数据：  
  
-   可以让 Analysis Services 通过计算均值或使用前一个值来填充缺失值。 可以通过对挖掘模型设置 MISSING_VALUE_SUBSTITUTION 参数来实现此目的。 有关此参数的详细信息，请参阅[Microsoft 时序算法技术参考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。 有关如何更改现有挖掘模型上的参数的信息，请参阅[查看或更改算法参数](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md)。  
  
-   可以更改数据源或筛选基础视图，以消除不规则序列或替换各值。 您可以在关系数据源中实现此目的，或者可以通过创建自行命名的查询或命名计算来修改数据源视图。 有关详细信息，请参阅 [多维模型中的数据源视图](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)。 本课程后面的一个任务将演示如何生成命名查询和自定义计算。  
  
 对于本方案，某一序列的起始位置缺失了某些数据，即：在 2007 年 7 月之前，T1000 产品系列不存在数据。 除此之外，所有序列都在同一天终止，且没有任何缺失值。  
  
 Microsoft 时序算法的要求是，在单个模型中包含的任何序列都应具有相同的**结束**点。 由于 T1000 型号的自行车是在 2007 年引进的，此序列数据的开始日期晚于其他型号自行车数据的开始日期，但此序列的结束日期与其他序列相同；因此，该数据是可使用的。  
  
#### <a name="to-close-the-data-source-view-designer"></a>关闭数据源视图设计器  
  
-   右键单击该选项卡，**浏览 VTimeSeries 表**，然后选择 "**关闭**"。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建预测结构和模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 时序算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
