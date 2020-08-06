---
title: Distributed Replay 客户端配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ccf03e32-6bd9-43c0-b9b6-9fe0d9163339
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 53124029483c25ed7894b279283e1de02c647350
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591104"
---
# <a name="distributed-replay-client-configuration"></a>Distributed Replay 客户端配置
  使用 **安装向导的** “Distributed Replay 客户端配置” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页可以指定您希望向其授予针对 Distributed Replay 客户端服务的管理权限的用户。  
  
 具有管理权限的用户将可以不受限制地访问 Distributed Replay 客户端服务。  
  
## <a name="options"></a>选项  
 **控制器名称**  
 这是一个可选参数，默认值为 \<*blank*> 。  
  
 输入客户端计算机将与 Distributed Replay 客户端服务进行通信的控制器的名称。 注意以下事项：  
  
-   名称必须为完全限定域名 (FQDN)。 例如，位于 Microsoft 的产品层次结构中名为 server1 的主机必须具有 server1.products.microsoft.com 的 FQDN。  
  
-   如果您已经设置了一个控制器，则在配置每个客户端时输入该控制器的名称。  
  
-   如果您尚未设置控制器，则可以将控制器名称保留为空。 但是，您必须在 **“客户端配置”** 文件中手动输入控制器名称。  
  
 **工作目录**  
 为 Distributed Replay 客户端服务指定工作目录。  
  
 默认工作目录为 \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\。  
  
 **默认目录**  
 为 Distributed Replay 客户端服务指定结果目录。  
  
 默认结果目录为 \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\。  
  
  
