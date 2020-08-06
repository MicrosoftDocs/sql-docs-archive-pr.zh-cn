---
title: 在脚本组件中使用变量 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4328a938c56ad8383c12cdae1d6511604ec65582
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691315"
---
# <a name="using-variables-in-the-script-component"></a>在脚本组件中使用变量
  变量存储包及其容器、任务和事件处理程序在运行时可以使用的值。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services-ssis-variables.md)。  
  
 您可以通过在 " `ReadOnlyVariables` `ReadWriteVariables` **脚本转换编辑器**" 的 "**脚本**" 页上的 "和" 字段中输入逗号分隔的变量列表，使现有变量可用于只读或读/写访问。 请注意，变量名称区分大小写。 使用 `Value` 属性可以从单个变量读取数据或向其中写入数据。 当脚本在运行时操作变量时，脚本组件将在后台处理任何所需的锁定。  
  
> [!IMPORTANT]  
>  `ReadWriteVariables` 集合仅供在 `PostExecute` 方法中尽可能优化性能并降低锁定冲突的风险。 因此不能在处理每行数据时直接递增包变量的值， 而应递增本地变量的值，并在所有数据处理完毕后，在 `PostExecute` 方法中将包变量的值设置为本地变量的值。 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性解决此限制问题，本主题稍后会进行介绍。 但是，在处理每一行时直接写包变量将会对性能产生负面影响，并增加锁定冲突的风险。  
  
 有关“脚本转换编辑器”的“脚本”页的详细信息，请参阅[在脚本组件编辑器中配置脚本组件](configuring-the-script-component-in-the-script-component-editor.md)和[脚本转换编辑器（“脚本”页）](../../script-transformation-editor-script-page.md) 。  
  
 脚本组件在 `Variables` 项目项中创建一个 `ComponentWrapper` 集合类，该集合类为每个预配置变量值包含一个强类型的取值函数属性，该属性与变量本身同名。 此集合通过 `Variables` 类的 `ScriptMain` 属性公开。 取值函数属性根据需要提供对变量值的只读或读/写权限。 例如，如果将名为 `MyIntegerVariable` 的整数变量添加到 `ReadOnlyVariables` 列表中，则可在脚本中使用以下代码检索该变量的值：  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 还可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性（通过调用 `Me.VariableDispenser` 进行访问）在脚本组件中使用变量。 在这种情况下，使用的不是变量的已命名类型化取值函数属性，而是直接访问这些变量。 使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 时，您必须在您自己的代码中处理锁定语义和变量值的数据类型转换。 如果要使用在设计时不可用，而是以编程方式在运行时创建的变量，则必须使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 属性，而不是已命名的类型化取值函数属性。  
  
![Integration Services 图标 (小型) ](../../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 变量](../../integration-services-ssis-variables.md)   
 [使用包中的变量](../../use-variables-in-packages.md)  
  
  
