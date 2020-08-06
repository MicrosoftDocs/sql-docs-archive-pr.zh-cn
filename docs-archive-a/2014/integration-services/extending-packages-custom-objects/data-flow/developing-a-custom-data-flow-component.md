---
title: 开发自定义数据流组件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7126129ede3f419c6fbdcae6245a47636e6e65ed
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690763"
---
# <a name="developing-a-custom-data-flow-component"></a>开发自定义数据流组件
  数据流任务由一些组件组成，这些组件用于连接各种数据源，然后快速转换和路由数据。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 提供一个可扩展的对象模型，该模型允许开发人员创建可在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 和已部署的包中使用的自定义源、转换和目标。 本节包含的主题将指导您开发自定义数据流组件。

## <a name="in-this-section"></a>本节内容
 [创建自定义数据流组件](creating-a-custom-data-flow-component.md)介绍创建自定义数据流组件的初始步骤。

 数据流[组件的设计时方法](design-time-methods-of-a-data-flow-component.md)描述要在自定义数据流组件中实现的设计时方法。

 数据流[组件的运行时方法](run-time-methods-of-a-data-flow-component.md)描述要在自定义数据流组件中实现的运行时方法。

 [执行计划和缓冲区分配](execution-plan-and-buffer-allocation.md)介绍数据流执行计划和数据缓冲区分配。

 使用数据流[中的数据类型](working-with-data-types-in-the-data-flow.md)说明数据流如何将 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 数据类型映射到 .NET Framework 托管数据类型。

 [验证数据流组件](validating-a-data-flow-component.md)说明用于验证组件配置和重新配置组件元数据的方法。

 [实现外部元数据](implementing-external-metadata.md)说明如何使用外部元数据列进行数据验证。

 [在数据流组件中引发和定义事件](raising-and-defining-events-in-a-data-flow-component.md)介绍如何引发预定义事件和自定义事件。

 [在数据流组件中记录和定义日志条目](logging-and-defining-log-entries-in-a-data-flow-component.md)说明如何创建和写入自定义日志项。

 [在数据流组件中使用错误输出](using-error-outputs-in-a-data-flow-component.md)说明如何将错误行重定向到其他输出。

 [升级数据流组件的版本](upgrading-the-version-of-a-data-flow-component.md)说明如何在首次使用组件的新版本时更新已保存的组件元数据。

 [为数据流组件开发用户界面](developing-a-user-interface-for-a-data-flow-component.md)说明如何实现组件的自定义编辑器。

 [开发特定类型的数据流组件](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)介绍如何开发这三种类型的数据流组件：源、转换和目标。

## <a name="reference"></a>参考
 <xref:Microsoft.SqlServer.Dts.Pipeline>包含用于创建自定义数据流组件的类和接口。

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>包含组成数据流任务对象模型的类和接口，用于创建自定义数据流组件或生成数据流任务。

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>包含用于创建数据流组件的用户界面的类和接口。

 [Integration Services 错误和消息引用](../../integration-services-error-and-message-reference.md)列出预定义的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 错误代码及其符号名称和说明。

## <a name="related-sections"></a>相关章节

### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：

 [开发 Integration Services 的自定义对象](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)介绍实现的所有类型自定义对象的基本步骤 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 。

 [持久保存自定义对象](../../extending-packages-custom-objects/persisting-custom-objects.md)描述自定义持久性，并在必要时对其进行说明。

 [生成、部署和调试自定义对象](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)介绍用于生成、签名、部署和调试自定义对象的方法。

### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息
 有关可在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的其他自定义对象类型的信息，请参阅以下主题：

 [开发自定义任务](../../extending-packages-custom-objects/task/developing-a-custom-task.md)讨论如何对自定义任务进行编程。

 [开发自定义连接管理器](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)讨论如何对自定义连接管理器进行编程。

 [开发自定义日志提供程序](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)讨论如何对自定义日志提供程序进行编程。

 [开发自定义 ForEach 枚举器](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)讨论如何对自定义枚举器进行编程。

![Integration Services 图标 (小型) ](../../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。

## <a name="see-also"></a>另请参阅
 [用脚本组件扩展数据流] (。/..[比较脚本解决方案和自定义对象的](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md


