---
title: 教程：脱机生成快速图表报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports, creating
- tutorials, getting started
- creating reports
ms.assetid: 6b1db67a-cf75-494c-b70c-09f1e6a8d414
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 51a9e648550a0108f47e3d93d75267ab0c1c24f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580015"
---
# <a name="tutorial-create-a-quick-chart-report-offline-report-builder"></a>教程：脱机创建快速图表报表（报表生成器）
  在本教程中，将使用向导创建饼图，然后将对其稍作修改以了解都能执行哪些操作。 您可以通过两种不同的方式学习本教程。 这两种方法具有相同的结果：如下图所示的饼图：

 ![“运行”视图中的“我的第一个饼图”](../media/rs-my1stpierunview.gif ""运行" 视图中的第一个饼图")

## <a name="prerequisites"></a>必备条件
 无论您是使用 XML 数据还是 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询，都需要有权访问 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 报表生成器。 可以运行独立版本，也可以运行 ClickOnce 版本（可从报表管理器或 SharePoint 站点获取）。 ClickOnce 版本只有第一步（如何打开报表生成器）不同。 有关详细信息，请参阅[安装、卸载和报表生成器支持](../install-uninstall-and-report-builder-support.md)。

##  <a name="two-ways-to-do-this-tutorial"></a><a name="TwoWays"></a>完成本教程的两种方法

