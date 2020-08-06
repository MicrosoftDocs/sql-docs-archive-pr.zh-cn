---
title: 报表的嵌入数据集和共享数据集（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10420"
ms.assetid: c5852c8a-40e4-424d-a847-64eb151448ff
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 03d442606c72c0037cc45022031c8caca76b64b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579498"
---
# <a name="report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs"></a>报表的嵌入数据集和共享数据集（报表生成器和 SSRS）
  数据集指定要从数据连接使用的数据。 数据集基于已作为嵌入数据源或对报表服务器上共享数据源的引用保存在报表中的数据连接。 数据集包括指定一组字段的查询。 在您将这些字段拖到设计图面上时，将创建在报表运行时对实际数据进行计算的表达式。  
  
 有两种类型的数据集：  
  
-   **共享数据集。** 在报表服务器上定义共享数据集。 您可以浏览到服务器以便创建共享数据集，或选择一个预定义数据集以便添加到您的报表。 使用共享数据集可以提供可由多个报表使用的查询。 共享数据集存储在报表服务器上，并与报表或共享数据源分开管理。 例如，报表服务器管理员可能会更新查询，以便利用改进的索引或其他查询性能优化。  
  
-   **嵌入的数据集。** 只能在嵌入了嵌入数据集的报表中定义和使用嵌入数据集。 当您希望从外部数据源获取将只在一个报表中使用的数据时，使用嵌入数据集。 当您希望创建没有其他依赖项且不需要用于多个报表的查询时，嵌入数据集非常有用。  
  
 数据集还包含参数、筛选器和指定字符区分的数据选项（包括区分大小写、假名类型、宽度、重音以及排序规则信息）。  
  
 ![rs_DatasetStory](../media/rs-datasetstory.gif "rs_DatasetStory")  
  
1.  **“报表数据”窗格中的数据集** 在创建嵌入数据集或添加共享数据集后，会在“报表数据”窗格中出现一个数据集。 数据集基于数据源。  
  
2.  **查询设计器** 当您设计数据集查询时，与数据源类型相关联的查询设计器将打开。  
  
3.  **查询命令** 查询设计器可帮助您生成查询命令。 命令语法由数据访问接口确定。  
  
4.  **数据扩展插件/数据访问接口** 对数据的连接可通过多个数据访问层。  
  
5.  **外部数据源** 检索来自关系数据库、多维数据库、SharePoint 列表、Web 服务或报表模型的数据。  
  
6.  **查询结果** 您可以运行查询并查看示例结果集。 您必须拥有设计时凭据才能运行查询。  
  
7.  **来自架构的元数据** 数据访问接口将架构查询命令与检索数据集字段集合的元数据的查询分开运行。 例如， [!INCLUDE[tsql](../../../includes/tsql-md.md)] `SELECT` 语句返回数据库表的列名称。 使用“报表数据”窗格展开数据集以查看数据集字段集合。  
  
 通过使用预定义的共享数据集和报表部件，也可以将数据包含在报表中。 这些项已具有您所需的数据连接信息。 有关详细信息，请参阅[将数据添加到报表 &#40;报表生成器和 ssrs&#41;](report-datasets-ssrs.md)和[报表部件 &#40;报表生成器和 ssrs&#41;](../report-parts-report-builder-and-ssrs.md)。  
  
 有关内置数据源类型和数据扩展插件的详细信息，请参阅[从外部数据源中添加数据 (SSRS)](add-data-from-external-data-sources-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-report-datasets-and-queries"></a><a name="Overview"></a> 了解报表数据集和查询  
 报表数据集包含在外部数据源上运行并且指定要检索的数据的查询命令。 为了生成该查询命令，您使用与外部数据源的数据扩展插件相关联的查询设计器。 在查询设计器中，您可以运行该查询命令并查看结果集。 该结果集是一个矩形行集，它具有列名以及在每一行中值的数目都相同的行。 不支持层次结构数据（也称作“不规则层次结构”  ）。 列名以数据集字段列表的形式保存在报表定义中。  
  
 在您向报表中添加数据集后，在“报表数据”窗格中将字段从其字段集合拖到表、图表以及用于设计报表布局的其他报表项中。 有关使用字段的详细信息，请参阅 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)。  
  
### <a name="understanding-data-from-a-report-dataset"></a>了解报表数据集数据  
 根据数据扩展插件，报表数据集可以由以下类型的数据组成：  
  
-   来自关系数据库的结果集，它可以是运行数据库命令、存储过程或用户定义函数的结果。 如果通过单个查询检索到多个结果集，则仅处理第一个结果集，并忽略所有其他结果集。 例如，在基于文本的查询设计器中运行以下查询时，只有 `Production.Product` 的结果集出现在结果窗格中：  
  
    ```  
    SELECT ProductID FROM Production.Product  
    GO  
    SELECT ContactID FROM Person.Contact  
    ```  
  
-   来自多维数据源的平展行集，此类数据源使用 XML for Analysis (XMLA) 协议。 某些数据访问接口提供来自数据源的其他单元和维度属性，在结果集中看不到这些属性，但它们会出现在报表中。  
  
-   来自 XML 数据源的平展结果集，此类数据源包括 XML 元素、它们的属性以及它们的子元素。  
  
-   来自任何注册和配置的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 数据访问接口的结果集。  
  
-   来自为特定数据源设计的报表模型的数据，这样的报表模型具有预定义实体、实体关系和字段。 有关详细信息，请参阅 SQL Server 联机丛书[Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312)中的 "将**报表**模型用作数据源"。  
  
 当在运行时处理报表时，查询返回的实际结果集可能有零行或更多行。 在查询中定义的列也有可能已从数据源中丢失。 来自数据源的 Null 值映射到 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 值 `System.DBNull.Value`。  
  
 有关数据集字段的详细信息，请参阅 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)。  
  
