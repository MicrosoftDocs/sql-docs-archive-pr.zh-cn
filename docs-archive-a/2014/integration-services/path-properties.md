---
title: 路径属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca263b866fb6d5d7ceb6352f708f387d79cad4f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578288"
---
# <a name="path-properties"></a>路径属性
  对象模型中的数据流对象在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 组件、输入和输出以及输入列和输出列的级别上具有通用属性和自定义属性。 其中许多属性的值是只读的，由数据流引擎在运行时分配。  
  
 本主题列出并描述了连接数据流对象的路径的自定义属性。  
  
## <a name="path-properties"></a>路径属性  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型中，数据流中连接组件的路径实现 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 接口。  
  
 下表介绍了数据流中路径的可配置属性。 数据流引擎还为此处未列出的其他只读属性赋值。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer（枚举）|用于指示在设计器图面上显示路径时是否应显示批注的值。 可能的值为 `AsNeeded`、`SourceName`、`PathName` 和 `Never`。 默认值为 `AsNeeded`。|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|与路径关联的输入。|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|与路径关联的输出。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 路径](data-flow/integration-services-paths.md)   
 [通用属性](../../2014/integration-services/common-properties.md)   
 [转换自定义属性](data-flow/transformations/transformation-custom-properties.md)   
 [可以使用表达式设置的数据流属性](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
