---
title: 脚本组件中的日志记录 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4c29dfffee6cacb39272aef07caa5539555cdd4c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587906"
---
# <a name="logging-in-the-script-component"></a>脚本组件中的日志记录
  使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包中的日志记录可以记录预定义的事件或用户定义的消息，从而将有关执行进度、结果和问题的详细信息保存下来，以供日后分析。 脚本组件可以使用 `ScriptMain` 类的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法记录用户定义的数据。 如果启用了日志记录，并且已选择 ScriptComponentLogEntry 事件登录“配置 SSIS 日志”对话框的“详细信息”选项卡，调用一次 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法会将事件信息存储在为数据流任务配置的所有日志提供程序中。  
  
 下面是一个简单的日志记录示例：  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  尽管可以直接从脚本组件执行日志记录，但是您可能希望考虑实现事件，而不是日志记录。 如果使用事件，不仅能够启用事件消息的日志记录，而且能够通过默认的或用户定义的事件处理程序响应事件。  
  
 有关日志记录的详细信息，请参阅 [Integration Services (SSIS) 日志记录](../../performance/integration-services-ssis-logging.md)。  
  
![Integration Services 图标 (小型) ](../../media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 日志记录](../../performance/integration-services-ssis-logging.md)  
  
  
