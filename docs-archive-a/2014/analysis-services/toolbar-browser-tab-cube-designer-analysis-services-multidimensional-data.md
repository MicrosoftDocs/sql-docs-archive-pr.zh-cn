---
title: 工具栏 (浏览器选项卡，多维数据集设计器)  (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
author: minewiskan
ms.author: owend
ms.openlocfilehash: cba90d60a9ec3b3651c4889be423a5c1311fc9c1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688275"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>工具栏（“浏览器”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  在设计或浏览多维数据集或其对象或在创建 MDX 查询期间，使用多维数据集设计器的 **“工具栏”** 中的功能可以执行常规操作。 在设计时和查询视图中均可执行的操作包括设置用户上下文、处理对象以及设置默认语言。

 下表列出了 **“工具栏”** 按钮及其功能。

|Button|描述|
|------------|-----------------|
|**编辑为文本**|不可用于此数据源类型。|
|**导入**|从文件系统中的报表定义 (.rdl) 文件导入现有查询。|
|![更改为 MDX 查询视图](media/rsqdicon-commandtypemdx.gif "更改为 MDX 查询视图")|切换到命令类型 MDX。|
|![刷新结果数据](media/rsqdicon-refresh.gif "刷新结果数据")|刷新数据源的元数据。|
|![添加计算成员](media/rsqdicon-addcalculatedmember.gif "添加计算成员")|显示 **“计算成员生成器”** 对话框。|
|![切换显示空单元](media/rsqdicon-showemptycells.gif "切换为显示空单元格")|在“数据”窗格中的显示或不显示空单元格之间切换。 （这等同于在 MDX 中使用 NON EMPTY 子句）。|
|![自动执行查询](media/rsqdicon-autoexecute.gif "自动执行查询")|在每次进行更改时自动运行查询并显示结果。 结果将显示在“数据”窗格中。|
|![“显示聚合”按钮](media/rsqdicon-showaggregations.gif "“显示聚合”按钮")|在“数据”窗格中显示聚合。|
|![删除](media/rsqdicon-delete.gif "删除")|通过查询在“数据”窗格中删除选定列。|
|![“查询参数”对话框图标](media/iconqueryparameter.gif "“查询参数”对话框图标")|显示 **“查询参数”** 对话框。 指定查询参数的值时，会自动创建一个同名参数。|
|![“准备查询”按钮](media/rsqdicon-preparequery.gif "“准备查询”按钮")|准备查询。|
|![运行查询](media/rsqdicon-run.gif "运行查询")|运行查询并在“数据”窗格中显示结果。|
|![取消查询](media/rsqdicon-cancel.gif "取消查询")|取消查询。|
|![切换到设计模式](media/rsqdicon-designmode.gif "切换到设计模式")|在设计模式和查询模式之间切换。|

 通常，工具栏按钮在 **“设计模式”** 和 **“查询模式”** 下是相同的； 但是下列按钮在查询模式下不可用：

-   **编辑为文本**

-   **添加计算成员**（![添加计算成员](media/rsqdicon-addcalculatedmember.gif "添加计算成员")）

-   **显示空单元格**（![切换为显示空单元格](media/rsqdicon-showemptycells.gif "切换为显示空单元格")）

-   **自动执行**（![自动执行查询](media/rsqdicon-autoexecute.gif "自动执行查询")）

-   **显示聚合**![“显示聚合”按钮](media/rsqdicon-showaggregations.gif "“显示聚合”按钮")

## <a name="options"></a>选项

|选项|描述|
|------------|-----------------|
|**Process**|单击此项可显示 **“处理”** 对话框，并处理多维数据集。 有关“处理”**** 对话框的详细信息，请参阅[处理对话框（Analysis Services - 多维数据）](process-dialog-box-analysis-services-multidimensional-data.md)。|
|**更改用户**|单击此选项可显示 "**安全上下文**" 对话框，并更改 "**浏览器**" 选项卡上使用的用户和角色。有关 "**安全上下文**" 对话框的详细信息，请参阅 "[安全上下文" 对话框 &#40;Analysis Services 多维数据&#41;](security-context-dialog-box-analysis-services-multidimensional-data.md)。|
|**重新连接**|如果 **“浏览器”** 选项卡会话由于连接丢失或超时而断开，单击此项可将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] “计算” **选项卡重新连接到包含多维数据集的** 实例和数据库。|
|**“刷新”**|单击此项可以刷新 **“元数据”** 和 **“报表”** 窗格。|
|**升序排序**|单击此项可以按 **“语言”** 中指定语言的升序顺序，对 **“报表”** 窗格中的所选行的同级成员进行排序。<br /><br /> **注意**仅当选择了 "**报表**" 窗格中的单元时，才会启用此选项。|
|**降序排序**|单击此项可以按 **“语言”** 中指定语言的降序顺序，对 **“报表”** 窗格中的所选行的同级成员进行排序。<br /><br /> 注意：只有在“报表”窗格中选择了单元时，才会启用此选项。 ****|
|**自动筛选**|单击此项可以自动筛选 **“结果”** 窗格中的结果。|
|**仅显示顶部/底部**|选择一个值或百分比，基于所选度量值在 **“报表”** 窗格中只显示最前面或最后面指定数量或百分比的单元。<br /><br /> 有关此选项的详细信息，请参阅 [TopCount (MDX)](/sql/mdx/topcount-mdx)、[TopPercent (MDX)](/sql/mdx/toppercent-mdx)、[BottomCount (MDX)](/sql/mdx/bottomcount-mdx) 和 [BottomPercent (MDX)](/sql/mdx/bottompercent-mdx)。|
|**进行**|单击此项可以显示小计。|
|**所有项总计**|单击此项可以在 **“报表”** 窗格中显示所有成员的总计。|
|**显示空单元**|单击此项可以在 **“报表”** 窗格中显示空单元。|
|**清除结果**|单击此项可以清除 **“报表”** 窗格中的结果。|
|**命令和选项**|单击此项可以显示 **“命令和选项”** 对话框，并编辑 **“报表”** 窗格中 Microsoft Office 11.0 数据透视表控件的高级属性。 有关 **“命令和选项”** 对话框的详细信息，请参阅 Microsoft Office 文档。|
|**透视**|选择用于在 **“元数据”** 和 **“报表”** 窗格中查看数据和元数据的透视。<br /><br /> 若要在不使用透视的情况下查看多维数据集，请选择多维数据集名称。|
|**语言**|选择用于在 **“元数据”** 和 **“报表”** 窗格中查看数据和元数据的语言。<br /><br /> 若要使用默认语言查看多维数据集，请选择 **“默认值”**。|


