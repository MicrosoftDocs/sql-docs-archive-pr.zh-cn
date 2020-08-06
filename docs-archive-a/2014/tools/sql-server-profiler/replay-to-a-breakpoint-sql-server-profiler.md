---
title: 重播到 (SQL Server Profiler) 的断点 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
author: stevestein
ms.author: sstein
ms.openlocfilehash: f33b6862847b042a2613d8c2aa035dd5805493ca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692024"
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>重播到断点 (SQL Server Profiler)
  本主题说明如何在您要通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]进行重播的跟踪文件或表中设置断点。 在重播跟踪之前，在跟踪文件或表中设置断点可以使您在发生特定事件时暂停重播跟踪。 在重播跟踪时使用断点能够支持调试，因为您可以将长跟踪脚本的重播分解为较短的段以便进行增量分析。  
  
### <a name="to-replay-to-a-breakpoint"></a>重播到断点  
  
1.  打开要重播的跟踪文件或跟踪表。 有关详细信息，请参阅 [打开跟踪文件 (SQL Server Profiler)](open-a-trace-file-sql-server-profiler.md) 或 [打开跟踪表 (SQL Server Profiler)](open-a-trace-table-sql-server-profiler.md)一起提供的预定义优化模板。  
  
     请确保打开的跟踪文件或跟踪表包含重播所需的事件类。 有关详细信息，请参阅 [Replay Requirements](replay-requirements.md)。  
  
2.  在跟踪窗口中，单击要用作断点的事件。 可以使用以下三种方法来设置断点：  
  
    -   按 F9。  
  
    -   在 **“重播”** 菜单上，单击 **“切换断点”** 。  
  
    -   右键单击“事件”，再单击“切换断点”  。  
  
     选定跟踪事件的旁边将显示一个红色项目符号，表示其为跟踪断点。  
  
     重复此步骤可以设置多个断点。  
  
3.  在 **“重播”** 菜单上，单击 **“启动”** ，然后连接到要重播跟踪的服务器。  
  
4.  在 **“重播配置”** 对话框中，验证设置，再单击 **“确定”** 。  
  
     将启动重播，并在到达断点时暂停。  
  
5.  按 F5 可恢复重播并继续运行直到下一个断点。  
  
6.  重复步骤 5 到跟踪的末尾。  
  
## <a name="see-also"></a>另请参阅  
 [重播至光标处 (SQL Server Profiler)](replay-to-a-cursor-sql-server-profiler.md)   
 [重播跟踪](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
