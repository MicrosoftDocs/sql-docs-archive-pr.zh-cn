---
title: SQL Server 代理属性（“登录”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 01fc6329-5d6b-4186-9565-395f375477bb
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd899e8824adacd07fa1d8d7d51b2143d10cadd4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586033"
---
# <a name="sql-server-agent-properties-log-on-tab"></a>SQL Server 代理属性（“登录”选项卡）
  使用 **“SQL Server 代理属性”** 对话框中的 **“登录”** 选项卡，可以指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务使用的帐户，还可以启动和停止该服务。 对帐户密码的更改立即生效，无需重新启动服务。  
  
> [!NOTE]  
>  更改群集实例的服务使用的帐户名时，新帐户必须是安装期间为待更改服务指定的域组的成员，或者您必须具有向该组添加成员的权限。 如果您无权修改组成员身份，请与域管理员联系。  
  
## <a name="options"></a>选项  
 **本地系统帐户**  
 指定一个不要求输入密码的本地系统帐户。 不过，本地系统帐户可能会限制该服务与其他服务器进行交互，具体取决于该帐户所拥有的权限。  
  
 **本帐户**  
 指定一个使用 Windows 身份验证的本地用户帐户或域用户帐户。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议使用具有最低服务权限的域用户帐户。 有关选择帐户的信息，请在联机丛书中搜索“设置 Windows 服务帐户”。  
  
 **帐户名**  
 指定本地用户帐户名或域用户帐户名。  
  
 **密码**  
 键入帐户的密码。  
  
 **确认密码**  
 再次键入帐户的密码。  
  
 **启动**  
 启动服务。  
  
 **Stop**  
 停止服务。  
  
 **暂停**  
 暂停服务。  
  
 **恢复**  
 恢复暂停的服务。  
  
  
