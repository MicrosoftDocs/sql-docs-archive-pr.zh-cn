---
title: " (维度向导) 指定源信息 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 99bbaac0bdf24a18dcde455e779f056b98106dc4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589247"
---
# <a name="specify-source-information-dimension-wizard"></a>指定源信息（维度向导）
  可以使用 **“选择主维度表”** 页，为要创建的维度选择数据源视图、主维度表、键列和成员名列。  
  
 **打开维度向导**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“维度”文件夹，然后单击“新建维度”********。  
  
## <a name="options"></a>选项  
 **数据源视图**  
 选择数据源视图。  
  
 **主表**  
 从所选数据源视图中选择一个表，用作维度的主表。  
  
 **键列**  
 从维度的键属性的“主表”指定的表中选择键列。****  
  
> [!NOTE]  
>  您可以选择多列。 如果该表包含组合主键，则选择组合主键中包含的所有列。 键列的顺序很重要。  
  
 **名称列**  
 从提供维度成员名称的“主表”指定的表中选择列。**** 使用组合键时，必须指定名称列。 若要创建组合键的名称列，建议您在数据源视图中创建串联指定键列的命名计算。 使用单个键时，名称列是可选的。  
  
## <a name="see-also"></a>另请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [Analysis Services 多维数据 &#40;维度&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
