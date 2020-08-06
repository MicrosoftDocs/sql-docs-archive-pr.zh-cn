---
title: 设置仪表上指针的格式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2fdf670a-5237-48fe-813d-97657c5c77d2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c74cb4d4c61c18d25069dab062bf09804f5935b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682717"
---
# <a name="formatting-pointers-on-a-gauge-report-builder-and-ssrs"></a>设置仪表上指针的格式（报表生成器和 SSRS）
  仪表指针指示仪表的当前值。 默认情况下，添加字段之后，字段中包含的值将聚合为仪表指针显示的一个值。 可以为仪表添加多个指针以便指向基于相同刻度的多个值，也可以添加多个刻度，并为添加的每个刻度各添加一个指针。 向仪表添加字段之后，必须对相应刻度设置最大值和最小值，以便为指针值提供上下文。 您还可以选择设置某一范围的最小值和最大值，该范围在刻度上显示一个关键区域。  
  
 通过右键单击指针并选择“径向指针属性”或“线性指针属性”，可以设置指针的外观属性   。 每个仪表指针都包含一组相同的属性。 此外，每个仪表类型还包含相应的特有外观属性：  
  
-   在径向仪表中，可以指定针式指针和指针顶端。  
  
-   在线性仪表上，可以指定温度计指针，它是条形指针的变体。 温度计指针可用于指定球的形状。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="how-the-pointer-is-connected-to-data"></a><a name="HowPointer"></a> 指针与数据的连接方式  
 默认情况下，添加仪表时，它包含一个没有任何关联字段的指针。 这称为空指针。 在向数据窗格添加字段之前，空指针将一直显示零。 向数据窗格添加某一字段后，指针随即连接到该字段。 如果从数据窗格中删除某一字段，还将删除与该字段关联的指针。  
  
 添加数据之后，若右键单击指针，将显示“清除指针值”和“删除指针”选项   。 **“清除指针值”** 选项将删除附加到仪表的字段，但仍将在仪表上显示指针。 **“删除指针”** 选项将从仪表中删除字段，并且从视图中删除指针。 如果向该仪表重新添加字段，则将重新显示该默认指针。 将指针的 "**隐藏**" 属性设置为时 `True` ，指针不会在设计图面上隐藏，而是在运行时隐藏。  
  
  
##  <a name="displaying-multiple-pointers-on-the-gauge"></a><a name="DisplayingMultiple"></a> 在仪表上显示多个指针  
 可以为仪表添加多个指针以便指向基于相同刻度的多个值。 这对同时显示较低值和较高值很有用。 若要在仪表上为相同刻度指定多个指针，请右键单击仪表内的任意位置，并单击快捷菜单上的“添加指针”  。 或者，也可以通过右键单击仪表内的任意位置，再单击“添加刻度”来添加刻度  。 然后，可以添加新指针，该指针将与最新刻度自动关联。  
  
 指针重叠时，指针的绘制顺序由它们添加到仪表中的顺序确定。 更改数据窗格中的字段顺序无法对指针的绘制顺序进行重新排序。 若要更改多个指针的绘制顺序，请打开“属性”窗格并单击“指针 (…)”  。然后，更改指针在指针集合中的顺序。  
  
  
##  <a name="setting-gradients-on-a-needle-cap"></a><a name="SettingGradients"></a> 在指针顶端上设置渐变  
 只能在径向仪表上指定可绘制在指针上面或下面的顶端。 所有指针顶端样式都是使用无法修改的内置渐变绘制的。 但 `RoundedDark` 样式除外，你可以为该样式指定渐变颜色和渐变样式。  
  
  
##  <a name="setting-a-snapping-interval"></a><a name="SettingSnappingInterval"></a> 设置对齐间隔  
 对齐间隔定义一个数值，舍入后的值是它的倍数。 默认情况下，仪表将指向已在数据窗格中指定的字段的精确值。 但是，您可能希望该精确值向上舍入或向下舍入，以使指针与预设的间隔对齐。 例如，如果仪表上的值为 34.2 并且您将对齐间隔指定为 5，则仪表指针将指向 35。 如果仪表上的值为 31.2 并且您将对齐间隔指定为 5，则仪表指针将指向 30。 有关详细信息，请参阅[在仪表上设置对齐间隔 &#40;报表生成器和 SSRS&#41;](../set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs.md)。  
  
  
##  <a name="specifying-an-image-as-a-pointer-on-a-radial-gauge"></a><a name="SpecifyingImage"></a> 指定图像作为径向仪表的指针  
 除指针样式的内置列表以外，还可以指定图像作为指针。 当使用图像替换现有针式指针样式时，该方法最有效。 图像叠加在指针之上，但所有指针功能都适用。 将图像用作指针时，颜色和渐变选项不适用。  
  
 如果指针图像的形状不规则，则应将颜色指定为透明色，以隐藏不应在仪表上显示的图像区域。 定义透明色时，仪表将图像转置到现有指针之上并裁剪该图像，以便仅显示指针形状。 仪表重新缩放图像，使其适合指针大小。 为指针指定图像时，在仪表上面添加的所有后续指针均绘制到该图像下面。 为此，如果仪表上存在多个指针，最好不要为指针指定图像。 有关详细信息，请参阅[指定图像作为仪表上的指针 &#40;报表生成器和 SSRS&#41;](../specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs.md)。  
  
  
## <a name="see-also"></a>另请参阅  
 [设置仪表上刻度的格式（报表生成器和 SSRS）](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [设置仪表上范围的格式（报表生成器和 SSRS）](formatting-ranges-on-a-gauge-report-builder-and-ssrs.md)   
 [仪表（报表生成器和 SSRS）](gauges-report-builder-and-ssrs.md)  
  
  
