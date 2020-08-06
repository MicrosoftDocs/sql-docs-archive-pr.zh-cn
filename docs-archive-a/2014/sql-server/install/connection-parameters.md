---
title: 连接参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 27eb69dfd2c41710a47861e0992486267f692a3a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579977"
---
# <a name="connection-parameters"></a>连接参数
  若要分析某些服务器类型（比如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]），则必须选择具体的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 会自动选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例。 您可以更改此选择，但一次只能选择一个实例供升级顾问分析。 如果包括了要求身份验证的服务器类型，则必须输入身份验证模式和凭据。  
  
## <a name="options"></a>选项  
 **服务器名称**  
 使用您在“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件”窗格中输入的计算机名进行预填充。  
  
 **实例名**  
 从计算机中可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中进行选择。 如果看不到实例列表，请使用 MSSQLSERVER 扫描默认实例。 这对于远程计算机来说尤其重要。 也可以使用单词“default”来扫描默认实例。  
  
 **身份验证**  
 从此计算机上可用的身份验证模式列表中进行选择。 默认情况下，身份验证模式为 Windows 身份验证。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请在框中输入用户名。 建议该用户名具有计算机上的管理凭据。  
  
> [!NOTE]  
>  如果选择 "Windows 身份验证"，则将在 "**用户名**" 文本框中填充当前登录用户的用户名。  
  
 **密码**  
 输入指定用户的密码。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
