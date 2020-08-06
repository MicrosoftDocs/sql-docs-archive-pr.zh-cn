---
title: 架构生成向导 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2cd58ada8ea4c2dd17ba4427578ac1336a6bd353
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588723"
---
# <a name="schema-generation-wizard-analysis-services"></a>架构生成向导 (Analysis Services)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 项目或数据库中定义 OLAP 对象时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持两种使用关系架构的方法。 通常，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或数据库中，将基于在数据源视图中构造的逻辑数据模型来定义 OLAP 对象。 此数据源视图将基于一个或多个关系数据源中的架构元素定义，如在数据源视图中自定义那样。  
  
 或者，您可以首先定义 OLAP 对象，然后生成数据源视图、数据源和支持这些 OLAP 对象的基础关系数据库架构。 该关系数据库称为主题区域数据库。  
  
 此方法有时称为由上而下设计，并且通常用于对建模确定原型并进行分析。 使用此方法时，使用架构生成向导基于在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目或数据库中定义的 OLAP 对象创建基础数据源视图和数据源对象。  
  
 这是一个迭代的方法。 更改维度和多维数据集的设计时，您很可能多次重新运行该向导。 每次运行该向导时，它会将更改合并到基础对象中，并尽可能保留基础数据库中的数据。  
  
 生成的架构是 SQL Server 关系数据库引擎架构。 该向导不生成其他关系数据库产品的架构。  
  
 使用您用于填充 SQL Server 关系数据库的任意工具和技术单独添加在主题区域数据库中填充的数据。 在大多数情况下，重新运行向导时会保留该数据，但是也有例外。 例如，如果您删除包含数据的维度或属性，则必须删除某些数据。 如果架构生成向导因架构的更改必须删除某些数据，则您便会在删除数据之前收到一则警告，然后可以取消重新生成。  
  
 作为通用规则，当架构生成向导在以后重新生成对象时，对最初由架构生成向导生成的对象所做的任何更改都要被覆盖。 但是，当您将列添加到架构生成向导生成的表中时，便属于此规则的主要例外情况。 在这种情况下，架构生成向导将保留您添加到表中的列以及这些列中的数据。  
  
## <a name="in-this-section"></a>本节内容  
 下表列出了说明如何使用架构生成向导的其他主题。  
  
|主题|说明|  
|-----------|-----------------|  
|[使用架构生成向导 (Analysis Services)](schema-generation-wizard-analysis-services.md)|介绍如何为主题区域数据库和临时区域数据库生成架构。|  
|[了解数据库架构](understanding-the-database-schemas.md)|介绍为主题区域数据库和临时区域数据库生成的架构。|  
|[了解增量生成](understanding-incremental-generation.md)|介绍架构生成向导的增量式生成功能。|  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)   
 [多维模型中的数据源](data-sources-in-multidimensional-models.md)   
 [支持 &#40;SSAS 多维&#41;的数据源](supported-data-sources-ssas-multidimensional.md)  
  
  
