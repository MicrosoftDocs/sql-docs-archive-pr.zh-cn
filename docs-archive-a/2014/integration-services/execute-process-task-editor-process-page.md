---
title: 执行进程任务编辑器 (进程页) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executeprocesstask.process.f1
helpviewer_keywords:
- Execute Process Task Editor
ms.assetid: 0fc22406-e79b-47a4-a7e4-108d4ce6202f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ce8629be2c07ae4caac4586b266936a908e71499
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682361"
---
# <a name="execute-process-task-editor-process-page"></a>执行进程任务编辑器（“进程”页）
  可以使用 **“执行进程任务编辑器”** 对话框的 **“进程”** 页配置执行进程的选项。 这些选项包括要运行的可执行文件、该可执行文件的位置、命令提示符参数以及提供输入及捕获输出的变量。  
  
 若要了解此任务，请参阅 [Execute Process Task](control-flow/execute-process-task.md)。  
  
## <a name="options"></a>选项  
 **RequireFullFileName**  
 指示在指定位置未找到可执行文件时该任务是否应失败。  
  
 **可执行文件**  
 键入要运行的可执行文件的名称。  
  
 **参数**  
 提供命令提示符参数。  
  
 **WorkingDirectory**  
 键入包含可执行文件的文件夹的路径，或单击浏览 (…) 按钮定位到该文件夹  。  
  
 **StandardInputVariable**  
 选择为进程提供输入的变量，或单击 \<**New variable...**> 创建新的变量：  
  
 **相关主题：**  [添加变量](../../2014/integration-services/add-variable.md)  
  
 **StandardOutputVariable**  
 选择捕获进程输出的变量，或单击 \<**New variable...**> 创建新的变量。  
  
 **StandardErrorVariable**  
 选择捕获处理器的错误输出的变量，或单击 \<**New variable...**> 创建新的变量。  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 指示在进程退出代码与 **SuccessValue**中指定的值不同时任务是否失败。  
  
 **SuccessValue**  
 指定可执行文件返回的用来指示进程成功的值。 默认情况下，此值设置为 **0**。  
  
 **TimeOut**  
 指定进程可以运行的秒数。 如果值为 **0** ，则表示不使用超时值，进程一直运行到处理完毕或出错为止。  
  
 **TerminateProcessAfterTimeOut**  
 指示在 **TimeOut** 选项指定的超时期限过后是否强制结束进程。 只有在 **TimeOut** 不为 **0**时，此选项才可用。  
  
 **WindowStyle**  
 指定用于运行进程的窗口样式。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
