---
title: 开发自定义日志提供程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88d4f70fa9d50628b831b56f9fa22100648fce51
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578361"
---
# <a name="developing-a-custom-log-provider"></a>开发自定义日志提供程序
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 所具有的广泛的日志记录功能使其可捕获在包执行过程中发生的事件。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包含各种日志提供程序，可用于创建日志并以 XML、文本、数据库或 Windows 事件日志等格式存储这些日志。 如果提供的日志提供程序和输出格式不能完全满足您的需要，您可以创建自定义日志提供程序。

 若要创建自定义日志提供程序，必须创建从 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基类继承的类，再将 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 属性应用到新类，然后重写基类的重要方法和属性，包括 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 属性和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法。

## <a name="in-this-section"></a>本节内容
 本节介绍如何创建、配置和编写自定义日志提供程序代码。

 [创建自定义日志提供程序](creating-a-custom-log-provider.md)介绍如何为自定义日志提供程序项目创建类。

 [编写自定义日志提供程序代码](coding-a-custom-log-provider.md)介绍如何通过重写基类的方法和属性实现自定义日志提供程序。

 [为自定义日志提供程序开发用户界面](developing-a-user-interface-for-a-custom-log-provider.md)中不支持自定义日志提供程序的自定义用户界面 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 。

## <a name="related-topics"></a>相关主题

### <a name="information-common-to-all-custom-objects"></a>所有自定义对象的通用信息
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的所有类型自定义对象的通用信息，请参阅以下主题：

 [开发 Integration Services 的自定义对象](../developing-custom-objects-for-integration-services.md)介绍实现的所有类型自定义对象的基本步骤 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 。

 [持久保存自定义对象](../persisting-custom-objects.md)描述自定义持久性，并在必要时对其进行说明。

 [生成、部署和调试自定义对象](../building-deploying-and-debugging-custom-objects.md)介绍用于生成、签名、部署和调试自定义对象的方法。

### <a name="information-about-other-custom-objects"></a>其他自定义对象的信息
 有关可在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中创建的其他自定义对象类型的信息，请参阅以下主题：

 [开发自定义任务](../task/developing-a-custom-task.md)讨论如何对自定义任务进行编程。

 [开发自定义连接管理器](../connection-manager/developing-a-custom-connection-manager.md)讨论如何对自定义连接管理器进行编程。

 [开发自定义 ForEach 枚举器](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)讨论如何对自定义枚举器进行编程。

 [开发自定义数据流组件](../data-flow/developing-a-custom-data-flow-component.md)讨论如何对自定义数据流源、转换和目标进行编程。

![Integration Services 图标 (小型) ](../../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。


