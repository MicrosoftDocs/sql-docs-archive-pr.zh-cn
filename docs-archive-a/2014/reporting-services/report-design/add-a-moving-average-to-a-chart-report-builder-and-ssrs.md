---
title: 向图表添加移动平均线（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9bc16d0cb45a3240148f931009a836c231b442b5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577290"
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>向图表添加移动平均线（报表生成器和 SSRS）
  移动平均值是序列中数据的平均值，它是根据定义的时间段内的数据计算的。 可以在图表中显示移动平均值来标识明显趋势。  
  
 移动平均值公式是技术分析中最常用的价格指标。 包括平均值、中值和标准偏差在内的许多其他公式也可以从图表的序列中派生。 指定移动平均值时，每个公式可能有一个或多个必须指定的参数。  
  
 在设计模式下添加移动平均值公式时，添加的行序列只会显示为占位符。 该图表将在报表处理期间计算每个公式的数据点。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中不提供对趋势线的内置支持。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>将计算的移动平均值添加到图表的序列  
  
1.  右键单击“ **值** ”区域中的字段，然后单击“ **添加计算序列**”。 随即打开 **“计算序列属性”** 对话框。  
  
2.  从“ **公式** ”下拉列表中选择“ **移动平均值** ”选项。  
  
3.  为表示移动平均值期间的 **“期间”** 指定一个整数值。  
  
    > [!NOTE]  
    >  期间是用来计算移动平均值的天数。 如果未在 X 轴上指定日期／时间值，该期间将由用于计算移动平均值的数据点的数量来表示。 如果只有一个数据点，移动平均值公式将不会进行计算。 移动平均值从第二个点处开始计算。 如果您指定 **“从第一点开始”** 选项，则图表将从第一个点处的移动平均值开始。 如果只有一个数据点，则计算出的移动平均值中的点将与原始序列中的第一个点一致。  
  
## <a name="see-also"></a>另请参阅  
 [设置图表格式 &#40;报表生成器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [图表 &#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [向图表添加空点 &#40;报表生成器和 SSRS&#41;](add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  
