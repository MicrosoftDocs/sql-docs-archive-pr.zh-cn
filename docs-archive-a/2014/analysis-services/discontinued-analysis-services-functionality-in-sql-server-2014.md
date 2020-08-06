---
title: SQL Server 2014 中的废止 Analysis Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5414344eb65c907593c9077ee2ba5610b8b397c0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590981"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>SQL Server 2014 中废弃的 Analysis Services 功能
  此主题介绍 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中不再可用的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]功能。  
  
## <a name="discontinued-features-in-sssql14"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|类别|不推荐使用的功能|替代功能|  
|--------------|------------------------|-----------------|  
|本地多维数据集|InsertInto 连接字符串属性|用于填充本地多维数据集的原始连接字符串语法已替换为 Create Global Cube（创建全局多维数据集）语句。 有关详细信息，请参阅[CREATE GLOBAL CUBE 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)。|  
|本地多维数据集|CreateCube 连接字符串属性|用于填充本地多维数据集的原始连接字符串语法已替换为 Create Global Cube（创建全局多维数据集）语句。 有关详细信息，请参阅[CREATE GLOBAL CUBE 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-global-cube)。|  
|数据挖掘|SQL Server 2000 PMML|SQL Server 2000 PMML 功能生成了一种格式的 PMML，它具有专有扩展插件，以支持由 PMML 规范中未提供的数据挖掘算法所提供的独特功能。 在 SQL Server 2005 中，Analysis Services 已将 PMML 功能更新为更高的 PMML 2.1 标准。 因此，不再需要在 SQL Server 2000 中添加的专有扩展插件，尽管此版本中仍支持它们。|  
|MDX 语句|Create Action 语句|包括此语句是为了向后兼容。 它将替换为 Action 对象。 有关如何在最新版本的中创建操作的详细信息 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，请参阅[&#40;Analysis Services 多维数据&#41;的操作](multidimensional-models/actions-analysis-services-multidimensional-data.md)。|  
  
## <a name="discontinued-features-in-previous-releases"></a>以前版本中废止的功能  
 用于将 SQL Server 2000 Analysis Services 数据库迁移到更新版本的迁移向导已被废弃，因为不再支持 SQL Server 2000。  
  
 为与 SQL Server 2000 Analysis Services 数据库兼容而提供的决策支持对象 (DSO) 库也已废弃，因为该库不再是 SQL Server 的一部分了。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 向后兼容性](analysis-services-backward-compatibility.md)  
  
  
