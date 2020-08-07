---
title: 完成安装后步骤 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 0a788a2a-9b4f-4bfc-b1b5-83eeb1ea9ab2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1e9aae3dccaa409bcebc473213286f3edf19e7f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587655"
---
# <a name="complete-the-post-installation-steps"></a>完成安装后步骤
  安装 Distributed Replay 后，您必须修改 Distributed Replay 控制器和客户端服务帐户。  
  
### <a name="to-complete-the-post-installation-steps"></a>完成安装后步骤  
  
1.  **创建防火墙规则**：在控制器和客户端计算机上，必须允许相应服务的入站流量通过防火墙。 指定位于安装文件夹中的服务可执行文件的防火墙规则。  
  
    1.  对于控制器服务，请为位于安装文件夹中的 **DReplayController.exe**创建规则。 例如，下面的命令会启用该规则，其中 `%InstallPath%` 是服务的安装文件夹：  
  
         `netsh advfirewall firewall add rule name="allow dreplay controller" dir=in program="%InstallPath%\DReplayController\DReplayController.exe" action=allow`  
  
    2.  对于客户端服务，请在每台客户端计算机上为位于安装文件夹中的 **DReplayClient.exe**创建规则。 例如，下面的命令会启用该规则，其中 `%InstallPath%` 是服务的安装文件夹：  
  
         `netsh advfirewall firewall add rule name="allow dreplay client" dir=in program="%InstallPath%\DReplayClient\DReplayClient.exe" action=allow`  
  
2.  **在目标服务器上授予每个客户端权限**：在客户端计算机上安装完客户端服务后，必须手动将客户端服务帐户添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目标实例上的 sysadmin 角色中。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您必须具有管理权限才能安装任何 Distributed Replay 功能。 只有拥有 sysadmin 权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名才可以将客户端服务帐户添加到测试服务器的 sysadmin 服务器角色中。 有关分布式重播的安全注意事项的详细信息，请参阅 [Distributed Replay Security](distributed-replay-security.md)。  
  
  
