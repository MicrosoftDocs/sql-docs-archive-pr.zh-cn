---
title: 在 MDX 查询设计器中为 Analysis Services (报表生成器和 SSRS) 定义参数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6b2b05fc0122eb25a7a0799f7b47b1b99486a28c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694282"
---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services-report-builder-and-ssrs"></a>在 Analysis Services 的 MDX 查询设计器中定义参数（报表生成器和 SSRS）
  若要参数化 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源的 MDX 查询，则必须向查询添加查询参数。 在 MDX 查询设计器中，在设计模式和查询模式下都可以通过指定筛选器来添加查询参数。 使用查询参数定义查询后，Reporting Services 会自动创建报表参数和数据集，以提供有效值的列表。 这样用户就可以指定要直接传递给查询的值。

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>在设计模式下的 MDX 中定义查询参数

1.  在“报表数据”窗格中，右键单击从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源类型创建的数据集，然后单击“查询”  。 此时将在设计模式下打开 MDX 查询设计器。

2.  将维度拖至筛选区域，然后将其放入 **“维度”** 列的第一个单元格中。

3.  在“ **层次结构** ”列中，从下拉列表中选择一个值。

4.  在“ **运算符** ”列中，从下拉列表中选择一个运算符。

5.  在“ **筛选表达式** ”列中，从下拉列表中选择单个值，或单击“ **全部** ”成员选择所有值。

6.  在 **“参数”** 列中，选择复选框以创建报表参数。

7.  单击 **“运行”** 。

     运行查询后，单击工具栏中的 **“设计”** 可以切换到查询模式来查看所创建的 MDX 查询。 若要继续使用设计模式开发查询，请不要在查询模式下更改查询文本。 单击 **“设计”** 可以切换回设计模式。

8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

     在“报表数据”窗格中，展开“参数”节点以显示自动为筛选器创建的报表参数。

     若要查看为报表参数提供可用值的数据集，请右键单击“报表数据”窗格中的任意空白区域，然后单击“ **显示隐藏的数据集**”。 此时“报表数据”窗格将显示报表中的所有数据集。

### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>在查询模式下的 MDX 中定义查询参数

1.  在“报表数据”窗格中，右键单击从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据源类型创建的数据集，然后单击“查询”  。 此时将在设计模式下打开 MDX 查询设计器。

2.  在工具栏上单击 **“设计”** 以切换到查询模式。

3.  在 MDX 查询设计器工具栏上，单击“查询参数”  （![“查询参数”对话框图标](../../analysis-services/media/iconqueryparameter.gif "“查询参数”对话框图标")）。 此时将打开“查询参数”对话框。

4.  在 "**参数**" 列中，单击 **\<Enter Parameter>** ""，然后键入参数的名称。

5.  在“ **维度** ”列中，从下拉列表中选择一个值。

6.  在“ **层次结构** ”列中，从下拉列表中选择一个值。

7.  在 **“多个值”** 列中，选中复选框以创建多值参数。

8.  在“ **默认值** ”列中，根据步骤 5 中的选择，从下拉列表中选择一个值或多个值。

9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

10. 在查询设计器工具栏中，单击 **“运行”** 。

11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]

     在“报表数据”窗格中，展开“参数”节点以显示自动为筛选器创建的报表参数。

     若要查看为报表参数提供可用值的数据集，请右键单击“报表数据”窗格中的任意空白区域，然后单击“ **显示隐藏的数据集**”。 此时“报表数据”窗格将显示报表中的所有数据集。

## <a name="see-also"></a>另请参阅
 [Mdx &#40;SSRS&#41;Analysis Services 连接类型](analysis-services-connection-type-for-mdx-ssrs.md) [Analysis Services Mdx 查询设计器用户界面](analysis-services-mdx-query-designer-user-interface.md)


