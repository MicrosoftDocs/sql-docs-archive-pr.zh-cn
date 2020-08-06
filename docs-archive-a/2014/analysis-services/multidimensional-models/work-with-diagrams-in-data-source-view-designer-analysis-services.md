---
title: 使用数据源视图设计器中的关系图 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.diagramorganizerpane.f1
- sql12.asvs.dsvdesigner.findtable.f1
- sql12.asvs.dsvdesigner.diagrampane.f1
helpviewer_keywords:
- data source views [Analysis Services], diagrams
- diagrams [Analysis Services]
ms.assetid: 491fdd22-2326-4f27-a0dd-0a02faae3fd8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 40a58ed33ff6cfaebf2a6e7c084500dd3ae072da
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587045"
---
# <a name="work-with-diagrams-in-data-source-view-designer-analysis-services"></a>使用数据源视图设计器中的关系图 (Analysis Services)
  数据源视图 (DSV) 关系图是 DSV 中对象的直观表示形式。 您可以交互使用该关系图以添加、隐藏、删除或修改特定对象。 还可以对同一 DSV 创建多个关系图以特别关注对象的某个子集。  
  
 若要更改关系图窗格中显示的关系图区域，请单击该窗格右下角的四向箭头，然后在关系图的缩略图上拖动选择框，直到选定要在关系图窗格中显示的区域为止。  
  
 本主题包含下列部分：  
  
 [添加关系图](#bkmk_add)  
  
 [编辑或删除关系图](#bkmk_edit)  
  
 [在关系图中查找表](#bkmk_findtables)  
  
 [排列关系图中的对象](#bkmk_arrangeobjects)  
  
 [保留对象排列](#bkmk_preserve)  
  
##  <a name="add-a-diagram"></a><a name="bkmk_add"></a> 添加关系图  
 创建 DSV 时自动创建 DSV 关系图。 在 DSV 存在后，您可以创建其他关系图、删除它们或隐藏特定对象以创建更便于管理的 DSV 表示形式。  
  
 若要创建新关系图，请右键单击“关系图组织程序”**** 窗格中的任意地方，再单击“新建关系图”****。  
  
 当您在 Analysis Services 项目中最初定义数据源视图 (DSV) 时，添加到数据源视图的所有表和视图都将添加到 \<All Tables> 关系图中。 在数据源视图设计器的“关系图组织程序”窗格中将显示此关系图，在“表”窗格中将列出此关系图中的表及其列和关系，并在架构窗格中将以图形方式显示此关系图中的表及其列和关系。 但是，当您向关系图中添加表、视图和命名查询时 \<All Tables> ，此关系图中的对象数量非常困难，尤其是将多个事实数据表添加到关系图中，维度表与多个事实数据表相关。  
  
 当您只需要在数据源视图中查看表的子集时，若要减少视觉混乱，可以定义由数据源视图中所选表、视图和命名查询的子集组成的子关系图（简称为关系图）。 根据业务或解决方案的需要，可以使用关系图对数据源视图中的项进行分组。  
  
 您可以将相关表和命名查询分组到单独的关系图中以便用于业务，这样可以使包含许多表、视图和命名查询的数据源视图更易于理解。 同一个表或命名查询可以包含在多个关系图中， \<All Tables> 关系图除外。 在 \<All Tables> 关系图中，数据源视图中包含的所有对象都只显示一次。  
  
##  <a name="edit-or-delete-a-diagram"></a><a name="bkmk_edit"></a>编辑或删除关系图  
 使用关系图时，要特别注意用于添加和删除对象的命令。 例如，从关系图中删除对象时会将它从 DSV 中删除。 如果您只想将其从关系图中删除，请改用 **“隐藏表”** 。  
  
 ![“关系图”工作区的右键单击菜单的屏幕快照](../media/ssas-olapdsv-diagram.gif "“关系图”工作区的右键单击菜单的屏幕快照")  
  
 尽管您可以逐个隐藏对象，但是使用“显示相关表”命令可将所有相关对象重新显示在关系图中。 若要控制将哪些对象返回到工作区，请从“表”窗格中拖动它们。  
  
##  <a name="find-tables-in-a-diagram"></a><a name="bkmk_findtables"></a>在关系图中查找表  
 如果架构很大，则在 **“关系图”** 窗格中滚动到特定表可能很困难。 但是，下列工具将使在关系图中查找表变得容易。  
  
-   在 **“表”** 窗格中滚动表列表。  
  
     若要在当前显示的关系图中包括某个表，请将该表从 **“表”** 窗格拖到关系图窗格中。  
  
     若要将显示焦点置于已包含在关系图中的某个表上，请在 **“表”** 窗格中选择相应的表。  
  
-   **关系图**窗格中的表定位器—表定位器是一个4向箭头图标，位于 "**关系图**" 窗格右下角的垂直和水平滚动条的交点处。 它可打开“关系图”窗格中当前关系图的缩略图表示。 您可以使用此缩略图将“关系图”窗格中的视图更改到关系图的任何位置。  
  
-   使用 "**查找表**" 对话框-右键单击 "关系图" 窗格中的 "打开区域"，然后单击 "**查找表**"。 或者，单击工具栏或 **“数据源视图”** 菜单上的 **“查找表”** 命令。  
  
     您可以在“筛选器”框中键入字符串和通配符以查看关系图中的表的子集。  
  
##  <a name="arrange-objects-in-a-diagram"></a><a name="bkmk_arrangeobjects"></a> 在关系图中排列对象  
 虽然数据源视图设计器可以定义多个关系图，从而使得 DSV 更易于理解，但是，包含大量表的关系图可能难以读取，并且手动重新排列表的布局也是一个乏味的过程。 根据当前关系图中表与表之间的关系，数据源视图设计器可以使用矩形布局或对角线布局，自动重新排列当前关系图中的表。  
  
-   在矩形布局中，将在表与表之间（而不是列与列之间）绘制关系线。 表与表之间绘制有水平和垂直的关系线。  
  
-   在对角线布局中，将在表中相关列之间尽可能直接地绘制关系线。 多列之间的关系将附加到表中的第一个相关列。 如果表中的列不可见，则会在表的顶部绘制关系线。  
  
##  <a name="preserve-object-arrangement"></a><a name="bkmk_preserve"></a>保留对象排列  
 在按所需方式手动排列表后，在关系图中添加更多表可能导致关系图刷新，从而删除最近对对象布局所做的所有修改。  
  
 在添加表（此操作会使关系图组织程序移动其他表以便容纳新表）时，更有可能出现此行为。 它随后重新绘制关系图以确保正确表示所有表和连接线。 此时，对特定对象的位置进行的所有手动调整都可能丢失。  
  
 为避免此问题，请首先添加所有表，然后再进行任何最终调整。 以后重新打开关系图时，对象应该保留它们在关系图中的位置。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)   
 [数据源视图设计器（Analysis Services - 多维数据）](../data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
