---
title: 配置帐户以创建和管理 SQL Server 代理作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: stevestein
ms.author: sstein
ms.openlocfilehash: 83313389b3b872004fb23b0babdad19cfb5b8e7d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591072"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
  本主题介绍如何配置用户以创建或执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。  
  
-   **开始之前：** [安全性](#Security)  
  
-   **若要配置用户以创建和管理 SQL Server 代理作业，请使用：**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 若要配置用户以创建或执行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业，必须先将现有 SQL Server 登录名或 msdb 角色添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 数据库中的以下代理固定数据库角色之一： SQLAgentUserRole、SQLAgentReaderRole 或 SQLAgentOperatorRole。  
  
 默认情况下，这些数据库角色的成员可以创建各自的作业步骤，这些作业步骤不执行其他作业步骤。 如果这些非管理用户要运行那些执行其他作业步骤类型（例如， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包）的作业，它们需要对代理帐户具有访问权限。 sysadmin 固定服务器角色的所有成员都有创建、修改和删除代理帐户的权限。 有关与这些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色相关的权限的详细信息，请参阅 [SQL Server 代理固定数据库角色](sql-server-agent-fixed-database-roles.md)。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
 **将 SQL 登录帐户或 msdb 角色添加到 SQL Server 代理固定数据库角色**  
  
1.  在 **对象资源管理器**中，展开某个服务器。  
  
2.  展开 **“安全性”**，然后展开 **“登录名”**。  
  
3.  右键单击要添加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色的登录帐户，然后选择“属性”****。  
  
4.  在 "**登录属性**" 对话框的 "**用户映射**" 页上，选择包含的行 `msdb` 。  
  
5.  在 **“数据库角色成员身份: msdb”** 下，选中适当的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理固定数据库角色。  
  
 **配置代理帐户以创建和管理 SQL Server 代理作业步骤**  
  
1.  在 **对象资源管理器**中，展开某个服务器。  
  
2.  展开 **“SQL Server 代理”**。  
  
3.  右键单击“代理”****，再选择“新建代理”****。  
  
4.  在 **“新建代理帐户”** 对话框的 **“常规”** 页上，指定新代理的代理名称、凭据名称和说明。 请注意，在创建 SQL Server 代理的代理帐户之前，必须先创建一个凭据。 有关创建凭据的详细信息，请参阅[create a credential](../../relational-databases/security/authentication-access/create-a-credential.md)和[Create credential &#40;transact-sql&#41;](/sql/t-sql/statements/create-credential-transact-sql)。  
  
5.  检查此代理的相应子系统。  
  
6.  在 **“主体”** 页上，添加或删除登录名或角色，以授予或删除对代理帐户的访问权限。  
  
## <a name="see-also"></a>另请参阅  
 [实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)  
  
  