### <a name="dataset-query"></a>数据集查询  
 在设计时，当在查询设计器中运行数据集查询时，将看到显示示例数据的来自数据源的行集。 在运行时，当用户查看报表时，数据集查询可能产生不同的值，因为数据源的数据已经更改。 每次处理报表时，都可能出现新数据。  
  
 当您定义每个数据集时，报表生成器将打开与数据源类型相对应的查询设计器，以便帮助您设计查询。 例如，若要为来自 SQL Server 关系数据库的数据定义一个查询，表/矩阵、图表和地图向导将打开一个简单的图形界面来帮助您生成查询，您需要执行的所有工作就是选择您希望位于数据集中的字段。  
  
 在查询设计器中，您可以执行以下操作：  
  
-   在基于图形和基于文本的查询视图之间切换。 使用该图形可以浏览数据源上的架构、表、视图和存储过程。 使用基于文本的视图可以键入、粘贴或查看现有查询，通常用于不能在图形查询设计器中显示的复杂查询。 例如，您可以从 [!INCLUDE[tsql](../../../includes/tsql-md.md)] (.sql) 文件、报表服务器上的其他报表或者文件共享中的报表定义 (.rdl) 文件导入查询。  
  
-   运行查询以查看数据。 查询会返回一个结果集。 结果集中的列将成为数据集字段的集合。 结果中的行将成为数据集数据。 您可以一直对查询进行操作，直到获得所需的列。  
  
-   添加查询参数，以便仅检索报表所需的数据。 查询参数会自动生成匹配的报表参数。 对于报表模型数据源，您指定的筛选器将自动生成一个匹配的报表参数。 用户可以利用报表参数来指定在运行报表时要查看的报表数据。 例如，用户选择其所需数据的产品类别，并且在报表运行时，只有这些产品类别的数据将出现在报表中。  
  
-   从另一个报表导入现有查询。  
  
 查询设计器可以根据数据源类型提供图形模式或文本模式。 如果您选择文本模式，则必须为数据源使用相应的查询语法。  
  
 定义报表数据集时，可以在查询中设置数据属性，也可以接受由数据访问接口设置的默认值。 可以通过使用以下策略之一来更改数据类型：  
  
-   重写数据集查询，以将某字段明确转换为其他数据类型。  
  
-   编辑数据集中的字段，并提供自定义格式。  
  
-   基于数据库字段创建新的自定义字段，并提供自定义格式。  
  
 有关详细信息，请参阅 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)。  
  
### <a name="importing-existing-queries-for-a-dataset"></a>为数据集导入现有查询  
 创建数据集时，可以创建新的查询，也可以从文件或从另一个报表导入现有查询。 从另一个报表导入查询时，可以从此报表内数据集的列表中选择要导入哪个查询。  
  
 仅支持 .sql 和 .rdl 文件类型。 多维表达式 (MDX) 查询、数据挖掘预测 (DMX) 查询和模型查询 (SMQL) 只能由关联的查询设计器生成。  
  
