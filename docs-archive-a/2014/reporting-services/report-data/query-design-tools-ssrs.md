---
title: 查询设计工具报表设计器 SQL Server Data Tools (SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb26b23d65c970b927f8edc8fe20c45e3dd23597
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688600"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>SQL Server Data Tools 的报表设计中的查询设计工具 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了各种查询设计工具，您可以使用这些工具在报表设计器中创建数据集查询。 要处理的数据源类型确定了特定查询设计器的可用性。 此外，某些查询设计器还提供了其他模式，以便选择是在可视模式下工作，还是直接在查询语言中工作。 本主题将介绍每种工具及其支持的数据源类型。 本主题将介绍下列工具：

-   [基于文本的查询设计器](#Textbased)

-   [图形查询设计器](#Graphical)

-   [报表模型查询设计器](#Model)

-   [MDX 查询设计器](#MDX)

-   [DMX 查询设计器](#DMX)

-   [SapNetWeaver BI 查询设计器](#SAPBW)

-   [Hyperion Essbase 查询设计器](#Hyperion)

 使用报表服务器项目模板或报表服务器向导项目模板时，所有查询设计工具都在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的数据设计环境中运行。 有关使用查询设计器的详细信息，请参阅 [Reporting Services Query Designers](../reporting-services-query-designers.md)。

##  <a name="text-based-query-designer"></a><a name="Textbased"></a>基于文本的查询设计器
 基于文本的查询设计器是大多数支持的关系数据源的默认查询生成工具，包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Oracle、Teradata、OLE DB、XML 和 ODBC。 与图形查询设计器相比，此查询设计工具无法在查询设计过程中验证查询语法。 下图显示了基于文本的查询设计器。

 ![用于关系数据查询的通用查询设计器](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "用于关系数据查询的通用查询设计器")

 建议使用基于文本的查询设计器创建复杂查询、使用存储过程、查询 XML 数据以及编写动态查询。 根据数据源的不同，可以通过切换工具栏上的“编辑为文本”按钮而在图形查询设计器和基于文本的查询设计器之间进行切换****。 有关详细信息，请参阅 [基于文本的查询设计器用户界面](../text-based-query-designer-user-interface.md)。

##  <a name="graphical-query-designer"></a><a name="Graphical"></a>图形查询设计器
 图形查询设计器用于创建或修改针对关系数据库运行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询。 此查询设计工具用于多种 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 产品和其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 组件中。 此工具支持 Text、StoredProcedure 和 TableDirect 模式，具体取决于数据源类型。 下图显示了图形查询设计器。

 ![用于 SQL 查询的图形查询设计器](../media/rsqd-dsaw-sql.gif "用于 SQL 查询的图形查询设计器")

 可以通过切换工具栏上的“编辑为文本”按钮而在图形查询设计器和基于文本的查询设计器之间进行切换。**** 有关详细信息，请参阅 [Graphical Query Designer User Interface](graphical-query-designer-user-interface.md)。

##  <a name="report-model-query-designer"></a><a name="Model"></a>报表模型查询设计器
 报表模型查询设计器用于创建或修改针对已发布到报表服务器的 SMDL 报表模型运行的查询。 针对模型运行的报表支持点击链接型数据浏览。 查询在运行时确定数据浏览路径。 下图显示了报表模型查询设计器。

 ![语义模型查询设计器 UI](../media/rsqd-dsawmodel-smql.gif "语义模型查询设计器 UI")

 若要使用报表模型查询设计器，必须定义指向已发布模型的数据源。 定义数据源的数据集时，可以在报表模型查询设计器中打开数据集查询。 报表模型查询设计器可在图形模式或基于文本的模式下使用。 可以通过切换工具栏上的“编辑为文本”按钮而在图形查询设计器和基于文本的查询设计器之间进行切换。**** 有关详细信息，请参阅 [Report Model Query Designer User Interface](report-model-query-designer-user-interface.md)。

##  <a name="mdx-query-designer"></a><a name="MDX"></a>MDX 查询设计器
 多维表达式 (MDX) 查询设计器用于创建或修改针对具有多维数据集的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源运行的查询。 下图显示了定义查询和筛选器后的 MDX 查询设计器。

 ![Analysis Services MDX 查询设计器的设计视图](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查询设计器的设计视图")

 若要使用 MDX 查询设计器，必须定义包含可用 Analysis Services 多维数据集的数据源，该多维数据集应是有效的并已经过处理。 为数据源定义数据集时，可以在 MDX 查询设计器中打开查询。 如有必要，请使用工具栏上的 MDX 和 DMX 按钮在 MDX 和 DMX 模式之间进行切换。 有关详细信息，请参阅 [Analysis Services MDX Query Designer User Interface](analysis-services-mdx-query-designer-user-interface.md)。

##  <a name="dmx-query-designer"></a><a name="DMX"></a>DMX 查询设计器
 数据挖掘预测表达式 (DMX) 查询设计器用于创建或修改针对具有挖掘模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源运行的查询。 下图显示了选择模型和输入表后的 DMX 查询设计器。

 ![Analysis Services DMX 查询设计器的设计视图](../media/rsqd-dsawas-dmx-designmode.gif "Analysis Services DMX 查询设计器的设计视图")

 若要使用 DMX 查询设计器，必须定义包含有效数据挖掘模型的可用数据源。 为数据源定义数据集时，可以在 DMX 查询设计器中打开查询。 如有必要，请使用工具栏上的 MDX 和 DMX 按钮在 MDX 和 DMX 模式之间进行切换。 选择模型后，可创建向报表提供数据的数据挖掘预测查询。 有关详细信息，请参阅 [Analysis Services DMX 查询设计器用户界面](analysis-services-dmx-query-designer-user-interface.md)。

##  <a name="sap-netweaver-bi-query-designer"></a><a name="SAPBW"></a>Sap NetWeaver BI 查询设计器
 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 查询设计器用于从 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 数据库中检索数据。 若要使用此查询设计器，必须定义至少包含一个 InfoCube、MultiProvider 或启用了 Web 的查询的 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 数据源。 下图显示了 [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] 查询设计器。

 ![在设计模式下使用 MDX 的查询设计器](../media/rsqd-dssapbw-mdx-designmode.gif "在设计模式下使用 MDX 的查询设计器")

##  <a name="hyperion-essbase-query-designer"></a><a name="Hyperion"></a>Hyperion Essbase 查询设计器
 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 查询设计器用于在 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 数据库和应用程序中检索数据。 下图显示了 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 查询设计器。

 ![用于 Hyperion Essbase 数据源的查询设计器](../media/rsqd-dshyperionessbase-mdx-designmode.gif "用于 Hyperion Essbase 数据源的查询设计器")

 若要使用此查询设计器，必须具有至少包含一个数据库的 [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] 数据源。 有关详细信息，请参阅 [SAP NetWeaver BI Query Designer User Interface](sap-netweaver-bi-query-designer-user-interface.md)。

## <a name="see-also"></a>另请参阅
 [Reporting Services 工具](../tools/reporting-services-tools.md)[将数据添加到报表中 &#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md) [中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) [Reporting Services Tutorials &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md) Reporting Services Reporting Services &#40;&#41;ssrs Reporting Services[支持的数据源](../create-deploy-and-manage-mobile-and-paginated-reports.md)&#40;ssrs&#41;[创建嵌入数据源或共享数据源 &#40;ssrs](../create-an-embedded-or-shared-data-source-ssrs.md)&#41;


