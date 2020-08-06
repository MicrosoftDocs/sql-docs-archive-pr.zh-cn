---
title: " (多维数据集向导) 选择创建方法 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubewizard.cubedefinition.f1
ms.assetid: 985d3b5b-7891-465b-862d-f7e75431b342
author: minewiskan
ms.author: owend
ms.openlocfilehash: c8c4d611e00a2b3f5d115ea5749b1e494a44bf57
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589891"
---
# <a name="select-creation-method-cube-wizard"></a>选择创建方法（多维数据集向导）
  可以使用 **“选择创建方法”** 页指定创建多维数据集的方式。  
  
## <a name="options"></a>选项  
 **使用现有表**  
 选择此选项可以通过使用数据源中的现有表创建多维数据集。 该向导将引导您完成基于现有表选择和定义度量值组和维度的整个过程，从而生成新多维数据集。  
  
 **创建空的多维数据集**  
 选择此选项可以创建空的多维数据集。 当要手动创建所有内容或者多维数据集中的所有度量值组都是链接度量值组时，此选项将非常有用。  
  
> [!NOTE]  
>  仅当您正处理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目时，此选项才可用；如果您直接连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，此选项将不可用。  
  
 **在数据源中生成表**  
 选择此选项可以首先创建一个多维数据集，然后可基于多维数据集定义在数据源中生成新表。  
  
> [!NOTE]  
>  若要使用此选项，则您必须拥有在基础数据源中创建对象的权限。  
  
 选择此选项后， **“模板”** 选项将可用。  
  
 **模板**  
 选择要用于创建多维数据集的模板。 模板可以提供一组面向特定业务用途的定义。  
  
> [!NOTE]  
>  仅当选择了“在数据源中生成表”**** 选项时，此选项才可用。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据集对象 &#40;Analysis Services 多维数据&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多维模型中的多维数据集](multidimensional-models/cubes-in-multidimensional-models.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
