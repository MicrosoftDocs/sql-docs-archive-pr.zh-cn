---
title: 管理工具命令行选项（Distributed Replay 实用工具）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 506be071f44937d82902585e5a0621212083dfa5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587657"
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>管理工具命令行选项（分布式重播实用工具）
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 管理工具 `DReplay.exe` 是一个命令行工具，可用于与 Distributed Replay 控制器进行通信。 可使用此管理工具在控制器上启动、监视和取消操作。  
  
 ![主题链接图标](../../database-engine/media/topic-link.gif "“主题链接”图标") 有关与此管理工具语法结合使用的语法约定的详细信息，请参阅 [Transact-SQL 语法约定 (Transact-SQL)](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql)。  
  
## <a name="syntax"></a>语法  
  
```  
  
      dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-mcontroller] -iinput_trace_file  
    -dcontroller_working_dir [-cconfig_file] [-fstatus_interval]  
  
  dreplay replay [-mcontroller] -dcontroller_working_dir [-o]  
    [-starget_server] -wclients [-cconfig_file]  
    [-fstatus_interval]  
  
  dreplay status [-mcontroller] [-fstatus_interval]  
  
  dreplay cancel [-mcontroller] [-q]   
```  
  
## <a name="remarks"></a>备注  
 您可以使用 `DReplay.exe` 发出以下命令行选项：  
  
 **preprocess**  
 启动预处理阶段。 控制器准备您从生产环境中捕获的输入跟踪数据，以便对目标服务器进行重播。  
  
 **replay**  
 启动事件重播阶段。 控制器将重播数据调度到指定客户端，启动分布式重播并同步客户端。 每个选定的客户端可以选择记录重播活动并在本地保存结果跟踪文件。  
  
 **status**  
 查询控制器并显示当前状态。  
  
 **cancel**  
 取消正在控制器上运行的当前操作。  
  
 对于包含命令参数和示例的详细语法信息，请参阅下列主题：  
  
-   [预处理选项（分布式重播管理工具）](preprocess-option-distributed-replay-administration-tool.md)  
  
-   [重播选项（分布式重播管理工具）](replay-option-distributed-replay-administration-tool.md)  
  
-   [状态选项（分布式重播管理工具）](status-option-distributed-replay-administration-tool.md)  
  
-   [取消选项（分布式重播管理工具）](cancel-option-distributed-replay-administration-tool.md)  
  
 RPC 将作为 RPC 而非语言事件进行重播。  
  
## <a name="permissions"></a>权限  
 您必须作为交互用户、本地用户或域用户帐户运行管理工具。 若要使用本地用户帐户，管理工具和控制器必须在同一台计算机上运行。  
  
 有关详细信息，请参阅 [Distributed Replay Security](distributed-replay-security.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 分布式重播](sql-server-distributed-replay.md)  
  
  
