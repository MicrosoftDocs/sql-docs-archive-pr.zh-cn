---
title: " (数据挖掘向导) 指定表类型 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytabletypes.f1
ms.assetid: 8209a707-faef-4ffc-8991-6c13bb350753
author: minewiskan
ms.author: owend
ms.openlocfilehash: 88c09f26958c37ed0a99efb54a5eb5c08505d16b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589244"
---
# <a name="specify-table-types-data-mining-wizard"></a>指定表类型(数据挖掘向导)
  可以使用 **“指定表类型”** 页指定用于定义挖掘结构的表。 如果未选择某个表，则将不能使用该表来定义挖掘结构。  
  
> [!NOTE]  
>   可以在以后在 **数据挖掘设计器** 的 **“挖掘结构”** 选项卡上添加表。  
  
 **有关详细信息，请参阅** [嵌套表（Analysis Services – 数据挖掘）](data-mining/nested-tables-analysis-services-data-mining.md)、[数据挖掘向导（Analysis Services - 数据挖掘）](data-mining/data-mining-wizard-analysis-services-data-mining.md)和[创建关系挖掘结构](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>选项  
 **表**  
 显示在向导的“选择数据源视图”**** 页上选择的数据源视图中的表。  
  
 **区分**  
 选择一个要用作事例表的表。  
  
 **嵌套**  
 选择要用作嵌套表的表。  
  
> [!NOTE]  
>  这些表必须与事例表具有多对一关系，而不是一对多关系。 必须在数据源视图中指定此关系，才能将表选择为嵌套表。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘向导 F1 帮助 &#40;Analysis Services 数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [在数据挖掘向导 &#40;选择数据源视图&#41;](select-data-source-view-data-mining-wizard.md)   
 [在数据挖掘向导 &#40;指定定型数据&#41;](specify-the-training-data-data-mining-wizard.md)  
  
  
