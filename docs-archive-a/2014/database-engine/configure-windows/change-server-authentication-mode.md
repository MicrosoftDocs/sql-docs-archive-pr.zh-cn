---
title: 更改服务器身份验证模式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8bda31ca7d0c5949173a9a3e5ea656c1757c04f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693097"
---
# <a name="change-server-authentication-mode"></a>更改服务器身份验证模式
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中更改服务器身份验证模式。 安装过程中， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 设置为 **“Windows 身份验证模式”** 或 **“SQL Server 和 Windows 身份验证模式”** 。 安装完成后，您可以随时更改身份验证模式。  
  
 如果在安装过程中选择了“Windows 身份验证模式”，则 sa 登录名将被禁用，安装程序会分配一个密码。 如果稍后将身份验证模式更改为“SQL Server 和 Windows 身份验证模式”，则 sa 登录名仍处于禁用状态。 若要使用 sa 登录名，请使用 ALTER LOGIN 语句启用 sa 登录名并分配一个新密码。 sa 登录名只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到服务器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要更改服务器身份验证模式，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 sa 帐户是一个广为人知的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户，并且经常成为恶意用户的攻击目标。 除非您的应用程序需要使用 sa 帐户，否则请不要启用它。 为 sa 登录名使用一个强密码非常重要。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>更改安全身份验证模式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对象资源管理器中，右键单击服务器，再单击“属性”。  
  
2.  在 **“安全性”** 页上的 **“服务器身份验证”** 下，选择新的服务器身份验证模式，再单击 **“确定”** 。  
  
3.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 对话框中，单击 **“确定”** 以确认需要重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
4.  在“对象资源管理器”中，右键单击服务器，并单击“重新启动”。 如果运行有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理，则也必须重新启动该代理。  
  
#### <a name="to-enable-the-sa-login"></a>启用 sa 登录名  
  
1.  在对象资源管理器中，展开 "**安全性**"，展开 "登录名"，右键单击 `sa` ，然后单击 "**属性**"。  
  
2.  在 **“常规”** 页上，您可能需要为登录名创建密码并确认该密码。  
  
3.  在 **“状态”** 页上的 **“登录”** 部分，单击 **“启用”** ，然后单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **启用 sa 登录名**  
  
1.  在“对象资源管理器”中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 下面的示例启用 sa 登录名并设置一个新密码。  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [强密码](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 安装的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [在系统管理员被锁定时连接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  
