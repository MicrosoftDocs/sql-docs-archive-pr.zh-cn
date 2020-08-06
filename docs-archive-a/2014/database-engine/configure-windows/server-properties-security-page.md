---
title: 服务器属性（“安全性”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5f45c0a04a0d7cc627901d8de24175f1d63a99fe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591581"
---
# <a name="server-properties-security-page"></a>服务器属性（“安全性”页）
  使用此页可以查看或修改服务器安全选项。  
  
## <a name="server-authentication"></a>服务器身份验证  
 **Windows 身份验证模式**  
 使用 Windows 身份验证对所尝试的连接进行验证。 更改安全模式时，如果 **sa** 密码为空白，系统就会提示用户输入 **sa** 密码。  
  
> [!IMPORTANT]  
>  Windows 身份验证比 SQL Server 身份验证更加安全。 请尽量使用 Windows 身份验证。  
  
 **SQL Server 和 Windows 身份验证模式**  
 使用混合模式的身份验证对所尝试的连接进行验证，以便向后兼容早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 更改安全模式时，如果 **sa** 密码为空白，系统就会提示用户输入 **sa** 密码。  
  
> [!NOTE]  
>  更改安全性配置后需要重新启动服务。 将服务器身份验证改为 SQL Server 和 Windows 身份验证模式时，不会自动启用 SA 帐户。 若要使用 SA 帐户，请执行带有 ENABLE 选项的 [ALTER LOGIN](/sql/t-sql/statements/alter-login-transact-sql) 命令。  
  
## <a name="login-auditing"></a>登录审核  
 无  
 关闭登录审核。  
  
 **仅限失败的登录**  
 仅审核未成功的登录。  
  
 **仅限成功的登录**  
 仅审核成功的登录。  
  
 **成功和失败的登录**  
 审核所有登录尝试。  
  
> [!NOTE]  
>  更改审核级别后需要重新启动服务。  
  
## <a name="server-proxy-account"></a>服务器代理帐户  
 **启用服务器代理帐户**  
 启用供 **xp_cmdshell**使用的帐户。 在执行操作系统命令时，代理帐户可模拟登录、服务器角色和数据库角色。  
  
> [!CAUTION]  
>  服务器代理帐户所用的登录帐户应该只具有执行既定工作所需的最低权限。 代理帐户的权限过大有可能会被恶意用户利用，从而危及系统安全。  
  
 **代理帐户**  
 指定所使用的代理帐户。  
  
 **密码**  
 指定代理帐户的密码。  
  
## <a name="options"></a>选项  
 **启用 C2 审核跟踪**  
 审核对语句和对象的所有访问尝试，并记录到文件中，对于默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，该文件位于 \MSSQL\Data 目录中，对于*命名实例，该文件位于 \MSSQL$* instancename [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Data 目录中。 有关详细信息，请参阅 [c2 审核模式服务器配置选项](c2-audit-mode-server-configuration-option.md)。  
  
 **跨数据库所有权链接**  
 选中此项将允许数据库成为跨数据库所有权链的源或目标。 有关详细信息，请参阅 [跨数据库所有权链接服务器配置选项](cross-db-ownership-chaining-server-configuration-option.md)。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