##  <a name="comparing-and-creating-shared-datasets-and-embedded-datasets"></a><a name="Compare"></a> 比较和创建共享数据集和嵌入数据集  
 在报表中或已发布的报表部件中定义嵌入数据集。 对嵌入数据集进行更改将只影响该报表或该报表部件。  
  
 共享数据集在报表服务器或 SharePoint 站点上定义，它基于共享数据源并且可由多个报表和报表部件使用。 对共享数据集定义进行更改将影响使用它的所有报表和所有报表部件。  
  
 在您向报表中添加共享数据集时，数据集字段集合将更新为报表服务器上的当前定义。 在对报表服务器进行更改时，您不会收到更新通知。 若要将字段集合的本地副本与对报表服务器上共享数据集定义的更改保持同步，必须刷新本地字段集合。 有关详细信息，请参阅[在“报表数据”窗格中添加、编辑和刷新字段（报表生成器和 SSRS）](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)。  
  
 已发布的报表项包含它们所依赖的嵌入数据集和共享数据集。 有关详细信息，请参阅 [报表生成器中的报表部件和数据集](report-parts-and-datasets-in-report-builder.md)。  
  
 嵌入数据源和共享数据源的区别在于创建、存储和管理它们的方式不同。 下表总结了嵌入数据源和共享数据源之间的差异：  
  
|说明|嵌入<br /><br /> 数据源|共享<br /><br /> 数据源|  
|-----------------|------------------------------|----------------------------|  
|数据连接嵌入在报表定义中。|![可用](../media/greencheck.gif "可用")||  
|指向报表服务器上的数据连接的指针嵌入在报表定义中。||![可用](../media/greencheck.gif "可用")|  
|在报表服务器上管理|![可用](../media/greencheck.gif "可用")|![可用](../media/greencheck.gif "可用")|  
|对于共享数据集，要求这么做||![可用](../media/greencheck.gif "可用")|  
|对于组件，要求这么做||![可用](../media/greencheck.gif "可用")|  
  
 在报表设计器中，您可以将共享数据集作为报表项目的一部分创建，并且控制是否将这些共享数据集部署到报表服务器。 您不能通过浏览报表服务器来选择某个共享数据集以添加到您的报表中。  
  
 在报表生成器中，您可以执行以下操作：  
  
-   若要创建共享数据集，请使用共享数据集设计视图。 您可以将其保存到报表服务器或 SharePoint 站点上，以便与其他报表共享。 此外，您还可以通过浏览报表服务器来编辑现有的共享数据集。 在此视图中，您可以生成查询和设置所有数据集选项。 有关详细信息，请参阅[共享数据集设计视图（报表生成器）](../report-builder/shared-dataset-design-view-report-builder.md)。  
  
-   若要在报表中添加共享数据集，请在“报表设计”视图中打开报表生成器。 从向导或“报表数据”窗格中，浏览到报表服务器，然后选择要添加到报表的共享数据集。 在此视图中，您除了可以添加字段外，不能更改查询。 您可以覆盖其他数据选项并添加筛选器， 但不能删除筛选器。  
  
 下表将可为报表服务器上共享数据集的定义配置的属性与可为报表定义中共享数据集的实例配置的属性进行了比较。  
  
|properties|有关定义的配置说明|有关实例的配置说明|  
|--------------|--------------------------------------------|------------------------------------------|  
|查询文本|配置查询，包括将查询定义为表达式。|无法更改查询。|  
|查询参数|不能引用报表参数<br /><br /> 包含默认值<br /><br /> 包含只读标志|配置定义中未标记为只读的参数|  
|筛选器|定义筛选器|无法查看或更改作为定义的一部分的数据集筛选器<br /><br /> 可以创建其他筛选器|  
|数据源|必须为共享数据源|无法更改数据源|  
|字段|来自查询命令的字段<br /><br /> 计算字段不是数据集定义的一部分|查看字段，但无法对其进行更改<br /><br /> 字段集合是静态的，它基于您向报表中添加共享数据集时所使用的查询。 若要进行更新，请单击 **“数据集属性”** 对话框中的 **“刷新字段”** 。 实际的字段集合可以是定义中当前查询返回的任何集合。<br /><br /> 添加计算字段|  
|数据集|数据选项，如区分大小写|覆盖实例中的数据选项|  
  
 有关创建数据集的详细信息，请参阅 SQL Server 联机丛书的 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312)中的 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)和 [Reporting Services 工具](../tools/reporting-services-tools.md)。  
  
