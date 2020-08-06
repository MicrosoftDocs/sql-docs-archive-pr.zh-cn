---
title: Analysis Services) 的最大容量规范 (|Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [Analysis Services], maximum number
- objects [Analysis Services], maximum size
ms.assetid: 49fe1673-b908-4c7a-88ff-415efd294d27
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0495ed563585a5b7427655428a257174673fc02
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589290"
---
# <a name="maximum-capacity-specifications-analysis-services"></a>最大容量规范 (Analysis Services)
  以下各表基于不同的服务器部署模式指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 组件中定义的各种对象的最大大小和最大数量。  
  
 本主题包含以下各节：  
  
 [多维和数据挖掘 (DeploymentMode=0)](#bkmk_OLAP)  
  
 [SharePoint (DeploymentMode=1)](#bkmk_sharepoint)  
  
 [表格 (DeploymentMode=2)](#bkmk_vertipaq)  
  
##  <a name="multidimensional-and-data-mining-deploymentmode0"></a><a name="bkmk_OLAP"></a>多维和数据挖掘 (DeploymentMode = 0)   
 MOLAP 存储模式（既存储数据，也存储元数据）具有针对文件大小的附加物理限制。 字符串存储文件的默认最大大小是 4 GB。 如果您要求更大的文件来用于字符串存储，则可以指定其他字符串存储体系结构。 有关详细信息，请参阅[配置维度和分区的字符串存储](../configure-string-storage-for-dimensions-and-partitions.md)。  
  
|对象|最大大小/数量|  
|------------|----------------------------|  
|一个实例中的数据库数|2^31-1 = 2,147,483,647|  
|数据库中的维度|2^31-1 = 2,147,483,647|  
|维度中的属性|2^31-1 = 2,147,483,647|  
|维度属性中的成员|2^31-1 = 2,147,483,647|  
|维度中的用户定义层次结构|2^31-1 = 2,147,483,647|  
|用户定义层次结构中的级别|2^31-1 = 2,147,483,647|  
|数据库中的多维数据集|2^31-1 = 2,147,483,647|  
|多维数据集中的度量值组|2^31-1 = 2,147,483,647|  
|度量值组中的度量值|2^31-1 = 2,147,483,647|  
|多维数据集中的计算|2^31-1 = 2,147,483,647|  
|多维数据集中的 KPI|2^31-1 = 2,147,483,647|  
|多维数据集中的操作|2^31-1 = 2,147,483,647|  
|多维数据集中的分区|2^31-1 = 2,147,483,647|  
|多维数据集中的翻译|2^31-1 = 2,147,483,647|  
|分区中的聚合|2^31-1 = 2,147,483,647|  
|查询返回的单元数|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名称的长度|100 个字符|  
|数据挖掘模型属性列中的最大不同状态数|2^31-1 = 2,147,483,647|  
|考虑的最大属性数（功能选择）|2^31-1 = 2,147,483,647|  
  
 有关对象命名准则的详细信息，请参阅[ASSL 对象和对象特性](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
 有关联机分析处理 (OLAP) 和数据挖掘的数据源限制的详细信息，请参阅[&#40;Ssas 多维&#41;支持的数据](../supported-data-sources-ssas-multidimensional.md)源、 [&#40;Ssas 多维&#41;支持的数据源](../supported-data-sources-ssas-multidimensional.md)以及[ASSL 对象和对象特性](../scripting-language-assl/assl-objects-and-object-characteristics.md)。  
  
##  <a name="sharepoint-deploymentmode1"></a><a name="bkmk_sharepoint"></a>SharePoint (DeploymentMode = 1)   
  
|对象|最大大小/数量|  
|------------|----------------------------|  
|一个实例中的数据库数|2^31-1 = 2,147,483,647|  
|数据库中的表|2^31-1 = 2,147,483,647|  
|表中的列|2 ^ 31-1 = 2147483647**警告：** 表中的总列数取决于与同一个表关联的度量值和计算列的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的行数|无限制**警告：** 限制为单个列不能包含超过1999999997个非重复值。|  
|表中的层次结构数|2^31-1 = 2,147,483,647|  
|层次结构中的级别数|2^31-1 = 2,147,483,647|  
|关系|2^31-1 = 2,147,483,647|  
|表中的键列|2^31-1 = 2,147,483,647|  
|表中的度量值|2 ^ 31-1 = 2147483647**警告：** 表中的度量值总数取决于与同一个表关联的列总数和计算列数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的计算列|2 ^ 31-1 = 2147483647**警告：** 表中的计算列总数取决于与同一个表关联的列和度量值的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|查询返回的单元数|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名称的长度|100 个字符|  
  
##  <a name="tabular-deploymentmode2"></a><a name="bkmk_vertipaq"></a>表格 (DeploymentMode = 2)   
  
|对象|最大大小/数量|  
|------------|----------------------------|  
|一个实例中的数据库数|2^31-1 = 2,147,483,647|  
|数据库中的表|2^31-1 = 2,147,483,647|  
|表中的列|2 ^ 31-1 = 2147483647**警告：** 表中的总列数取决于与同一个表关联的度量值和计算列的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的行数|无限制**警告：** 对于表中的单个列，不能包含超过1999999997个非重复值的限制。|  
|表中的层次结构数|2^31-1 = 2,147,483,647|  
|层次结构中的级别数|2^31-1 = 2,147,483,647|  
|关系|2^31-1 = 2,147,483,647|  
|表中的键列|2^31-1 = 2,147,483,647|  
|表中的度量值|2 ^ 31-1 = 2147483647**警告：** 表中的度量值总数取决于与同一个表关联的列总数和计算列数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|表中的计算列|2 ^ 31-1 = 2147483647**警告：** 表中的计算列总数取决于与同一个表关联的列和度量值的总数。 一个表中列数、度量值数和计算列数之和的最大数目为 2^31-1 = 2,147,483,647|  
|查询返回的单元数|2^31-1 = 2,147,483,647|  
|源查询的记录大小|64K|  
|对象名称的长度|100 个字符|  
  
## <a name="see-also"></a>另请参阅  
 [确定 Analysis Services 实例的服务器模式](../../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [常规属性](../../server-properties/general-properties.md)  
  
  
