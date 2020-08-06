---
title: 配置度量值属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7ca291a5181fdb3f7a88845431d61ffd7a1034eb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691982"
---
# <a name="configure-measure-properties"></a>配置度量值属性
  通过使用度量值的属性，您可以定义度量值的工作方式并控制如何向用户显示度量值。  
  
 当创建或编辑多维数据集或度量值时可在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中设置属性。 你还可以编程方式（用 MDX 或 AMO）设置它们。 有关详细信息，请参阅[在多维模型中创建度量值和度量值组](create-measures-and-measure-groups-in-multidimensional-models.md)、[CREATE MEMBER 语句 (MDX)](/sql/mdx/mdx-data-definition-create-member) 或 [AMO OLAP 基本对象的编程](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects)。  
  
## <a name="measure-properties"></a>度量值属性  
 度量值从其所属的度量值组中继承某些属性，除非这些属性在度量值级别被覆盖。 度量值属性确定度量值的聚合方式、它的数据类型、对用户的显示名称、度量值将在其中出现的显示文件夹、它的格式字符串、任何度量值表达式、基础源列和它对用户的可见性。  
  
|属性|定义|  
|--------------|----------------|  
|`AggregateFunction`|必需。 确定度量值的聚合方式。 `Sum` 是默认聚合。 有关详细信息，请参阅针对每个函数说明的 [Use Aggregate Functions](use-aggregate-functions.md) 。|  
|`DataType`|必需。 指定与度量值绑定的基础事实数据表中的列的数据类型。 默认情况下，此值从源列继承。|  
|`Description`|提供度量值的说明，可以在客户端应用程序中显示该说明。|  
|`DisplayFolder`|指定当用户连接到多维数据集时度量值将在其中显示的文件夹。 多维数据集有很多度量值时，可以使用显示文件夹来对度量值进行分类，从而改善用户的浏览体验。|  
|`FormatString`|通过使用度量值的 `FormatString` 属性，可以选择用于向用户显示度量值的格式。<br /><br /> 虽然 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中提供了显示格式的列表，但你仍可以指定多个该列表中没有的其他格式。 您可以指定在 Microsoft Visual Basic 中有效的任何命名格式或用户定义格式。|  
|`ID`|必需。 显示度量值的唯一标识符 (ID)。 此属性是只读的。|  
|`MeasureExpression`|指定定义度量值的值的受约束的 MDX 表达式。 表达式在聚合之前在叶级进行求值，并且允许对值设置权重。 例如，在货币转换中，销售额按汇率加权。|  
|`Name`|必需。 指定度量值的名称。|  
|`Source`|必需。 指定与度量值绑定的数据源视图中的列。 请参阅[数据源和绑定（SSAS 多维）](data-sources-and-bindings-ssas-multidimensional.md)。|  
|`Visible`|确定客户端应用程序中度量值的可见性。|  
  
## <a name="see-also"></a>另请参阅  
 [配置度量值组属性](configure-measure-group-properties.md)   
 [修改度量值](../lesson-3-1-modifying-measures.md)  
  
  
