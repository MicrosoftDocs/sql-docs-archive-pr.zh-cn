---
title: 数据库维度属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- metadata [Analysis Services]
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 075548ef-08a3-413c-8ee0-4a074c276fcc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 504e190f4c513a8c999c4d7d7ab9eaabb83298c3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588729"
---
# <a name="database-dimension-properties"></a>数据库维度属性
  在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，维度的特征是由维度的元数据根据各种维度属性的设置以及维度所包含的属性或层次结构来定义的。 下表说明了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的维度属性。  
  
|属性|说明|  
|--------------|-----------------|  
|`AttributeAllMemberName`|指定维度中属性的“全部”成员的名称。|  
|`Collation`|确定维度使用的排序规则。|  
|`CurrentStorageMode`|包含维度的当前存储模式。|  
|`DependsOnDimension`|包含维度所依赖的其他维度的 ID（如果有的话）。|  
|`Description`|包含维度的说明。|  
|`ErrorConfiguration`|可配置的错误处理设置，用于处理重复键、未知键、错误限制以及检测到错误执行的操作、错误日志文件和空键处理。|  
|`ID`|包含维度的唯一标识符 (ID)。|  
|`Language`|指定维度的默认语言。|  
|`MdxMissingMemberMode`|确定如何处理多维表达式 (MDX) 语句中缺少的成员。|  
|`MiningModelID`|包含数据挖掘维度所关联的挖掘模型的 ID。 此属性仅适用于挖掘模型维度。|  
|`Name`|指定维度的名称。|  
|`ProactiveCaching`|定义维度的主动缓存设置。|  
|`ProcessingGroup`|指定处理组。 值为 ByAttribute 或 ByTable。 默认值为 `ByAttribute`。|  
|`ProcessingMode`|指示是否应该在处理期间或处理之后对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进行聚合以及为其建立索引。|  
|`ProcessingPriority`|确定在后台操作期间（例如惰性聚合、索引或群集）维度的处理优先级。|  
|`Source`|标识维度绑定到的数据源视图。|  
|`StorageMode`|确定维度的存储模式。|  
|`Type`|指定维度的类型。|  
|`UnknownMember`|指示未知成员是否可见。|  
|`UnknownMemberName`|指定维度未知成员的标题，以维度的默认语言显示。|  
|`WriteEnabled`|指示维度写回是否可用（视安全权限而定）。|  
  
> [!NOTE]  
>  有关在处理 null 值和其他数据完整性问题时设置 ErrorConfiguration 和 UnknownMember 属性的值的详细信息，请参阅[处理 Analysis Services 2005 中的数据完整性问题](https://go.microsoft.com/fwlink/?LinkId=81891)。  
  
## <a name="see-also"></a>另请参阅  
 [属性和属性层次结构](attributes-and-attribute-hierarchies.md)   
 [用户层次结构](user-hierarchies.md)   
 [维度关系](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [维度（Analysis Services - 多维数据）](dimensions-analysis-services-multidimensional-data.md)  
  
  