##  <a name="filtering-sorting-and-grouping-data-in-a-dataset"></a><a name="SortGroupFilter"></a> 对数据集中的数据进行筛选、排序和分组  
 数据集中的数据来自对外部数据源运行查询命令所获得的结果。 数据扩展插件的查询命令语法确定是否可以对数据进行排序或分组。 在为报表检索数据前，在查询中发生排序和分组。 在为报表检索数据后发生筛选。  
  
 有关详细信息，请参阅 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
### <a name="filtering-data-in-a-dataset"></a>筛选数据集中的数据  
 筛选器是报表中数据集定义的一部分。 使用数据集筛选器可以指定数据集中的哪些数据将包含在报表中。 对某一数据集指定筛选器后，基于该数据集的所有数据区域都将只显示经过数据集筛选器筛选后的数据。  
  
 筛选器是共享数据集定义的一部分。 共享数据集筛选器会影响包含共享数据集的所有报表。 在您将共享数据集添加到报表后，或者添加具有相关共享数据集的组件后，可以创建其他数据集筛选器。 您创建的筛选器仅用于您的报表中，它们不是报表服务器上共享数据集定义的一部分。  
  
 可以对数据区域或数据区域组设置附加筛选器。 还可以使用参数和筛选器的组合，使用户能够选择他们要在报表中看到的数据。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
### <a name="sorting-data-in-a-dataset"></a>对数据集中的数据进行排序  
 在数据集中，数据的顺序就是从外部数据源检索数据的顺序。 此顺序就是您在查询设计器中运行查询时看到的顺序。 如果查询命令语法支持排序，则您可以在数据作为报表数据返回前，编辑查询以便对源中的数据进行排序。 例如，对于 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询，ORDER BY 语句控制排序顺序。  
  
 若要在数据返回到报表后对数据进行排序，请对数据区域和数据区域组定义排序表达式。 有关详细信息，请参阅针对特定数据区域类型的主题，例如[表、矩阵和列表（报表生成器和 SSRS）](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
 还可以使用参数和排序表达式的组合，使用户能够选择为报表中的数据选择排序顺序。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
### <a name="grouping-data-in-a-dataset"></a>对数据集中的数据进行分组  
 不能对数据集中的数据进行分组。 若要聚合数据集中的数据，您可以编辑查询命令以便在为报表检索数据前计算聚合。 这些聚合值称为“服务器聚合”  。 在表达式中，若要将这些值标识为预先计算的聚合，请使用聚合函数。 有关详细信息，请参阅 [Aggregate 函数（报表生成器和 SSRS）](../report-design/report-builder-functions-aggregate-function.md)。  
  
##  <a name="using-parameters-and-datasets"></a><a name="Parameters"></a> 使用参数和数据集  
 对于包含查询变量的嵌入数据集查询，可以自动创建查询参数和相应的报表参数。 在报表运行时，报表参数的值将链接到数据集查询参数。 这样，在外部数据源上运行的查询命令将包括为报表参数指定的值。 通过报表参数，用户可以选择他们要在报表中看到的数据。 可以在[“数据集属性”对话框 ->“参数”（报表生成器）](../dataset-properties-dialog-box-parameters-report-builder.md)页中查看查询参数和报表参数的链接方式。  
  
 对于共享数据集，查询参数是可以在独立于报表的报表服务器上管理的共享数据集定义的一部分。 下表描述对查询参数值的支持：  
  
-   可以基于表达式。  
  
-   可以包括默认值。  
  
-   可以设置为只读。 在报表的共享数据集的实例中不能更改只读参数。  
  
-   不能包括对表示报表参数的内置 Parameters 集合的引用。  
  
 若要为共享数据集配置查询参数值，请在数据集设计模式中，浏览到并打开报表服务器中的共享数据集，并且设置[“数据集属性”对话框 ->“参数”（报表生成器）](../dataset-properties-dialog-box-parameters-report-builder.md)页上的选项。 有关详细信息，请参阅 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)。  
  
 对于某些多维数据源，例如 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，可以利用图形查询设计器来指定查询筛选器和选择要用于创建相应查询参数的选项。 在您选择该参数选项时，数据扩展插件将自动创建一个单独的报表数据集，以便为该参数的下拉列表提供可用值。 默认情况下，这些隐藏的数据集不显示在“报表数据”窗格中。  
  
 链接到查询参数的报表参数有助于在从外部数据源返回数据前筛选数据。 您还可以通过创建作为报表定义的一部分的筛选器，对报表中的数据进行筛选。 有关详细信息，请参阅 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)。  
  
