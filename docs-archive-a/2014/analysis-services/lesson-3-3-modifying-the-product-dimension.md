---
title: 修改 "产品" 维度 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 04c0a778a73371dada92c9ff207a17366a2fbc7f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588133"
---
# <a name="modifying-the-product-dimension"></a>修改“产品”维度
  在本主题下的任务中，将使用命名计算为产品系列提供更具说明性的名称，在“产品”维度中定义一个层次结构，并为该层次结构指定“(全部)”成员名称。 还可以按显示文件夹组合各个属性。  
  
## <a name="adding-a-named-calculation"></a>添加命名计算  
 您可以向数据源视图内的表中添加命名计算。 在下面的任务中，将创建一个用来显示产品系列完整名称的命名计算。  
  
#### <a name="to-add-a-named-calculation"></a>添加命名计算  
  
1.  若要打开“Adventure Works DW 2012”**** 数据源视图，请在解决方案资源管理器中的“数据源视图”**** 文件夹中双击“Adventure Works DW 2012”****。  
  
2.  在关系图窗格的底部，右键单击“Product”**** 表标题，然后单击“新建命名计算”****。  
  
3.  在 "**创建命名计算**" 对话框中，在 `ProductLineName` "**列名称**" 框中键入。  
  
4.  在“表达式”**** 框中，键入或复制并粘贴下面的 **CASE** 语句：  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
     此 **CASE** 语句可以为多维数据集内的每个产品系列创建用户友好的名称。  
  
5.  单击 **"确定"** 以创建 `ProductLineName` 命名计算。 您可能需要等待。  
  
6.  在“文件”菜单上，单击“全部保存”。  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>修改某个特性的 NameColumn 属性  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>修改某个特性的 NameColumn 属性值  
  
1.  切换到“产品”维度的维度设计器。 为此，请双击解决方案资源管理器的“维度”**** 节点的“产品”**** 维度。  
  
2.  在“维度结构”**** 选项卡的“属性”**** 窗格中，选择“产品系列”****。  
  
