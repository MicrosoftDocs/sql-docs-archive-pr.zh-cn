---
title: 向表或矩阵添加交互式排序（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10121"
- sql12.rtp.rptdesigner.textboxproperties.intrctvsort.f1
ms.assetid: 05819637-729b-4cf6-82de-91a99f184ec6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c0c453a8ea338ab9a09d7552c064f2eb85add985
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692731"
---
# <a name="add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs"></a>向表或矩阵添加交互式排序（报表生成器和 SSRS）
  添加交互式排序按钮可以让用户能够更改表和矩阵中行和列的排序顺序。 只有支持用户交互的呈现格式（例如 HTML）才支持此功能。  
  
 创建交互式排序按钮时，必须指定要排序的对象、排序依据以及要应用排序的作用域。 例如，可以按客户姓氏对详细信息行进行排序，按销售额对类别组中的子类别组值进行排序，或者按总计对类别和子类别组值的组合进行排序。  
  
 查看报表时，支持交互式排序的列带有箭头图标，图标可以更改来指示排序顺序。 第一次单击交互式排序按钮时，将按升序对项进行排序。 随后单击则会在升序和降序之间切换排序顺序。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="in-this-article"></a><a name="BackToTop"></a> 本文内容  
 [对不具有组的表的详细信息行进行排序](#SortingDetailRows)  
  
 [对表或矩阵的顶级父行组进行排序](#SortingTopLevelParent)  
  
 [对组的子组或详细信息行进行排序](#SortingChildGroups)  
  
 [基于复杂组表达式对行进行排序](#SortingMultipleRowGroups)  
  
 [同步多个数据区域的排序顺序](#SynchronizingSortOrder)  
  
##  <a name="sorting-detail-rows-for-a-table-with-no-groups"></a><a name="SortingDetailRows"></a> 对不具有组的表的详细信息行进行排序  
 将交互式排序按钮添加到列标题，可使用户能够单击列标题并按该列中显示的值对表中的详细信息行进行排序。  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-the-table-by-value"></a>将交互式排序按钮添加到列标题以按值对表进行排序  
  
1.  在报表设计视图内不具有组的表中，右键单击要向其添加交互式排序按钮的列标题中的文本框，再单击“文本框属性”  。  
  
2.  单击 **“交互式排序”** 。  
  
3.  选择 **“对此文本框启用交互式排序”** 。  
  
4.  在 **“选择排序对象”** 中，单击 **“详细信息行”** 。  
  
5.  在 **“排序依据”** 中，指定排序表达式。 从下拉列表中，选择与要为其定义排序操作的列对应的字段（例如，对名为“Title”的列标题，选择 `[Title]`）。 需要指定排序表达式。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  对要向其添加交互式排序按钮的每一列重复步骤 1-6。  
  
 若要验证排序操作，请单击 **“运行”** 以预览报表，然后单击交互式排序按钮。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="sorting-a-top-level-parent-row-group-for-a-table-or-matrix"></a><a name="SortingTopLevelParent"></a> 对表或矩阵的顶级父行组进行排序  
 将交互式排序按钮添加到列标题，可使用户能够单击列标题并按该列中显示的值对表或矩阵中的父组行进行排序。 子组的顺序保持不变。  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-groups"></a>将交互式排序按钮添加到列标题以对组进行排序  
  
1.  在报表设计视图内的表或矩阵中，右键单击要向其添加交互式排序按钮的组的列标题中的文本框，再单击“文本框属性”  。  
  
2.  单击 **“交互式排序”** 。  
  
3.  选择 **“对此文本框启用交互式排序”** 。  
  
4.  在 **“选择排序对象”** 中，单击 **“组”** 。  
  
5.  从下拉列表中，选择要排序的组的名称。 对于基于简单组表达式的组，将用组表达式填充 **“排序依据”** 值。  
  
    > [!NOTE]  
    >  对于复杂组表达式，请将“排序依据”表达式手动设置为与组表达式相同的值  。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 若要验证排序操作，请单击 **“运行”** 以预览报表，然后单击交互式排序按钮。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="sorting-child-groups-or-detail-rows-for-a-group"></a><a name="SortingChildGroups"></a> 对组的子组或详细信息行进行排序  
 将交互式排序按钮添加到组头行，可使用户能够对父组中的子组的值进行排序，或者对最内部的子组的详细信息行进行排序。  
  
#### <a name="to-add-an-interactive-sort-button-to-a-text-box-in-a-group-row-header-to-sort-child-groups-or-detail-rows"></a>将交互式排序按钮添加到组行标题中的文本框以对子组或详细信息行进行排序  
  
1.  在报表设计视图中，右键单击要向其添加交互式排序按钮的组头行中的文本框，然后单击“文本框属性”  。  
  
2.  单击 **“交互式排序”** 。  
  
3.  选择 **“对此文本框启用交互式排序”** 。  
  
4.  在 **“选择排序对象”** 中，单击下列某个选项：  
  
    -   **详细信息** ：单击 **“详细信息”** 以对详细信息行进行排序。 从下拉列表中，选择要按其排序的字段。 对于此选项，必须指定要按其排序的值。  
  
    -   **组** ：单击 **“组”** 以对子组值进行排序。 对于此选项，将从组表达式自动填充 **“排序依据”** 表达式。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 若要验证排序操作，请单击 **“运行”** 以预览报表，然后单击交互式排序按钮。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="sorting-rows-based-on-a-complex-group-expression"></a><a name="SortingMultipleRowGroups"></a> 基于复杂组表达式对行进行排序  
 将交互式排序按钮添加到列标题，可使用户能够单击列标题并对组合的父组和子组进行排序。 若要获得此效果，必须将组表达式更改为两个组的组合。 例如，假定用一个矩阵显示某个商店中按颜色和大小分组的商品的库存总计。 若要基于颜色和大小的组合对行进行排序，而不是让颜色和大小各有单独的组，则可以基于颜色和大小的组合来定义组。 有关定义组表达式的详细信息，请参阅[组表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)。  
  
 在下面的过程中，术语指定 Tablix 数据区域。 有关详细信息，请参阅 [Tablix 数据区域（报表生成器和 SSRS）](tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
 通常，基于多个组对行进行排序时，希望看到排序行的总计，而不考虑列组。 在此过程中，不使用任何列组。 开始将添加矩阵并删除默认列组。 另外，开始也可以添加表并删除详细信息组。  
  
#### <a name="to-add-an-interactive-sort-button-to-a-column-header-to-sort-multiple-groups"></a>将交互式排序按钮添加到列标题以对多个组进行排序  
  
1.  在报表设计视图中，添加一个矩阵。  
  
2.  将数值字段拖到数据单元，以将数据集链接到该矩阵。  
  
     接下来，您将需要用指定多个字段的组表达式创建组，并创建一个组头以用来显示组值。  
  
3.  确认在设计图面上已选择该矩阵。 “分组”窗格将显示默认的行和列组。  
  
4.  在“行组”窗格中，右键单击默认行组，再单击“编辑组”  。 此时将打开 **“组属性”** 对话框。  
  
5.  在 **“名称”** 中，用一个名称替换默认名称，该名称应指定要按其分组的多个组。  
  
6.  在“组表达式”的“分组方式”中，单击表达式 (fx) 按钮，打开“表达式”对话框     。  
  
7.  键入用于指定要按其分组的所有字段的表达式。 例如，以下组表达式将名为 Color 和 Size 的字段组合在一起： `=Fields!Color.Value & Fields!Size.Value`。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     此时已定义组。 接下来，将要显示的字段拖到矩阵的 Tablix 正文区。 将第 7 步中选择的按其分组的字段添加到 Tablix 正文区，每个字段位于其各自的列中。  
  
     此情况下，不需要 Tablix 行组区域中的第一个列。 若要删除此列，请右键单击列标题，再单击“删除列”  。 所显示的对话框将询问是否删除关联的组。 单击 **“否”** 。 将删除行组区域，而只保留 Tablix 正文区。  
  
     接下来，将删除默认列组。  
  
9. 在“列组”窗格中，右键单击默认列组，再单击“删除组”  。 将出现一个对话框，询问是要删除组以及相关的行和列，还是仅删除组。 单击 **“仅删除组”** 。 将删除列组，并删除列组区域。 只保留 Tablix 正文区。  
  
     接下来，需将交互式排序按钮添加到跨越矩阵的文本框。  
  
10. 单击第一行中的文本框，再单击 **“文本框属性”** 。  
  
11. 单击 **“交互式排序”** 。  
  
12. 选择 **“对此文本框启用交互式排序”** 。  
  
13. 在 **“选择排序对象”** 中，单击 **“组”** 。  
  
14. 从下拉列表中，选择在步骤 5 中创建的组的名称。 组表达式将自动复制到 **“排序依据”** 文本框。  
  
15. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     您已将排序按钮添加到文本框。  
  
16. （可选）还可以在显示组值的列中取消重复值。 在报表设计图面上，单击用于显示要隐藏其重复值的值的文本框。 在“属性”窗格中，滚动到 **HideDuplicates**，并从下拉列表中，选择链接到此矩阵的数据集的名称。  
  
 若要验证排序操作，请单击 **“运行”** 以预览报表，然后单击交互式排序按钮。 矩阵将按组表达式的组合值进行排序，但每个值分别显示在其各自的列中。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [返回页首](#BackToTop)  
  
##  <a name="synchronizing-sort-order-for-multiple-data-regions"></a><a name="SynchronizingSortOrder"></a> 同步多个数据区域的排序顺序  
 添加交互式排序按钮，可使用户能够单击一个排序按钮并对多个数据区域进行排序。 创建交互式排序按钮时，可以指定是否基于相同报表数据集同步多个数据区域的排序。 例如，报表可能包括以图形方式显示数据的矩阵和图表。 用户更改矩阵中行的排序顺序时，图表将自动显示相同的排序顺序。  
  
 若要同步排序顺序，必须为要排序的数据区域或组使用相同的排序表达式，并将排序的作用预定义为两个数据区域的共同祖先。 共同祖先可以是两个数据区域都链接到的数据集，也可以是两个数据区域都显示在其中的包含数据区域。 例如，假定一个报表同时具有显示相同数据集的数据和包含在列表中的矩阵和图表。 若要同步排序操作，必须对该矩阵的列指定交互式排序，并将作用域设置为该列表。 用户对矩阵进行排序时，也将对图表进行排序。  
  
#### <a name="to-synchronize-sort-order-with-a-chart-for-an-interactive-sort-button-on-a-matrix-data-region"></a>将矩阵数据区域上交互式排序按钮的排序顺序与图表同步  
  
1.  在报表设计视图中，向报表中添加一个矩阵。  
  
2.  将数值数据集字段添加到矩阵数据单元，例如，表示数量或销售额的字段。  
  
3.  定义行组。 默认情况下，组的排序顺序设置为与组表达式相同的表达式。  
  
4.  将图表（例如饼图）添加到报表。  
  
5.  将步骤 2 中选择的字段拖到 **“图表数据”** 窗格的 **“值”** 区域中。  
  
6.  将选择的要按其分组的字段拖到 **“类别组”** 区域中。  
  
     矩阵行组和图表类别组的组表达式必须相同。  
  
7.  右键单击类别组，再单击“类别组属性”  。  
  
8.  单击 **“排序”** 。  
  
9. 单击“添加”  。 将向排序选项网格添加一个新的排序行。  
  
10. 在“排序依据”中，从下拉列表选择在步骤 6 中选择的要按其分组的相同字段。  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
12. 在矩阵中，右键单击要向其添加交互式排序按钮的列标题中的文本框，再单击“文本框属性”  。  
  
13. 单击 **“交互式排序”** 。  
  
14. 选择 **“对此文本框启用交互式排序”** 。  
  
15. 在 **“选择排序对象”** 中，单击 **“组”** 。  
  
16. 从“组”下的下拉列表中，选择要排序的组的名称  。 将会自动为 **“排序依据”** 值设置此组的组表达式。  
  
17. 选择 **“同样将此排序应用于以下位置中的其他组和数据区域”** 。 在文本框中，键入数据集的名称，例如 "SalesData"。  
  
18. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 若要验证排序操作，请单击 **“运行”** 以预览报表，然后单击交互式排序按钮。 矩阵将按组表达式的组合值进行排序，但每个值分别显示在其各自的列中。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [返回页首](#BackToTop)  
  
## <a name="see-also"></a>另请参阅  
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [交互式排序（报表生成器和 SSRS）](interactive-sort-report-builder-and-ssrs.md)   
 [对数据区域中的数据进行排序（报表生成器和 SSRS）](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [利用 Tablix 数据区域的灵活性（报表生成器和 SSRS）](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)  
  
  
