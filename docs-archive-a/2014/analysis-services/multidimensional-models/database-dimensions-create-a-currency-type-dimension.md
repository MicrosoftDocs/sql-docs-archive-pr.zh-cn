---
title: 创建货币类型维度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], currency
- currency [Analysis Services]
- converting currency
- currency dimensions [Analysis Services]
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 91123fb5fda898e90056057114295335fbd1d32c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689072"
---
# <a name="create-a-currency-type-dimension"></a>创建货币类型维度
  在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，货币类型维度是指其属性表示用于财务报表的货币列表的维度。  
  
 通过货币维度，您可以为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中的多维数据集添加货币换算功能。 若要为多维数据集添加货币换算功能，请使用商业智能向导定义一个多维表达式 (MDX) 脚本命令，该命令可将货币度量值换算为适用于客户端应用程序区域设置的值。 若要创建此 MDX 脚本，商业智能向导需要以下信息：  
  
-   表示源货币的货币维度。 （此维度为源货币维度。）  
  
-   表示要使用的汇率的度量值组。  
  
 商业智能向导将根据此信息设计货币换算进程，该进程可以标识相应的目标货币维度（表示目标货币的货币维度）。 根据商业智能解决方案需要的货币换算的数量，商业智能向导可以定义多个目标货币维度。 有关定义货币换算的详细信息，请参阅[货币换算 (Analysis Services)](../currency-conversions-analysis-services.md)。  
  
 若要将某个维度标识为货币维度，请将该维度的 `Type` 属性设置为 `Currency`。  
  
## <a name="dimension-structure"></a>维度结构  
 一个货币维度必须在货币维度的维度表中至少包含一个用于标识单个货币的键特性。 源货币维度和目标货币维度中的键特性的值不相同：  
  
-   若要将某个特性标识为源货币维度的键特性，请将该特性的 `Type` 属性设置为 `CurrencySource`。  
  
-   若要将某个特性标识为目标货币维度，请将该特性的 `Type` 属性设置为 `CurrencyDestination`。  
  
 用于报表时，源货币维度和目标货币维度都可以包含以下特性（可选）：  
  
-   货币名称特性。  
  
     若要将某个特性标识为货币名称特性，请将该特性的 `Type` 属性设置为 `CurrencyName`。  
  
-   货币源特性。  
  
     若要将某个特性标识为货币源特性，请将该特性的 `Type` 属性设置为 `CurrencySource`。  
  
-   货币的国际标准组织 (ISO) 代码。  
  
     若要将某个特性标识为货币的 ISO 代码特性，请将该特性的 `Type` 属性设置为 `CurrencyIsoCode`。  
  
 有关属性类型的详细信息，请参阅 [配置属性类型](attribute-properties-configure-attribute-types.md)。  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>通过商业智能向导定义帐户智能  
 如果定义了帐户维度并将该维度添加到了多维数据集中，则可以使用商业智能向导来为维度添加帐户智能功能（如标识和映射帐户类型）。 有关详细信息，请参阅 [向维度中添加帐户智能](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [商业智能向导的 F1 帮助](../business-intelligence-wizard-f1-help.md)   
 [维度类型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
