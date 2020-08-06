---
title: 第 5 课：设置报表格式 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46efa9-6e04-48ec-afb4-5a2314dcb05a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 00f0d780e957fd9ff995fefb1d033275a7da428d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590578"
---
# <a name="lesson-5-formatting-a-report-reporting-services"></a>Lesson 5: Formatting a Report (Reporting Services)
  既然您已经向 Sales Orders 报表添加了一个数据区域和一些字段，那么您就可以设置日期和货币字段以及列标题的格式。  
  
 本主题内容：  
  
-   [设置日期格式](#bkmk_format_date)  
  
-   [设置货币格式](#bkmk_format_currency)  
  
-   [更改文本样式和列宽](#bkmk_change_textstyle)  
  
##  <a name="format-the-date"></a><a name="bkmk_format_date"></a>设置日期格式  
 默认情况下，Date 字段显示日期和时间信息。 您可以设置其格式，使其只显示日期。  
  
#### <a name="to-format-a-date-field"></a>设置日期字段格式  
  
1.  单击 **“设计”** 选项卡。  
  
2.  右键单击带有 `[Date]` 字段表达式的单元格，然后单击“文本框属性”。****  
  
3.  单击 "**数字**"，然后在 "**类别**" 字段中选择 `Date` 。  
  
4.  在 **“类型”** 框中，选择 **“2000 年 1 月 31 日”**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  预览报表以查看对 `[Date]` 字段的更改，然后更改回设计视图。  
  
##  <a name="format-the-currency"></a><a name="bkmk_format_currency"></a>设置货币格式  
 LineTotal 字段显示常规数字。 请设置其格式，以使其显示货币形式的数字。  
  
#### <a name="to-format-a-currency-field"></a>设置货币字段格式  
  
1.  右键单击带有 `[LineTotal]` 字段表达式的单元格，然后单击“文本框属性”。****  
  
2.  单击 **“数字”**，然后在 **“类别”** 字段中，选择 **“货币”**。  
  
3.  如果区域设置为“英语(美国)”，则默认设置应为：  
  
    -   **小数位数：2**  
  
    -   **负数：($12345.00)**  
  
    -   **符号：$ 英语(美国)**  
  
4.  选择“使用千位分隔符(,)”。****  
  
     如果示例文本为 **$12,345.00**，则说明您的设置是正确的。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  预览报表以查看对 `[LineTotal]` 字段的更改，然后更改回设计视图。  
  
##  <a name="change-text-style-and-column-widths"></a><a name="bkmk_change_textstyle"></a>更改文本样式和列宽  
 还可以更改标题行的格式设置，以使其与报表中的数据行区分开来。 最后，您将调整列的宽度。  
  
#### <a name="to-format-header-rows-and-table-columns"></a>设置标题行和表列的格式  
  
1.  单击表，以便在此表的上方和旁边显示列控点和行控点。  
  
     ![设计，带有标题行和详细信息行的表](../../2014/tutorials/media/rs-basictabledetailsdesign.gif "设计，带有标题行和详细信息行的表")  
  
     沿此表的上方和一侧显示的灰色条状物就是列控点和行控点。  
  
2.  指向列控点之间的行，使光标变为双箭头。 拖动列，调整到所需大小。  
  
3.  选择包含列标题标签的行，从 **“格式”** 菜单中，指向 **“字体”** ，然后单击 **“加粗”**。  
  
4.  若要预览报表，请单击 "**预览**" 选项卡。其外观应如下所示：  
  
     ![带有以粗体显示的列标题的表预览](../../2014/tutorials/media/rs-basictabledetailsformattedpreview.gif "带有以粗体显示的列标题的表预览")  
  
5.  在 **“文件”** 菜单上单击 **“全部保存”** 可保存报表。  
  
## <a name="next-steps"></a>后续步骤  
 您已成功地设置了列标题以及日期和货币值的格式。 接下来，您将向报表中添加分组和总计。 请参阅[第 6 课：添加分组和总计 (Reporting Services)](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置数字和日期格式 &#40;报表生成器和 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