-   [使用 XML 数据创建饼图](#CreatePieChartXML)

-   [使用包含数据的 Transact-SQL 查询创建饼图](#CreatePieQueryData)

### <a name="using-xml-data-for-this-tutorial"></a>使用本教程的 XML 数据
 通过复制本主题中的 XML 数据并粘贴到向导中，可以使用本主题中的 XML 数据。 不需要连接到报表服务器或处于 SharePoint 集成模式下的报表服务器，也不需要访问 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 的实例。

 [使用 XML 数据创建饼图](#CreatePieChartXML)

### <a name="using-a-transact-sql-query-that-contains-data-for-this-tutorial"></a>使用包含本教程数据的 Transact-SQL 查询
 可以复制本主题中包含数据的查询，并将其粘贴到向导中。 将需要 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 实例的名称以及足以对任何数据库进行只读访问的凭据。 本教程中的数据集查询使用文字数据，但必须由 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 实例处理查询以返回报表数据集所必需的元数据。

 使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询的优势在于，其他所有报表生成器教程均使用相同的方法，这样，在您学习其他教程时，您已经提前知道了该做什么。

 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询要求满足一些其他前提条件。 有关详细信息，请参阅[教程先决条件&#40;报表生成器&#41;](../report-builder-tutorials.md)。

 [使用包含数据的 Transact-SQL 查询创建饼图](#CreatePieQueryData)

## <a name="also-in-this-article"></a>本文还介绍了
 [运行向导之后](#AfterWizard)

 [后续操作](#WhatsNext)

##  <a name="creating-the-pie-chart-with-xml-data"></a><a name="CreatePieChartXML"></a>用 XML 数据创建饼图

#### <a name="to-create-the-pie-chart-with-xml-data"></a>用 XML 数据创建饼图

1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。

     此时将显示 "**入门**" 对话框。

    > [!NOTE]
    >  如果未显示 "**入门**" 对话框，请在 "**报表生成器**" 按钮中单击 "**新建**"。

2.  在左窗格中，验证是否选择了 "**报表**"。

3.  在右窗格中，单击 **“图表向导”** ，然后单击 **“创建”** 。

4.  在 **“选择数据集”** 页中，单击 **“创建数据集”** ，然后单击 **“下一步”** 。

5.  在 **“选择数据源的连接”** 页中，单击 **“新建”** 。

     此时将打开 **“数据源属性”** 对话框。

6.  可以将数据源命名为任何名称。 在 **“名称”** 框中，键入 **MyPieChart**。

7.  在 "**选择连接类型**" 框中，单击 " **XML"。**

8.  单击 "**凭据**" 选项卡，选择 "**使用当前 Windows 用户"。可能需要 Kerberos 委托**，然后单击 **"确定"**。

9. 在 **“选择数据源的连接”** 页中，单击 **MyPieChart**，然后单击 **“下一步”** 。

10. 复制以下文本，并将其粘贴到 "**设计查询**" 页中心的大框中。

    ```
    <Query>
    <ElementPath>Root /S  {@Sales (Integer)} /C {@FullName} </ElementPath>
    <XmlData>
    <Root>
    <S Sales="150">
      <C FullName="Jae Pak" />
    </S>
    <S Sales="350">
      <C FullName="Jillian  Carson" />
    </S>
    <S Sales="250">
      <C FullName="Linda C Mitchell" />
    </S>
    <S Sales="500">
      <C FullName="Michael Blythe" />
    </S>
    <S Sales="450">
      <C FullName="Ranjit Varkey" />
    </S>
    </Root>
    </XmlData>
    </Query>
    ```

11. （可选）单击“运行”按钮 (!)，查看要用于图表的数据****。

12. 单击“下一步”。

13. 在 **“选择图表类型”** 页中，单击 **“饼图”**，然后单击 **“下一步”**。

14. 在“排列图表字段”页中，在“可用字段”框中双击“Sales”字段************。

     注意，它将自动移动到 **“值”** 框，因为它是数字值。

15. 将“FullName”字段从“可用字段”框拖到“类别”框（或双击它，它将转到“类别”框），然后单击“下一步”********************。

16. 默认情况下，在 "**选择样式**" 页中选择 "**海运**"。 单击其他样式查看其外观。

17. 单击“完成”。

     现在，将在设计图面上看到新饼图报表。 看到的内容很有代表性。 图例读取 Full Name 1、Full Name 2 等，而不是销售人员的名字，并且饼图切片的大小不准确。 这只用于展示报表的外观。

18. 若要看见实际的饼图，请在功能区的 **“主文件夹”** 选项卡上单击 **“运行”** 。

 ![用于 "返回页首" 链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")[返回页首](#TwoWays)

##  <a name="creating-the-pie-chart-with-a-tsql-query"></a><a name="CreatePieQueryData"></a> 使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询创建饼图

#### <a name="to-create-the-pie-chart-with-a-tsql-query-that-contains-data"></a>使用包含数据的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询创建饼图

1.  单击 **“开始”**，依次指向 **“程序”**、 **Microsoft SQL Server 2012 Report Builder**，再单击 **“报表生成器”**。

2.  在 "**新建报表或数据集**" 对话框中，验证是否已在左窗格中选择 "**报表**"。

3.  在右窗格中，单击 **“图表向导”**，然后单击 **“创建”**。

4.  在 **“选择数据集”** 页中，单击 **“创建数据集”**，然后单击 **“下一步”**。

5.  在 **“选择数据源的连接”** 页中，选择现有数据源或浏览到报表服务器并选择一个数据源，然后单击 **“下一步”**。 您可能需要输入用户名和密码。

    > [!NOTE]
    >  只要您具有足够的权限，则选择哪一个数据源并不重要。 您将不会从数据源中获取数据。 有关详细信息，请参阅[教程先决条件&#40;报表生成器&#41;](../report-builder-tutorials.md)。

6.  在 "**设计查询**" 页上，单击 "**编辑为文本**"。

7.  将以下查询粘贴到查询窗格中：

    ```
    SELECT 150 AS Sales, 'Jae Pak' AS FullName 
    UNION SELECT 350 AS Sales, 'Jillian Carson' AS FullName 
    UNION SELECT 250 AS Sales, 'Linda C Mitchell' AS FullName 
    UNION SELECT 500 AS Sales, 'Michael Blythe' AS FullName 
    UNION SELECT 450 AS Sales, 'Ranjit Varkey' AS FullName 
    ```

8.  （可选）单击“运行”按钮 (!)，查看要用于图表的数据****。

9. 单击“下一步”。

10. 在 **“选择图表类型”** 页中，单击 **“饼图”**，然后单击 **“下一步”**。

11. 在“排列图表字段”页中，在“可用字段”框中双击“Sales”字段************。

     注意，它将自动移动到 **“值”** 框，因为它是数字值。

12. 将“FullName”字段从“可用字段”框拖到“类别”框（或双击它，它将转到“类别”框），然后单击“下一步”********************。

13. 在 **“选择样式”** 页中，默认情况下“海洋”为选中状态。 单击其他样式查看其外观。

14. 单击“完成”。

     现在，将在设计图面上看到新饼图报表。 看到的内容很有代表性。 图例读取 Full Name 1、Full Name 2 等，而不是销售人员的名字，并且饼图切片的大小不准确。 这只用于展示报表的外观。

15. 若要看见实际的饼图，请在功能区的 **“主文件夹”** 选项卡上单击 **“运行”** 。

 ![用于 "返回页首" 链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")[返回页首](#TwoWays)

##  <a name="after-you-run-the-wizard"></a><a name="AfterWizard"></a> 运行向导之后
 现在您便拥有了饼图报表，从而可以对其进行操作。 在功能区的 **“运行”** 选项卡上，单击 **“设计”**，这样可以继续修改它。

### <a name="make-the-chart-bigger"></a>放大图表
 您可能希望放大饼图。 单击图表（但不要单击图表中的任何元素）以选择它，并拖动右下角以调整它的大小。

### <a name="add-a-report-title"></a>添加报表标题
 选择图表顶部的词语 **“图表标题”** ，然后键入标题，例如 **Sales Pie Chart**。

### <a name="add-percentages"></a>添加百分比

##### <a name="to-display-percentage-values-as-labels-on-a-pie-chart"></a>在饼图上显示百分比值

1.  右键单击饼图并选择 "**显示数据标签**"。 数据标签应显示在饼图上的每个切片上。

2.  右键单击标签并选择 "**序列标签属性**"。 此时将显示 **“序列标签属性”** 对话框。

3.  `#PERCENT{P0}`"**标签数据**" 选项的类型。

     `{P0}` 提供没有小数位的百分比。 如果只是键入 `#PERCENT`，则数字将有两位小数。 `#PERCENT` 是执行计算或函数的关键字，还有很多这样的关键字。

 有关自定义饼图标签和图例的详细信息，请参阅[在饼图上显示百分比值&#40;报表生成器和 SSRS&#41;](../report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md) 和 [更改图例项文本&#40;报表生成器和 SSRS&#41;](../report-design/chart-legend-change-item-text-report-builder.md)。

 ![用于 "返回页首" 链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")[返回页首](#TwoWays)

##  <a name="whats-next"></a><a name="WhatsNext"></a>下一步是什么？
 现在，你已在报表生成器中创建了第一个报表，接下来可以尝试其他教程并开始从你自己的数据创建报表。 若要运行报表生成器，你需要有权使用*连接字符串*访问数据源（如数据库），这会将你实际连接到数据源。 系统管理员拥有此信息，并且可以为您设置相应的权限。

 若要完成其他教程，需要 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 实例的名称以及足以对任何数据库进行只读访问的凭据。 系统管理员也可以为您设置该权限。

 最后，若要将报表保存到报表服务器或与报表服务器集成的 SharePoint 站点，需要具有 URL 和相应权限。 可以直接从您的计算机运行您创建的任何报表，但如果从报表服务器或 SharePoint 站点运行报表，则报表会有更多功能。 您需要有一定权限才能运行您的报表或报表服务器或 SharePoint 站点上发布的其他报表。 请与系统管理员联系以获取访问权限。

 在入门之前，可能有必要了解一些概念和术语。 有关详细信息，请参阅[报表创作概念 &#40;报表生成器和 SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)。 而且，在创建第一个报表之前，应当花一些时间进行规划。 这将需要较长时间。 有关详细信息，请参阅[规划报表 &#40;报表生成器&#41;](../report-design/planning-a-report-report-builder.md)。

 ![用于 "返回页首" 链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标")[返回页首](#TwoWays)

## <a name="see-also"></a>另请参阅
 [SQL Server 2014 中](report-builder-in-sql-server-2016.md)[报表生成器&#41;报表生成器教程 &#40;](../report-builder-tutorials.md)


