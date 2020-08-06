---
title: 开发特定类型的数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3e168c866e03bfa5fd1f32127e4bfd6e58a2e8d5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691813"
---
# <a name="developing-specific-types-of-data-flow-components"></a>开发特定类型的数据流组件
  本节包括开发源组件、具有同步输出的转换组件、具有异步输出的转换组件以及目标组件的具体内容。  
  
 有关组件开发的常规信息，请参阅[开发自定义数据流组件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [开发自定义源组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 包含有关开发组件的信息，该组件访问外部数据源中的数据，并向该数据提供数据流中的下游组件。  
  
 [开发具有同步输出的自定义转换组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 包含有关开发其输出与输入同步的转换组件的信息。 这些组件不向数据流中添加数据，但处理通过该数据流的数据。  
  
 [开发具有异步输出的自定义转换组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 包含有关开发其输出与输入不同步的转换组件的信息。 这些组件接收来自上游组件的数据，但是也向数据流中添加数据。  
  
 [开发自定义目标组件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 包含有关开发组件的信息，该组件接收来自数据流上游组件的行，并将这些行写入外部数据源。  
  
## <a name="reference"></a>参考  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 包含用于创建自定义数据流组件的类和接口。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 包含数据流任务的非托管类和接口。 开发人员在以编程方式生成数据流或创建自定义数据流组件时，使用这些类和接口，以及托管 <xref:Microsoft.SqlServer.Dts.Pipeline> 命名空间。  
  
![Integration Services 图标 (小型) ](../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [比较脚本解决方案和自定义对象](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [开发特定类型的脚本组件](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
