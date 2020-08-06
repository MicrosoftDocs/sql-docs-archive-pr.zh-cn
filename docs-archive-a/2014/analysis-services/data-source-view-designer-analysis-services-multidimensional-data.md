---
title: 数据源视图设计器 (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
ms.openlocfilehash: 31e70f3f9b577f44b9ebb61b5ae2975c0a129828
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690228"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>数据源视图设计器（Analysis Services - 多维数据）
  数据源视图 (DSV) 是用于在多维模型中创建多维数据集和维度的外部关系数据源的逻辑视图。

 在生成 DSV 后，您可以在 **中使用** 数据源视图设计器 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 直接在 DSV 中工作，这在基础数据源缺少多维模型所需的数据元素时很有用。

 打开 **数据源视图设计器** ：

-   双击“解决方案资源管理器”**** 中的某个数据源视图。

-   在“解决方案资源管理器”**** 中右键单击某个数据源视图，选择“打开”或“视图设计器”********。

 **数据源视图设计器** 包含一个工具栏、一个显示 DSV 中对象及关系的图表、一个按字母顺序列出表和命名查询的表窗格，以及用于创建和查看 DSV 的特定图表的“关系图组织程序”窗格。 您可以通过右键单击某个表或关系来访问上下文相关命令。

 ![数据源视图设计器](media/ssas-dsvdesigner.PNG "数据源视图设计器")

 DSV 中至少会显示将用于在处理期间填充模型对象的关系数据库表。 通常可使用数据源视图向导生成 DSV。 DSV 中的表、列和关系将成为多维数据集中维度和度量值的基础。 在创建 DSV 后，可以使用数据源视图设计器修改它。

 大多数 Analysis Services 开发人员都会使用已生成的现有 DSV，并进行少量自定义。 特别是在源数据来自 SQL Server 数据库中的视图时尤其如此。 在这种情况下，您可能更希望在 T-SQL 视图（而不是在 Analysis Services DSV）中管理数据关系和计算。 但是，如果您不是基础数据库的所有者，则可以在 Analysis Services 中修改 DSV 以便进一步开发您的模型中使用的数据结构。

## <a name="tasks-in-data-source-view-designer"></a>数据源视图设计器中的任务
 使用数据源视图设计器，您可以对 DSV 进行以下编辑：

|||
|-|-|
|重命名列或表，或者创建新的计算列。 例如，可将名字和姓氏连接到新的全名列。|[在数据源视图中定义命名计算 (Analysis Services)](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|
|手动添加表关系|[在数据源视图中定义逻辑关系 (Analysis Services)](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|
|创建命名查询以定义基于 T-SQL 查询的新对象。|[在数据源视图中定义命名查询 (Analysis Services)](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|
|研究基础数据以查看模型对象表示的实际数据值。<br /><br /> 通过数据浏览，您可以直观地检查和复制从基础维度表或查询返回的数据。 默认情况下，数据浏览使用靠前计数抽样方法，具有 5000 个抽样计数，但您可以修正这些设置。|[在数据源视图中浏览数据 (Analysis Services)](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|
|为 DSV 中的所有或部分表和关系绘制关系图|[使用数据源视图设计器中的关系图 (Analysis Services)](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|

## <a name="see-also"></a>另请参阅
 [多维模型中的数据源视图在](multidimensional-models/data-source-views-in-multidimensional-models.md)[数据源视图中添加或删除表或视图的 &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)


