---
title: 基于使用情况的优化向导的 F1 帮助 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.f1
helpviewer_keywords:
- Usage-Based Optimization Wizard
ms.assetid: e5f5a938-ae7c-4f4e-9416-a7f94ac82763
author: minewiskan
ms.author: owend
ms.openlocfilehash: 517c122f79421294e1dfa562665948c4dc7bf95f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691346"
---
# <a name="usage-based-optimization-wizard-f1-help"></a>基于使用情况的优化向导的 F1 帮助
  基于使用情况的优化向导用于为分区设计聚合，它在输出方面与聚合设计向导相似。 但是，基于使用情况的优化向导设计聚合时所基于的是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例查询日志中所记录的特定使用模式的查询。 聚合通过允许 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 直接从多维数据集存储中检索预先计算的总计，而不必为每个查询重新计算基础数据源中的数据，从而提高了性能。  
  
 若要从内打开基于使用情况的优化向导 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ，请为项目打开多维数据集设计器， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 然后单击 "**聚合**" 选项卡。单击工具栏中的 "**基于使用情况的优化**" 按钮。  
  
 要从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 内打开基于使用情况的优化向导，请连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，然后打开“多维数据集”**** 文件夹。 选择多维数据集，然后打开 **“度量组”** 文件夹，然后展开要修改的度量组。 右键单击“分区”**** 文件夹，然后选择“基于使用情况的优化”****。  
  
 若要对这些聚合进行设计，可以使用聚合设计向导。 此向导可引导您完成以下步骤：  
  
-   为分区、度量值组或多维数据集的存储和缓存选项选择标准或自定义设置。  
  
-   为分区、度量值组或多维数据集所引用的对象提供估计计数或实际计数。  
  
-   指定聚合选项和限制，以优化所设计聚合的存储和查询性能。  
  
-   保存并根据需要处理分区、度量值组或多维数据集，以生成定义的聚合。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的聚合设计向导基于对分区结构的统计分析设计聚合，可生成受存储大小或估计性能提升范围限制的聚合设计。 您可以使用聚合设计向导改进分区的总体性能，但是并不能针对业务用户的特定需要设计聚合。 基于使用情况的优化向导可以针对这些特定需要设计聚合，但前提是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的查询日志包含了构造此类查询所需的足够信息。  
  
 通常，可以同时使用这两个向导来改进在部署时和一段时间后的性能。 在完成分区（或包含分区的多维数据集或度量值组）的初期部署后，应当首先使用聚合设计向导，以改进整体性能。 经过一段时间（在此期间您已在查询日志中记录了业务用户对分区的所有查询）之后，则可以使用基于使用情况的优化向导来进一步完善聚合设计，以便更好地满足业务用户的性能和查询要求。  
  
> [!NOTE]  
>  有关配置查询日志的信息，请参阅 [配置 Analysis Services 查询日志](instances/log-operations-in-analysis-services.md?view=sql-server-2014#bkmk_querylog)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [选择要修改 &#40;基于使用情况的优化向导的分区&#41;](select-partitions-to-modify-usage-based-optimization-wizard.md)  
  
-   [指定基于使用情况的优化向导 &#40;查询条件&#41;](specify-query-criteria-usage-based-optimization-wizard.md)  
  
-   [查看将优化 &#40;基于使用情况的优化向导的查询&#41;](review-the-queries-that-will-be-optimized-usage-based-optimization-wizard.md)  
  
-   [查看聚合使用情况 &#40;基于使用情况的优化向导&#41;](review-aggregation-usage-usage-based-optimiation-wizard.md)  
  
-   [指定基于使用情况的优化向导 &#40;对象计数&#41;](specify-object-counts-usage-based-optimization-wizard.md)  
  
-   [使用基于使用情况的优化向导 &#40;设置聚合选项&#41;](set-aggregation-options-usage-based-optimization-wizard.md)  
  
-   [完成向导 &#40;基于使用情况的优化向导&#41;](completing-the-wizard-usage-based-optimization-wizard.md)  
  
## <a name="see-also"></a>另请参阅  
 [聚合和聚合设计](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [多维模型中的多维数据集](multidimensional-models/cubes-in-multidimensional-models.md)   
 [聚合设计向导的 F1 帮助](aggregation-design-wizard-f1-help.md)   
 [&#40;多维数据的 Analysis Services 向导&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
