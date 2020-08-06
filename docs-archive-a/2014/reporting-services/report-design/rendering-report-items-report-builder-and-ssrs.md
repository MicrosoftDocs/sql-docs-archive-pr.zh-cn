---
title: 呈现报表项（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 99ebb4dc-41cc-42ac-82dd-a2b0e31155a0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4e0b1dabee096cfbaab53227926633f8d7a3697
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586429"
---
# <a name="rendering-report-items-report-builder-and-ssrs"></a>呈现报表项（报表生成器和 SSRS）
  报表项的数量、大小和位置会影响呈现器对表体的分页方式。 下面说明了各种报表项的呈现方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="overlapping-report-items"></a>重叠报表项  
 在 HTML、MHTML、Word、Excel、预览模式或报表查看器中不支持重叠报表项。 如果存在重叠项，则会移动它们。 以下规则应用于重叠报表项：  
  
-   如果报表项的垂直重叠较多，则其中一个重叠项将向右移动。 最左侧的项保持在原位置。  
  
-   如果报表项的水平重叠较多，则其中一个重叠项将向下移动。 最顶端的项保持在原位置。  
  
-   如果垂直重叠和水平重叠相同，则其中一个重叠项将向右移动。 最左侧的项保持在原位置。  
  
-   如果必须将某项移至正确的重叠，则相邻报表项将向下和/或向右移动，以在该项与其上方和/或左侧的报表项之间保持最小间距。 例如，假定两个报表项垂直重叠，并且第三个报表项位于这两项右侧 2 英寸处。 将重叠的报表项向右移动时，第三个报表项也会向右移动，以在其自身与其左侧的报表项之间保持 2 英寸距离。  
  
 硬分页格式（包括打印）支持重叠报表项。  
  
## <a name="visibility-and-report-items"></a>可见性与报表项  
 默认情况下可以隐藏或显示报表项，也可以使用表达式按条件隐藏或显示报表项。 或者，可以通过单击其他报表项来切换可见性。  
  
 呈现报表项时应用下列可见性规则：  
  
-   如果报表项及其内容始终隐藏（不是基于表达式隐藏或不能通过单击其他报表项来切换其可见性），则其右侧或下方的其他报表项不会移动来填充空白区域。 例如，如果矩形及其内包含的图像隐藏，则始于矩形右侧的报表项不会向左移动来填充空白区域。 矩形所占的空间将被保留。  
  
-   如果报表项及其内容按条件隐藏（基于表达式隐藏或通过单击其他报表项来切换其可见性），则其右侧或下方的报表项将向左移动来填充项隐藏时的空间。  
  
-   如果可通过单击其他报表项来切换报表项及其内容的可见性，则仅当报表项最初显示时，才会更改分页来容纳该报表项及其内容。  
  
## <a name="keeping-report-items-together-on-a-single-page"></a>将报表项显示在一页中  
 通过设置分组显示或显示在一起属性，可以显式或隐式地将报表内的许多报表项显示在一页中。 如果报表项没有任何逻辑分页符并且其大小小于可用页面区域，则报表项始终会呈现在同一页中。 如果报表项不能完全适合以通常方式开始的页面，则会在报表项之前插入硬分页符，强制将其显示在下一页。 对于软分页符呈现器，页面会增大以容纳该报表项。  
  
 当报表项始终隐藏时，将忽略将项显示在一起的规则。  
  
 以下项将始终显示在一起：  
  
-   图像。  
  
-   线条：  
  
-   图表、仪表和结构图。  
  
-   单独显示在另一页中的数据区域中的一行，选中分组显示选项。 这样会隐式将这一行与至少一个组实例显示在一起，以便不会使这一行孤立。 可以在数据区域或组中设置此选项。  
  
-   数据区域的标题区域。  
  
-   数据区域的标题区域和第一行数据。  
  
-   可在 Tablix 数据区域中切换的报表项。  
  
### <a name="priority-order"></a>优先级顺序  
 由于页面大小的限制，在将报表项显示在一起的规则之间可能会发生冲突。 发生冲突时，以下优先级顺序用于在呈现时将项显示在一起：  
  
-   线条、图表和图像。  
  
-   末行和孤立行控件。  
  
-   重复的列标题和行标题。  
  
     表头优先于表尾。 内部重复的组优先于外部组。 如果项设置了 `RepeatWith` 属性且距离目标数据区域较近，则这些项优先于距离数据区域较远的项。  
  
-   小报表项（例如文本框或矩形），其显式保持的属性设置为 `true` 。  
  
-   大型报表项（例如子报表或非最内部的 tablix 成员），其显式保持的属性设置为 `true` 。  
  
-   Tablix 数据区域，其显式保持和属性均设置为 `true` 。  
  
### <a name="subreports"></a>子报表  
 子报表呈现为一个包含在单独的报表 .rdl 文件中定义的另一报表的矩形。 子报表文件必须先发布到报表服务器，之后才能由父报表进行访问。  
  
 呈现子报表时应用以下规则：  
  
-   子报表可以增大至在定义子报表的 .rdl 文件中定义的表体大小。 例如，如果子报表的 RDL 指明子报表表体的宽度为 5 英寸，则子报表在父报表内的宽度也将为 5 英寸。  
  
-   子报表将继承父报表的列设置。 会始终忽略原始 RDL 中定义的列设置。  
  
-   将只呈现子报表的表体。 当子报表呈现在父报表中时，将不呈现子报表的 .rdl 文件中定义的表头和表尾部分。  
  
-   子报表具有显式 KeepTogether 属性。 当该属性设置为 `true` 时，如有可能，子报表中的所有项都将显示在一页中。  
  
-   如果子报表无法运行，则会在报表中显示为一个带有错误消息的文本框。 应用于子报表的样式属性将改为应用于该文本框。  
  
-   如果子报表由分页符拆分开，则 **“去掉分页符上的边框”** 设置将控制子报表的边框是关闭还是打开。  
  
 有关子报表的详细信息，请参阅[子报表（报表生成器和 SSRS）](subreports-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
