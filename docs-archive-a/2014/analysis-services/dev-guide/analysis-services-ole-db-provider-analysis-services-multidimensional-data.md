---
title: Analysis Services OLE DB Provider (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services OLE DB Provider
ms.assetid: cdeecd50-1d91-4162-a4a2-01c7799b02a8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8c0348a23a6def4c3cdbd083354083947ce1390b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591644"
---
# <a name="analysis-services-ole-db-provider-analysis-services---multidimensional-data"></a>Analysis Services OLE DB 访问接口（Analysis Services - 多维数据）
  Analysis Services OLE DB Provider 是与交互的应用程序的接口 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 它用于生成与多维数据进行交互的客户端应用程序。 此访问接口还提供对多维数据和关系数据进行联机或脱机数据挖掘分析的方法，且为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的一部分。 它可由第三方客户端应用程序进行再分发。  
  
 Analysis Services OLE DB 访问接口是用于与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行交互以完成以下任务的主要方法：连接到多维数据集或数据挖掘模型、查询多维数据集或数据挖掘模型，以及检索架构信息。  
  
 Analysis Services OLE DB 访问接口是一种独立的访问接口，通过该访问接口，客户端应用程序可以借助关系源和多维源创建本地多维数据集文件和挖掘模型。 客户端应用程序可以连接到本地多维数据集，并使用多维表达式 (MDX) 执行查询，而不用与运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的全功能服务器进行交互。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型数据访问 &#40;Analysis Services 多维数据&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  
