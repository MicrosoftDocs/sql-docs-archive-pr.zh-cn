---
title: 浏览器 (多维数据集设计器)  (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6ca5d5e314284bbb4d1c9e2cd88aa64ca4970aa9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579332"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>浏览器（多维数据集设计器）（Analysis Services - 多维数据）
  可以使用多维数据集设计器中的 **“浏览器”** 选项卡浏览多维数据集中的维度、度量值和 KPI。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集浏览器已与 MDX 查询设计器集成，并提供图形用户界面来帮助您创建 MDX 查询、筛选器和多维数据集切片，以及在层次结构中深化。

 **“浏览器”** 选项卡有两种模式： **“设计模式”** 和 **“查询模式”**。 在每种模式下，您都可以使用 **“元数据”** 窗格中的对象来浏览该多维数据集，也可以将 **“元数据”** 窗格中的成员拖入查询区域，以生成可检索要使用的数据的 MDX 查询。

 **使用图形设计模式浏览和查询**

 下图显示图形 **“设计模式”** 中的 **“浏览器”** 界面。

 ![Analysis Services MDX 查询设计器的设计视图](media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查询设计器的设计视图")

 在图形设计模式下工作时，如果**自动执行** (自动执行工具栏上![的 "查询"](media/rsqdicon-autoexecute.gif "自动执行查询")) 切换按钮，则每次将元数据对象拖到 "数据" 窗格时，**浏览器**都将运行查询。 你还可以使用 "**执行查询**" 手动运行查询， (在工具栏上![运行 "查询](media/rsqdicon-run.gif "运行查询")) " 按钮。

 若要将图形查询设计器更改为 **“查询”** 模式并处理 MDX 语句的文本，请单击工具栏上的 **“设计模式”** 按钮。

 **使用 MDX 文本模式浏览和查询**

 处于 MDX 文本设计模式中时，您可以直接使用 MDX。 **“元数据”** 窗格仍然可用，这样您可以向查询设计区域添加对象，同时您可以从 **“函数”** 窗格中的列表拖放 MDX 函数和运算符。

 下图显示查询模式的 **“浏览器”** 界面。

 ![Analysis Services MDX 查询设计器的查询视图](media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX 查询设计器的查询视图")

 您可以先在图形设计模式中开始工作，添加所有必需对象，添加筛选器对多维数据集进行切片，然后切换到文本模式以扩展生成的默认 MDX 查询，并包括更多成员属性和单元属性。

 **“元数据”** 窗格将显示 **“元数据”** 选项卡和 **“函数”** 选项卡。 通过 **“元数据”** 选项卡，可将维度、层次结构、KPI 和度量值拖到查询设计区域。 从 **“函数”** 选项卡上，您可以将函数拖至查询设计区域。 执行查询时，查询设计区域会显示 MDX 查询的结果。 还可以单击 **“工具栏”** 上的 **“在 Excel 中分析”** ，将数据导出到 Microsoft Office Excel，并像用户那样在数据透视表中查看结果。以下几节详细介绍每种模式的 **“浏览器”** 中的工具栏按钮和所有窗格。

 请注意，在文本模式下工作时，**自动执行** (自动执行工具栏上![的 "查询](media/rsqdicon-autoexecute.gif "自动执行查询")) 切换" 按钮不可用。 不过，您可以通过使用 "**执行查询**" () 工具栏上的 "执行![查询" 按钮](media/rsqdicon-run.gif "运行查询")来手动运行查询。

## <a name="sections"></a>部分
 **“在 Excel 中分析”** 工具栏中包含可以在设计视图或查询视图中使用的工具。 有关工具栏以及如何使用其功能的详细信息，请参阅[工具栏（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)。

 **“工具栏”** 可以使用多维数据集设计器中的 **“工具栏”** 功能可以将当前选定的多维数据集数据发送到 Excel，这样您就可以在数据透视表中预览这些数据。 当前选定的数据基于您从 **“元数据”** 窗格中添加的项以及您使用筛选器和查询生成函数可能已经定义的所有筛选器。 有关详细信息，请参阅[在 Excel 中分析（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)。

 **“元数据”** 可以使用多维数据集设计器中的 **“元数据”** 窗格可以查看多维数据集所包含的对象，以便在层次结构中深化以及浏览和使用度量值。 选择多维数据集后，您可以在 **“报表”** 窗格中查看与所选多维数据集相关联的数据。 有关此窗格的详细信息，请参阅[元数据（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)。

 **筛选和查询** 使用设计图面的这一区域可以生成 MDX 查询，只需从 **“元数据”** 窗格中拖放对象，并对源多维数据集或维度指定筛选条件。 有关详细信息，请参阅[查询和筛选（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)。

## <a name="see-also"></a>另请参阅
 [多维](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)[数据集](multidimensional-models/cubes-in-multidimensional-models.md)&#40;多维数据集中&#41;多维数据集 Analysis Services 多维数据集的多维数据集对象[&#40;Analysis Services 多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)