### <a name="displaying-hidden-datasets"></a>显示隐藏的数据集  
 为某些多维数据源创建参数化查询时，将自动创建为参数提供有效值的数据集。 在某些查询设计器上，通过指定筛选器然后选择用于创建参数的选项，创建上述数据集。 默认情况下，这些数据集不显示在“报表数据”窗格中，但可以显示它们。 有关详细信息，请参阅[为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS）](show-hidden-datasets-for-parameter-values-multidimensional-data.md)。  
  
##  <a name="using-maps-and-datasets"></a><a name="Maps"></a> 使用地图和数据集  
 如果您在报表中包括地图，则必须提供空间数据。 空间数据可来自报表数据集、地图库中的地图或 ESRI 形状文件。 来自报表或 ESRI 形状文件的空间数据在“报表数据”窗格中不作为数据集出现。 有关详细信息，请参阅[地图（报表生成器和 SSRS）](../report-design/maps-report-builder-and-ssrs.md)。  
  
##  <a name="displaying-data-from-multiple-datasets"></a><a name="Multiple"></a> 显示来自多个数据集的数据  
 报表通常有多个数据集。 下表介绍如何在报表中使用数据集：  
  
-   使用单独的数据区域显示每个数据集中的数据。 有关详细信息，请参阅[数据区域和地图（报表生成器和 SSRS）](../report-design/data-regions-and-maps-report-builder-and-ssrs.md)。  
  
-   可以将多个数据区域链接到一个数据集，并为相同数据提供多个视图。 有关详细信息，请参阅 [将多个数据区域链接到同一数据集（报表生成器和 SSRS）](../report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)。  
  
-   可以使用数据集提供报表参数的可用值或默认值的下拉列表。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
-   通过对钻取报表或子报表使用参数，可以链接多个数据集中的相关数据。 例如，销售报表可以显示所有商店的摘要数据，而钻取链接可以指定商店标识符作为具有以下数据集查询的报表的参数：检索指定商店各销售量的数据集查询。 有关详细信息，请参阅[钻取、向下钻取、子报表和嵌套数据区域（报表生成器和 SSRS）](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)和[子报表（报表生成器和 SSRS）](../report-design/subreports-report-builder-and-ssrs.md)。  
  
-   不能在单个数据区域中显示来自多个数据集的详细信息数据。 但是，可以在一个数据区域中显示多个数据集的聚合或内置函数值。 有关详细信息，请参阅 [聚合函数引用（报表生成器和 SSRS）](../report-design/report-builder-functions-aggregate-functions-reference.md)。 如果需要将来自多个数据集的详细信息数据组合到一个数据区域中，则必须重写查询，以作为单个数据集检索数据。  
  
##  <a name="displaying-a-message-when-no-rows-of-data-are-available"></a><a name="NoRows"></a> 在没有数据行可用时显示消息  
 在报表处理期间，当运行对数据集的查询时，结果集可能不包含任何行。 在呈现的报表中，链接到空数据集的数据区域将显示为空数据区域。 可以指定要在呈现的报表中代替空数据区域的显示文本。 还可以为子报表指定消息，以便如果在运行时对所有数据集的查询没有产生任何数据，则显示该消息。 有关详细信息，请参阅[为数据区域设置“无数据”消息（报表生成器和 SSRS）](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)。  
  
##  <a name="setting-dataset-options"></a><a name="Options"></a> 设置数据集选项  
 对于支持国际数据的数据源，可能需要调整那些影响排序顺序、国际字符属性以及是否区分大小写的数据集属性。 这些属性包括大小写、假名类型、宽度、重音和排序规则。 有关详细信息，请参阅 [SQL Server 联机丛书](https://go.microsoft.com/fwlink/?linkid=98335)中的“数据库和数据库引擎应用程序的国际化注意事项”和“使用排序规则”。 有关如何设置这些属性的详细信息，请参阅[“数据集属性”对话框 ->“选项”（报表生成器）](dataset-properties-dialog-box-options-report-builder.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)  
  
  
