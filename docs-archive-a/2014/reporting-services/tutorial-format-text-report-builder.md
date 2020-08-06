---
title: 教程：设置文本格式（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c96b500f8aa30b77c78f75ccd1342398fd44eb2c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692214"
---
# <a name="tutorial-format-text-report-builder"></a>教程：设置文本格式（报表生成器）
  在本教程中，您可以练习以不同方式设置文本格式。 在设置了具有数据源和数据集的空白报表后，您可以选择要完成的步骤。  
  
 下图显示与您将创建的报表类似的报表。  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 在一个步骤中，您可以故意犯某个错误，以便可以了解错误的成因。 然后，您可以纠正该错误以便实现预期效果。  
  
 您在本教程中创建的报表的增强版本可用作示例 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 报表生成器报表。 有关下载此示例报表和其他内容的详细信息，请参阅[报表生成器示例报表](https://go.microsoft.com/fwlink/?LinkId=184851)。  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>你将学习的内容  
  
### <a name="set-up-the-report"></a>设置报表  
 1. [创建具有数据源和数据集的空白报表](#CreateReport)  
  
 2. [向报表设计图面添加字段（故意犯错，然后纠正）](#AddField)  
  
 3. [向报表添加表 Design Surface](#AddTable)  
  
### <a name="pick-and-choose"></a>选取和选择  
 [向报表添加超链接](#AddHyperlink)  
  
 [旋转报表中的文本](#RotateText)  
  
 [用 HTML 格式显示文本](#FormatHTML)  
  
 [设置货币格式](#FormatCurrency)  
  
 [保存报表](#Save)  
  
 完成本教程的预计学时：20 分钟。  
  
## <a name="requirements"></a>要求  
 有关要求的详细信息，请参阅[教程先决条件（报表生成器）](../reporting-services/report-builder-tutorials.md)。  
  
##  <a name="create-a-blank-report-with-a-data-source-and-dataset"></a><a name="CreateReport"></a>创建具有数据源和数据集的空白报表  
  
#### <a name="to-create-a-blank-report"></a>创建空白报表  
  
1.  单击 "**开始**"，指向 "**程序**"，指向 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] "**报表生成器**"，然后单击 "**报表生成器**"。  
  
    > [!NOTE]  
    >  此时应显示 **“入门”** 对话框。 如果未显示该对话框，则从“报表生成器”按钮，单击 **“新建”**。  
  
2.  在 **“入门”** 对话框的左窗格中，确保已选择 **“新建报表”** 。  
  
3.  在右窗格中，单击 **“空白报表”**。  
  
#### <a name="to-create-a-data-source"></a>创建数据源  
  
1.  在 "报表数据" 窗格中，单击 "**新建**"，然后单击 "**数据源**"。  
  
2.  在“名称”框中，键入：TextDataSource********  
  
3.  单击 **“使用我的报表中嵌入的连接”**。  
  
4.  验证连接类型是否为 "Microsoft SQL Server"，然后在 "**连接字符串**" 框中键入： **Data \<servername> Source =**  
  
    > [!NOTE]  
    >  表达式 \<servername>（例如 Report001）指定安装了 SQL Server 数据库引擎实例的计算机。 本教程不需要具体数据；只需要与 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 数据库的连接。 如果你已经具有在“数据源连接”**** 下列出的某一数据源连接，则可以选择该连接并且转到下一过程“创建数据集”。 有关详细信息，请参阅[获取数据连接的备选方式（报表生成器）](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md)。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>创建数据集  
  
1.  在 "报表数据" 窗格中，单击 "**新建**"，然后单击 "**数据集**"。  
  
2.  确保数据源为 **TextDataSource**。  
  
3.  在“名称”框中，键入：TextDataset********。  
  
4.  确保已选择 **“文本”** 查询类型，然后单击 **“查询设计器”**。  
  
5.  单击 **“编辑为文本”**。  
  
6.  将以下查询粘贴到查询窗格中：  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  单击“运行” (**!**) 以运行查询。  
  
     查询结果将是可用于在您的报表中显示的数据。  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="add-a-field-to-the-report-design-surface"></a><a name="AddField"></a>向报表添加字段 Design Surface  
 如果您希望来自您的数据集的字段出现在报表中，则第一感可能是要将其直接拖到设计图面。 本练习指出为什么无法这样做以及相应替代步骤。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>向报表添加字段（获得错误结果）  
  
1.  将 **FullName** 字段从“报表数据”窗格中拖到设计图面中。  
  
     报表生成器将创建一个文本框，文本框中有一个表达式，该表达式表示为 \<Expr>。  
  
2.  单击 **“运行”** 。  
  
     请注意，只有一条记录**Fernando Ross**，它按字母顺序排列查询中的第一条记录。 该字段并不重复以便显示该字段中的其他记录。  
  
3.  单击 **“设计”** 返回设计视图。  
  
4.  在文本框中选择表达式 \<Expr> 。  
  
5.  在“属性”窗格中，对于“值”属性，将看到以下内容（如果没有看到“属性”窗格，则在“视图”选项卡上，选中“属性”）************：  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     `First` 函数设计为只检索字段中的第一个值，这就是您所看到的内容。  
  
     将该字段直接拖到设计图面上创建了一个文本框。 文本框本身并非数据区域，因此它们不显示来自报表数据集的数据。 数据区域（例如表、矩阵和列表）中的文本框显示数据。  
  
6.  选择文本框（如果您已经选择了表达式，则按下 Esc 以便选择该文本框），然后按 Delete 键。  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>向报表添加字段（获得正确结果）  
  
1.  在功能区的“插入”选项卡的“数据区域”区域中，单击“列表”************。 单击设计图面，然后拖动以便创建一个框，该框大约两英寸宽、一英寸高。  
  
2.  将 **FullName** 字段从“报表数据”窗格中拖到列表框中。  
  
     此时，报表生成器将创建一个文本框，表达式 `[FullName]` 将位于该文本框中。  
  
3.  单击 **“运行”** 。  
  
     请注意，此时该框将重复以便显示查询中的所有记录。  
  
4.  单击 **“设计”** 返回设计视图。  
  
5.  在文本框中选择该表达式。  
  
6.  在“属性”窗格中，对于“值”属性，将看到以下内容****：  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     通过将文本框拖到列表数据区域，将显示处于数据集中的数据。  
  
7.  选择列表框并按 Delete 键。  
  
##  <a name="add-a-table-to-the-report-design-surface"></a><a name="AddTable"></a>向报表添加表 Design Surface  
 创建此表，以便您可以在其中放置超链接和旋转后的文本。  
  
#### <a name="to-add-a-table-to-the-report"></a>将表添加到报表中  
  
1.  在 "**插入**" 菜单上，单击 "**表**"，然后单击 "**表向导**"。  
  
2.  在 "新建表或矩阵" 向导的 "**选择数据集**" 页上，单击 "**选择此报表中的现有数据集或共享数据**集"，然后单击 " **TextDataset () 此报表**"，然后单击 "**下一步**"。  
  
3.  在 "**排列字段**" 页上，将 "**区域**"、" **externallink><maml linktext>**" 和 "**产品**" 字段拖到 "**行组**"，将 " **Sales** " 字段拖到 "**值**" 中，**然后单击 "**  
  
4.  在 "**选择布局**" 页上，清除 "**展开/折叠组**" 复选框，以便可以看到整个表，然后单击 "**下一步**"。  
  
5.  在 "**选择样式**" 页上，单击 "**石板**"，然后单击 "**完成**"。  
  
6.  拖动该表以便该表位于标题块之下。  
  
7.  单击 **“运行”** 。  
  
     该表看起来没问题，但具有两个总计行。 **Externallink><maml linktext>** 字段不需要总计行。  
  
8.  单击 **“设计”** 返回设计视图。  
  
9. 右键单击包含的文本框 `[LinkText]` ，然后单击 "**拆分单元**"。  
  
10. 选择该单元格下方的空单元格 `[LinkText]` ，然后按住 SHIFT 键并选择其右侧的两个单元： " **Product** " 列中的 "**合计**" 单元和 " `[Sum(Sales)]` **销售**" 列中的单元格。  
  
11. 选定这三个单元后，右键单击其中一个单元格，然后单击 "**删除行**"。  
  
12. 单击 **“运行”** 。  
  
##  <a name="add-a-hyperlink-to-the-report"></a><a name="AddHyperlink"></a>向报表添加超链接  
 在本节中，您将向前一节中的表中的文本添加超链接。  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>向报表添加超链接  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  右键单击包含 `[LinkText]` 的单元格，然后单击“文本框属性”****。  
  
3.  在 "**文本框属性**" 框中，单击 "**操作**"。  
  
4.  单击 "**前往 URL**"。  
  
5.  在 "**选择 url** " 框中，单击 " **url**"，然后单击 **"确定"**。  
  
6.  请注意，文本在外观上看不出任何区别。 您需要使其看起来像链接文本。  
  
7.  选择 `[LinkText]`。  
  
8.  在 "**主页**" 选项卡的 "**字体**" 部分中，单击 "**下划线**" 按钮，然后单击 "**颜色**" 按钮旁的下拉箭头，然后单击 "**蓝色**"。  
  
9. 单击 **“运行”** 。  
  
     文本现在看起来像链接了。  
  
10. 单击某一链接。 如果计算机已连接到 Internet，则浏览器将打开到报表生成器的帮助主题。  
  
##  <a name="rotate-text-in-the-report"></a><a name="RotateText"></a>旋转报表中的文本  
 在本节中，您将旋转前一节的表中的某些文本。  
  
#### <a name="to-rotate-text"></a>旋转文本  
  
1.  单击 **“设计”** 返回设计视图。  
  
2.  单击包含 的单元格。 `[Territory].`  
  
3.  在“开始”**** 选项卡上的“字体”**** 部分中，单击“加粗”**** 按钮。  
  
4.  如果“属性”窗格未打开，请在“视图”选项卡上选中“属性”复选框********。  
  
5.  在 "属性" 窗格中找到 "WritingMode" 属性。  
  
    > [!NOTE]  
    >  对“属性”窗格中的属性进行分类时，WritingMode 位于“本地化”类别中****。 请确保您选择的是单元，而非文本。 WritingMode 是文本框的属性，而非文本的属性。  
  
6.  在列表框中，单击 " **Rotate270**"。  
  
7.  在 "**主页**" 选项卡上的 "**段落**" 部分中，单击**中间**和中间按钮，以在单元格的中间**垂直和水平**位置查找文本。  
  
8.  单击“运行”(**!**)。  
  
 现在， `[Territory]` 单元中的文本将从单元的底部到顶部垂直放置。  
  
##  <a name="displaying-text-with-html-formatting"></a><a name="FormatHTML"></a>用 HTML 格式显示文本  
  
#### <a name="to-display-text-formatted-as-html"></a>以 HTML 格式显示文本  
  
1.  单击 "**设计**" 切换到 "设计" 视图。  
  
2.  在“插入”选项卡上，单击“文本框”，然后在设计图面上，单击并拖动以便在表的下方创建一个宽度为四英寸、高度为三英寸的文本框********。  
  
3.  复制此文本并将其粘贴到文本框中：  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  选择文本框中的所有文本。  
  
     这是文本的属性，而非文本框的属性，因此，在一个文本框中，你可以混用纯文本和使用 HTML 标记作为样式的文本。  
  
5.  右键单击所有选定文本，然后单击“文本属性”****。  
  
6.  在 "**常规**" 页上的 "**标记类型**" 下，单击 " **Html-将 html 标记解释为样式**"。  
  
7.  单击“确定”  。  
  
8.  单击“运行” (**!**) 以预览报表。  
  
 文本框中的文本将显示为标题、段落和带项目符号的列表。  
  
##  <a name="format-currency"></a><a name="FormatCurrency"></a>设置货币格式  
  
#### <a name="to-format-numbers-as-currency"></a>将数字设为货币格式  
  
1.  单击 "**设计**" 切换到 "设计" 视图。  
  
2.  单击包含 `[Sum(Sales)]`的顶部表单元，按住 Shift 键，然后单击包含 `[Sum(Sales)]`的底部表单元。  
  
3.  在“开始”选项卡上的“数字”组中，单击“货币”按钮************。  
  
4.   (可选) 在 "**主页**" 选项卡上的 "**数字**" 组中，单击 "**占位符样式**" 按钮，然后单击 "**示例值**" 以查看数字的格式设置。  
  
5.  （可选）在“开始”选项卡上的“数字”组中，单击两次“减少小数位数”按钮，显示不带美分的美元数字************。  
  
6.  单击“运行” (**!**) 以预览报表。  
  
 报表现在将显示设置了格式的数据并且更易于阅读。  
  
##  <a name="save-the-report"></a><a name="Save"></a>保存报表  
 您可以将报表保存到报表服务器、SharePoint 库或本地计算机。  
  
 在本教程中，将报表保存到报表服务器。 如果您没有对报表服务器的访问权限，则可以保存到您的计算机。  
  
#### <a name="to-save-the-report-on-a-report-server"></a>将报表保存到报表服务器  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“最近使用的站点和服务器”**。  
  
3.  选择或键入您拥有保存报表权限的报表服务器的名称。  
  
     此时将显示“正在连接到报表服务器”消息。 当连接完成时，您将看到报表服务器管理员指定为报表默认位置的报表文件夹的内容。  
  
4.  在“名称”中，用选择的名称替换默认名称****。  
  
5.  单击“ **保存**”。  
  
 报表即已保存至报表服务器。 您连接的报表服务器的名称将显示在窗口底部的状态栏中。  
  
#### <a name="to-save-the-report-on-your-computer"></a>将报表保存到计算机上  
  
1.  从 **“报表生成器”** 按钮，单击 **“另存为”**。  
  
2.  单击 **“桌面”**、 **“我的文档”** 或 **“我的电脑”**，然后浏览到要将报表保存到的文件夹。  
  
3.  在“名称”中，用选择的名称替换默认名称****。  
  
4.  单击“ **保存**”。  
  
## <a name="next-steps"></a>后续步骤  
 可以通过多种方式设置文本格式报表生成器[教程：创建自由格式的报表 &#40;报表生成器&#41;](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md)包含更多示例。  
  
## <a name="see-also"></a>另请参阅  
 [教程 &#40;报表生成器&#41;](report-builder-tutorials.md)   
 [&#40;报表生成器和 SSRS 的格式设置报表项&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
