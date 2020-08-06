---
title: 定义帐户智能 (维度向导) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
ms.openlocfilehash: 90871e2299d1531db1b678b1f4b16ddd7f1db767
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588751"
---
# <a name="define-account-intelligence-dimension-wizard"></a>定义帐户智能（维度向导）
  可以使用 **“定义帐户智能”** 页，将 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型映射到与维度中的 **“帐户类型”** 属性类型关联的维度属性中定义的帐户类型。  
  
> [!NOTE]  
>   仅当您在 **“选择维度类型”** 页中选择 **“标准维度”** 以及在 **“指定维度类型”** 页上将维度属性映射到 **“帐户类型”** 属性类型时，才会显示此页。  
  
## <a name="options"></a>选项  
 **源表帐户类型**  
 显示分配给“指定维度键和类型”**** 页中“帐户类型”**** 属性类型的维度属性中包含的值。  
  
 **内置帐户类型**  
 选择在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型，该帐户类型将映射到源表中的帐户类型。  
  
 下表列出了在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型：  
  
|值|说明|  
|-----------|-----------------|  
|**资产**|在特定时间拥有的物品的价值。|  
|**Balance**|在特定时间某物的计数。|  
|**费用**|所花费的价值。|  
|**流向**|事物的增量计数。|  
|**收入**|收到的价值。|  
|**负债**|在特定时间所拖欠的价值。|  
|**统计**|某事物的计算比率，或者未聚合的某事物的计数。|  
  
## <a name="see-also"></a>另请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [Analysis Services 多维数据 &#40;维度&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
