---
title: 使用表达式指定指示器的大小（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b450abb957329b8dbaa4f7f0e4c963c5f63f06b3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577256"
---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>使用表达式指定指示器的大小（报表生成器和 SSRS）
  除了颜色、方向和形状外，您还可以使用大小来提供最佳的指示器视觉效果。  
  
 指示器具有名为 IndicatorStates 的指示器状态的集合。 IndicatorStates 集合通常具有多个状态。 每个状态都是该集合的成员，并且由一个图标表示。 这些状态一起构成了 IndicatorsStates 集合。  
  
 若要动态配置图标大小，请在报表生成器的“属性”窗格中设置 IndicatorsStates 集合中各成员的属性。 如果 **“属性”** 窗格不可见，请单击 **“视图”** 选项卡，然后选择 **“属性”** 。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，使用 **“属性”** 窗口以便设置成员属性。 如果 **“属性”** 窗口未打开，则按 F4 键。  
  
 “属性”窗格提供对指示器的 IndicatorStates 集合的属性的访问  。 可以通过使用表达式设置 IndicatorStates 集合成员的 ScaleFactor 属性，将图标配置为不同的大小。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
 在此过程中使用的表达式还用于生成具有不同大小的指示器的报表，如 [指示器（报表生成器和 SSRS）](indicators-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>使用表达式指定指示器图标大小  
  
1.  单击要更改的指示器。  
  
2.  在“属性”窗格中找到 IndicatorStates 属性。  
  
     如果“属性”窗格按类别进行组织，则将在“状态”类别中找到 IndicatorStates  。  
  
3.  单击 IndicatorStates 旁的省略号 **(...)** 按钮。 **“指示器状态集合编辑器”** 对话框将打开。  
  
     选择该集合的所有成员。  
  
4.  在“多选属性”列表中，单击 ScaleFactor 旁的向下箭头，然后单击“表达式”   。  
  
5.  在 **“表达式”** 对话框中，写入表达式。  
  
     下面的示例表达式基于 **SalesYTD** 字段的值使图标采用不同的大小。  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     有关详细信息，请参阅[表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [指示器（报表生成器和 SSRS）](indicators-report-builder-and-ssrs.md)  
  
  
