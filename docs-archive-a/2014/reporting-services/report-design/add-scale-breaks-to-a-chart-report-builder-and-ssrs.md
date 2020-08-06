---
title: 在图表中添加刻度分隔线（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 84d66436-ed62-4967-bbbd-b457593ee787
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1c081debd1e0a84158615edebdb6b84705c10e5b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691086"
---
# <a name="add-scale-breaks-to-a-chart-report-builder-and-ssrs"></a>在图表中添加刻度分隔线（报表生成器和 SSRS）
  刻度分隔线是在图表的绘图区绘制的一个条带，表示值轴（通常为垂直轴或 Y 轴）上高值和低值之间的一个中断。 使用刻度分隔线可以在同一图表区中显示两个不同范围。  
  
 ![具有刻度分割线的图表](../media/rs-multipledatarangeschart-scalebreak.gif "具有刻度分割线的图表")  
  
> [!NOTE]  
>  您不能指定在图表中放置刻度分隔线的位置。 图表根据数据集中的值使用自有的计算方法确定数据范围之间是否有足够的分离空间，以便在运行时的值轴（Y 轴）上绘制刻度分隔线。  
  
 具有刻度分隔线的图表的示例可用于示例报表。 有关下载此示例报表和其他内容的详细信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [报表生成器和报表设计器示例报表](https://go.microsoft.com/fwlink/?LinkId=198283)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-scale-breaks-on-the-chart"></a>启用图表中的刻度分隔线  
  
1.  右键单击垂直轴，然后单击“轴属性”  。 随即将打开“垂直轴属性”  对话框。  
  
2.  选中 **“启用刻度分隔线”** 复选框。  
  
### <a name="to-change-the-style-of-the-scale-break"></a>更改刻度分隔线的样式  
  
1.  打开“属性”窗格。  
  
2.  在设计图面上，右键单击图表中的 Y 轴。 Y 轴对象（默认情况下名为“图表轴”）的属性显示在“属性”窗格中。  
  
3.  在“刻度线”  部分，展开 ScaleBreakStyle 属性。  
  
4.  更改 ScaleBreakStyle 属性（如 BreakLineType 和 Spacing）的值。 有关设置刻度分隔线属性的详细信息，请参阅[在图表中显示包含多个数据区域的序列（报表生成器和 SSRS）](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)。  
  
## <a name="see-also"></a>另请参阅  
 [图表 &#40;报表生成器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [设置图表格式 &#40;报表生成器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [“轴属性”对话框 -&gt;“轴选项”（报表生成器和 SSRS）](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
