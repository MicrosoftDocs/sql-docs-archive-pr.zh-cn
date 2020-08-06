---
title: " (商业智能向导) 配置维度属性 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.selectattributes.f1
ms.assetid: 3d046e63-bcb1-4ab1-9c37-652463fa68c3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1d2e9bc83b7a6d83b6d2808b472d67169266ff07
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579238"
---
# <a name="configure-dimension-attributes-business-intelligence-wizard"></a>配置维度属性（商业智能向导）
  可以使用 **“配置维度属性”** 页，将维度属性映射到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用于标识帐户维度属性的属性类型。  
  
## <a name="options"></a>选项  
 **维度类型**  
 显示所选维度类型。  
  
> [!NOTE]  
>  此选项不可用，因为 `Type` 维度的属性不能更改为帐户维度的*帐户*之外的值。  
  
 **“维度属性”**  
 显示可以映射到维度中现有维度属性的有效属性类型。  
  
 **包括**  
 选中复选框，将维度中相应的属性类型包括在内。  
  
 **特性类型**  
 列出可以映射到维度中现有维度属性的属性类型。  
  
 **维度属性**  
 选择应该映射到相应属性类型的维度属性。  
  
 **基于帐户类型将度量值设置为半累加性**  
 选中此选项，可以将与此维度相关联的每个度量值更改为按帐户类型聚合。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此选项。  
  
## <a name="see-also"></a>另请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器 &#40;Analysis Services 多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器 &#40;Analysis Services 多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