3.  在屏幕右侧的 "属性窗口中，单击窗口底部的**NameColumn**属性字段，然后单击" 浏览 (**...** ") 按钮以打开"**名称列**"对话框。 （可能需要单击屏幕右侧的“属性”**** 选项卡以打开“属性”窗口。）  
  
4.  选择 " `ProductLineName` **源列**" 列表底部，然后单击 **"确定"**。  
  
     “NameColumn”字段现包含 **Product.ProductLineName (WChar)** 文本。 “产品系列”**** 属性层次结构的成员现将显示产品系列的完整名称，而不会显示缩写形式的产品系列名称。  
  
5.  在“维度结构”**** 选项卡的“属性”**** 窗格中，选择“产品密钥”****。  
  
6.  在属性窗口中，单击 " **NameColumn** " 属性字段，然后单击省略号 "浏览 (**...**) " 按钮以打开 "**名称列**" 对话框。  
  
7.  选择“源列”**** 列表中的“EnglishProductName”****，然后单击“确定”****。  
  
     “NameColumn”字段现包含 **Product.EnglishProductName (WChar)** 文本。  
  
8.  在属性窗口中，向上滚动，单击 "**名称**" 属性字段，然后键入 `Product Name` 。  
  
## <a name="creating-a-hierarchy"></a>创建层次结构  
  
#### <a name="to-create-a-hierarchy"></a>创建层次结构  
  
1.  将“产品系列”**** 属性从“属性”**** 窗格拖到“层次结构”**** 窗格中。  
  
2.  将“产品系列”**** 级别下方的“型号名称”**** 属性从“属性”**** 窗格拖到“层次结构”**** 窗格的“\<new level>”**** 单元中。  
  
3.  将 `Product Name` 属性从 "**属性**" 窗格拖到 " **\<new level>** **层次结构**" 窗格中的 "**模型名称**" 级别下的单元。 （您已在先前的章节中将 Product Key 重命名为 Product Name。）  
  
4.  在 "**维度结构**" 选项卡的 "**层次**结构" 窗格中，右键单击 "**层次**结构" 层次结构的标题栏，单击 "**重命名**"，然后键入 `Product Model Lines` 。  
  
     层次结构的名称现在为 `Product Model Lines` 。  
  
5.  在“文件”菜单上，单击“全部保存”。  
  
## <a name="specifying-folder-names-and-all-member-names"></a>指定文件夹名称与“全部”级别成员名称  
  
#### <a name="to-specify-the-folder-and-member-names"></a>指定文件夹名称和成员名称  
  
1.  在“属性”**** 窗格中，按住 Ctrl 键的同时单击下列各个属性，将它们选中：  
  
    -   **类**  
  
    -   **颜色**  
  
    -   **生产天数**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **大小**  
  
    -   **Size Range**  
  
    -   **样式**  
  
    -   **Weight**  
  
2.  在属性窗口的**AttributeHierarchyDisplayFolder**属性字段中，键入 `Stocking` 。  
  
     此时即将这些属性分组放到单独的显示文件夹中。  
  
3.  在“属性”**** 窗格中，选择以下属性：  
  
    -   **经销价格**  
  
    -   **标价**  
  
    -   **标准成本**  
  
4.  在属性窗口的 " **AttributeHierarchyDisplayFolder** " 属性单元中，键入 `Financial` 。  
  
     此时即将这些属性分组放到第二个显示文件夹中。  
  
5.  在“属性”**** 窗格中，选择以下属性：  
  
    -   **结束日期**  
  
    -   **开始日期**  
  
    -   **Status**  
  
6.  在属性窗口的 " **AttributeHierarchyDisplayFolder** " 属性单元中，键入 `History` 。  
  
     此时即将这些属性分组放到第三个显示文件夹中。  
  
7.  `Product Model Lines`在 "**层次结构**" 窗格中选择层次结构，然后将属性窗口中的**AllMemberName**属性更改为 `All Products` 。  
  
8.  单击 "**层次结构**" 窗格的打开区域，然后将属性窗口顶部的 " **AttributeAllMemberName** " 属性更改为 `All Products` 。  
  
     单击空白区域，即可修改“产品”维度自身的属性。 还可以单击“属性”**** 窗格中位于属性列表顶部的“产品”****。  
  
9. 在“文件”菜单上，单击“全部保存”。  
  
## <a name="defining-attribute-relationships"></a>定义属性关系  
 如果基础数据支持，则应定义属性间的属性关系。 定义属性关系可加快维度、分区和查询处理的速度。 有关详细信息，请参阅 [定义属性关系](multidimensional-models/attribute-relationships-define.md) 和 [属性关系](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
#### <a name="to-define-attribute-relationships"></a>定义属性关系  
  
1.  在“产品”维度的“维度设计器”**** 中，单击“属性关系”**** 选项卡。  
  
2.  在关系图中，右键单击“模型名称”**** 属性，然后单击“新建属性关系”****。  
  
3.  在“创建属性关系”对话框中，“源属性”是“型号名称”************。 将“相关属性”设置为“产品系列”********。  
  
     因为各成员之间的关系会随时间变化，所以在“关系类型”列表中，将关系类型设置保留为“柔性”********。 例如，产品型号可能会最终移动到另一个产品系列中。  
  
4.  单击“确定”。  
  
5.  在“文件”菜单上，单击“全部保存”。  
  
## <a name="reviewing-product-dimension-changes"></a>检查“产品”维度更改  
  
#### <a name="to-review-the-product-dimension-changes"></a>检查“产品”维度更改  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“生成”菜单上，单击“部署 Analysis Services 教程”********。  
  
2.  在收到“部署成功完成”**** 消息后，单击“产品”**** 维度的“维度设计器”**** 的“浏览器”**** 选项卡，然后单击设计器工具栏上的“重新连接”按钮。  
  
3.  验证 `Product Model Lines` 是否在 "**层次结构**" 列表中选中，然后展开 `All Products` 。  
  
     请注意，"**全部**" 成员的名称显示为 `All Products` 。 这是因为您已将层次结构的**AllMemberName**属性更改为 `All Products` 前面的课程。 另请注意，“产品系列”**** 级别的成员现在具有用户友好名称，而不是单字母缩写形式。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [修改“日期”维度](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>另请参阅  
 [在数据源视图中定义命名计算 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [创建用户定义的层次结构](multidimensional-models/user-defined-hierarchies-create.md)   
 [配置属性层次结构的“(全部)”级别](multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
