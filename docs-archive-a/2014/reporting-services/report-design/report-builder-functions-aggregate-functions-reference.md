---
title: 聚合函数参考（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b7c88935b303d36e73741bee17e966ec6616a030
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691604"
---
# <a name="aggregate-functions-reference-report-builder-and-ssrs"></a>聚合函数引用（报表生成器和 SSRS）
  若要在报表中包含聚合值，您可以在表达式中使用内置聚合函数。 数值字段的默认聚合函数是 SUM。 您可以编辑表达式，并使用其他内置聚合函数或指定不同的作用域。 作用域标识要用于计算的一组数据。  
  
 当报表处理器将报表数据和报表布局组合在一起时，将计算每个报表项的表达式。 当您查看每个报表页时，您将会在呈现的报表项中看到每个表达式的结果。  
  
 下表列出了您可以包括在表达式中的内置函数的类别：  
  
-   [内置聚合函数](#CalculatingAggregates)  
  
-   [对内置字段、集合和聚合函数的限制](#Restrictions)  
  
-   [对嵌套聚合的限制](#NestedRestrictions)  
  
-   [计算运行值](#CalculatingRunningValues)  
  
-   [检索行计数](#RetrievingRowCounts)  
  
-   [从另一个数据集中查找值](#LookupFunctions)  
  
-   [检索依赖排序的值](#RetrievingPostsortValues)  
  
-   [检索服务器聚合](#RetrievingServerAggregates)  
  
-   [检索递归级别](#RetrievingRecursiveLevel)  
  
-   [测试作用域](#TestingforScope)  
  
 若要确定函数的有效作用域，请参阅各个函数参考主题。 有关详细信息和示例，请参阅 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="built-in-aggregate-functions"></a><a name="CalculatingAggregates"></a> 内置聚合函数  
 下列内置函数为默认作用域或命名作用域中的一组非 Null 数值数据计算汇总值。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[Avg](report-builder-functions-avg-function.md)|返回在给定作用域中计算的、由表达式指定的所有非 Null 数值的平均值。|  
|[Count](report-builder-functions-count-function.md)|返回在给定作用域上下文中计算的，由表达式指定的非 Null 值的计数。|  
|[CountDistinct](report-builder-functions-countdistinct-function.md)|返回在给定作用域上下文中计算的，由表达式指定的所有非重复的非 Null 值计数。|  
|[Max](report-builder-functions-max-function.md)|返回在给定作用域上下文中由表达式指定的所有非 Null 数值的最大值。 可以使用此函数指定图表轴最大值以控制刻度。|  
|[Min](report-builder-functions-min-function.md)|返回在给定作用域上下文中由表达式指定的所有非 Null 数值的最小值。 可以使用此函数指定图表轴最小值以控制刻度。|  
|[StDev](report-builder-functions-stdev-function.md)|返回在给定作用域中计算的，由表达式指定的所有非 Null 数值的标准偏差。|  
|[StDevP](report-builder-functions-stdevp-function.md)|返回在给定作用域上下文中计算的，由表达式指定的所有非 Null 数值的总体标准偏差。|  
|[Sum](report-builder-functions-sum-function.md)|返回在给定作用域中计算的、由表达式指定的所有非 Null 数值的和。|  
|[Union](report-builder-functions-union-function.md)|返回在给定作用域中计算的、由表达式指定的 `SqlGeometry` 类型或 `SqlGeography` 类型的所有非 Null 的空间数据值的联合。|  
|[Var](report-builder-functions-var-function.md)|返回在给定作用域中计算的，由表达式指定的所有非 Null 数值的方差。|  
|[VarP](report-builder-functions-varp-function.md)|返回在给定作用域上下文中计算的、由表达式指定的所有非 Null 数值的总体方差。|  
  
##  <a name="restrictions-on-built-in-fields-collections-and-aggregate-functions"></a><a name="Restrictions"></a>对内置字段、集合和聚合函数的限制  
 下表汇总了可以在其中添加表达式（包含对全局内置集合的引用）的报表位置的限制。  
  
|报表中的位置|字段|参数|ReportItems|PageNumber<br /><br /> TotalPages|数据源<br /><br /> 数据集|变量|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|页眉<br /><br /> 页脚|是|是|最多一个<br /><br /> 注释 1|是|是|是|是|  
|正文|是<br /><br /> 注释 2|是|仅限当前作用域或包含作用域中的项<br /><br /> 注释 3|否|是|是|是|  
|报表参数|否|仅限列表中前面的参数<br /><br /> 注释 4|否|否|否|否|否|  
|字段|是|是|否|否|否|否|否|  
|查询参数|否|是|否|否|否|否|否|  
|组表达式|是|是|否|否|是|否|否|  
|排序表达式|是|是|否|否|是|是<br /><br /> 注释 5|否|  
|筛选表达式|是|是|否|否|是|是<br /><br /> 注释 6|否|  
|代码|否|是<br /><br /> 注释 7|否|否|否|否|否|  
|报表语言|否|是|否|否|否|否|否|  
|变量|是|是|否|否|是|当前作用域或包含作用域|否|  
|聚合|是|是|仅在页眉/页脚中|仅在报表项聚合中|是|否|否|  
|Lookup 函数|是|是|是|否|是|否|否|  
  
-   **备注1。** ReportItems 必须存在于呈现的报表页中，否则其值为 Null。 如果报表项的可见性取决于计算结果为 False 的表达式，则该页不存在此报表项。  
  
-   **备注2。** 如果在组作用域中使用了字段引用，并且该字段引用不包含在组表达式中，则未定义该字段的值，除非在该作用域中只有一个值。 若要指定值，请使用“First”或“Last”以及组作用域。  
  
-   **备注3。** 包含对 ReportItems 的引用的表达式可以为相同组作用域或包含组作用域中的其他 ReportItems 指定值。  
  
-   **注释 4。** 前面参数的属性值可能为 Null。  
  
-   **备注5。** 仅在成员排序中使用。 不能在数据区域排序表达式中使用。  
  
-   **注释 6。** 仅在成员筛选器中使用。 不能在数据区域或数据集筛选表达式中使用。  
  
-   **注释 7。** 处理代码块后，才可以初始化参数集合，因此，这些方法不能用于控制初始化上的参数。  
  
-   **注释 8。** 除 Count 和 CountDistinct 之外的所有聚合数据类型都必须为相同的数据类型或者所有值都为 null。  
  
##  <a name="restrictions-on-nested-aggregates"></a><a name="NestedRestrictions"></a> 对嵌套聚合的限制  
 下表汇总了对可以将其他聚合函数指定为嵌套函数的聚合函数的限制。  
  
|上下文|RunningValue|RowNumber|First<br /><br /> 上一个|上一篇|Sum 和其他预排序函数|ReportItem 聚合|Lookup 函数|Aggregate 函数|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|运行值|否|否|否|否|是|否|是|否|  
|First<br /><br /> 上一个|否|否|否|否|是|否|否|否|  
|上一篇|是|是|是|否|是|否|是|否|  
|Sum 和其他预排序函数|否|否|否|否|是|否|是|否|  
|ReportItem 聚合|否|否|否|否|否|否|否|否|  
|Lookup 函数|是|是<br /><br /> 注释 1|是<br /><br /> 注释 1|是<br /><br /> 注释 1|是<br /><br /> 注释 1|是<br /><br /> 注释 1|否|否|  
|Aggregate 函数|否|否|否|否|否|否|否|否|  
  
-   **备注1。** 如果 Lookup 函数未包含在聚合中，则聚合函数仅适用于 Lookup 函数的 *Source* 表达式中。 聚合函数不适用于 Lookup 函数的 *Destination* 表达式或 *Result* 表达式中。  
  
##  <a name="calculating-running-values"></a><a name="CalculatingRunningValues"></a>计算运行值  
 以下内置函数计算一组数据的运行值。 `RowNumber` 类似于 `RunningValue`，它将返回计数的运行值，该计数针对包含作用域中的每一行进行递增。 这些函数的作用域参数必须指定包含作用域，用于控制计数开始的时间。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[RowNumber](report-builder-functions-rownumber-function.md)|返回指定作用域内行数的运行计数。 `RowNumber` 函数从 1 开始重新计数，而不是从 0 开始。|  
|[RunningValue](report-builder-functions-runningvalue-function.md)|返回在给定作用域中计算的，由表达式指定的所有非 Null 数值的运行聚合。|  
  
##  <a name="retrieving-row-counts"></a><a name="RetrievingRowCounts"></a>检索行计数  
 下列内置函数计算给定作用域内的行数。 使用此函数可以对所有行进行计数，包括含有 Null 值的行。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[CountRows](report-builder-functions-countrows-function.md)|返回指定作用域内的行数，包括含有 Null 值的行。|  
  
##  <a name="looking-up-values-from-another-dataset"></a><a name="LookupFunctions"></a>从另一个数据集中查找值  
 下面的查找函数从指定数据集中检索值。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[Lookup 函数](report-builder-functions-lookup-function.md)|从数据集中返回指定表达式的值。|  
|[LookupSet 函数](report-builder-functions-lookupset-function.md)|从数据集中返回指定表达式的一组值。|  
|[Multilookup 函数](report-builder-functions-multilookup-function.md)|从包含名称/值对的数据集中返回一组名称的第一个匹配值的集合。|  
  
##  <a name="retrieving-sort-dependent-values"></a><a name="RetrievingPostsortValues"></a>检索排序依赖值  
 下列内置函数返回给定作用域内第一个、最后一个或以前的值。 这些函数依赖数据值的排序顺序。 例如，可以使用这些函数查找页上的第一个和最后一个值来创建字典样式页眉。 使用 `Previous` 可以将指定作用域内某一行中的值与该行以前的值进行比较，例如，使用它可以查出表中的年度同比百分比值。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[First](report-builder-functions-first-function.md)|返回指定表达式的给定作用域中的第一个值。|  
|[时间](report-builder-functions-last-function.md)|返回指定表达式的给定作用域中的最后一个值。|  
|[上一页](report-builder-functions-previous-function.md)|返回指定作用域内某项的前一个实例的值或该实例的指定聚合值。|  
  
##  <a name="retrieving-server-aggregates"></a><a name="RetrievingServerAggregates"></a>检索服务器聚合  
 下列内置函数从数据访问接口中检索自定义聚合。 例如，使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据源类型可以检索在用于组头的数据源服务器上计算的聚合。  
  
|**Function**|**说明**|  
|------------------|---------------------|  
|[聚合](report-builder-functions-aggregate-function.md)|按照数据访问接口的定义返回指定表达式的自定义聚合。|  
  
##  <a name="testing-for-scope"></a><a name="TestingforScope"></a>测试范围  
 下列内置函数测试报表项的当前上下文，以确定该报表项是否为特定作用域的成员。  
  
|函数|说明|  
|--------------|-----------------|  
|[InScope](report-builder-functions-inscope-function.md)|指示项的当前实例是否在指定的作用域内。|  
  
##  <a name="retrieving-recursive-level"></a><a name="RetrievingRecursiveLevel"></a>正在检索递归级别  
 下列内置函数检索处理递归层次结构时的当前级别。 此函数的结果与文本框中的 `Padding` 属性配合使用可以控制递归组可视层次结构的缩进级别。 有关详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
|函数|说明|  
|--------------|-----------------|  
|[级别](report-builder-functions-level-function.md)|返回在递归层次结构中的当前深度级别。|  
  
## <a name="see-also"></a>另请参阅  
 [表达式在报表中使用 &#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
