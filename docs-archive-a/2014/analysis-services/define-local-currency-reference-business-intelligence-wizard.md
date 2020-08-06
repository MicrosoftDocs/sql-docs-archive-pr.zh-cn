---
title: 定义 (商业智能向导) 的本地货币引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
ms.openlocfilehash: bcd5c01839ecc7ae120089f17a1b909f18464e9d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690864"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>定义本地货币引用（商业智能向导）
  可以使用“定义本地货币引用”**** 页，为涉及“选择换算类型”**** 页中指定的多对多或多对一换算类型的货币换算功能定义本地货币。 本地货币是存储 **“选择度量值”** 页中所选度量值的事务时使用的货币。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此页。 如果在“选择换算类型”**** 页中选择了“一对多”****，则不会显示此页。  
  
## <a name="options"></a>选项  
 **事实数据表中的标识符**  
 对于包含“选择度量值”**** 页中所选度量值的事实数据表所引用的货币维度，选择此选项可指定为该货币维度中的本地货币提供货币标识符的属性。  (一个 "货币" 维度，其 `Type` 属性设置为 "*货币*"。 )   
  
 在由事务本身确定事务的本地货币时使用此选项。 例如，在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 示例数据库中 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] ，"Internet 销售" 度量值组具有与货币维度的常规维度关系。 该度量值组的事实数据表包含一个外键列，该外键列引用该维度的维度表中的货币标识符。  
  
 **事实数据引用的货币维度和属性**  
 在成员表示本地货币的货币标识符的货币维度中选择货币属性。  (货币属性是其 `Type` 属性设置为 "*货币*" 的属性。 )   
  
> [!NOTE]  
>   如果未选择 **“事实数据表中的标识符”** 选项，则此选项不可用。  
  
 **维度表中的属性**  
 选择此选项可从与包含本地货币货币标识符的度量值组相关的维度中指定属性。  
  
 在由事务和另一个业务实体（如位置）之间的关系确定该事务的本地货币时使用此选项。 例如，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 示例数据库-中 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] ，"财务报表" 度量值组与 "货币" 维度之间通过 "单位" 维度的引用维度关系。 也就是说，“财务报表”度量值组的事实数据表包含一个外键列，该外键列引用了“单位”维度的维度表中的成员。 反过来，“单位”维度的维度表也包含一个外键列，该外键列引用“货币”维度的维度表中的货币标识符。  
  
 **引用货币的维度属性**  
 在成员引用本地货币的货币标识符的维度中选择属性。  
  
> [!NOTE]  
>   如果未选择 **“维度表中的属性”** 选项，则此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器 &#40;Analysis Services 多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器 &#40;Analysis Services 多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
