---
title: 设置目标服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd60a19234d186bb0912978589fa60fd8e8a8c22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682660"
---
# <a name="make-a-target-server"></a>设置目标服务器
  本主题说明如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 管理对象 (SMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中生成目标服务器。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要生成目标服务器，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 如果分布式作业的步骤与某个代理相关联，则该作业将在目标服务器上该代理帐户的上下文下运行。 请确保满足以下条件，否则与代理关联的作业步骤将不会从主服务器下载到目标服务器上：  
  
-   主服务器注册表子项**\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server \\ < *instance_name*> \sql server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) 设置为 1 () 为 true。 默认情况下，此子项设置为 0 (False)。  
  
-   目标服务器上已存在与运行作业步骤的主服务器代理帐户同名的代理帐户。  
  
 从主服务器将使用代理帐户的作业步骤下载到目标服务器时，如果作业步骤失败，可以检查 **msdb** 数据库中 **sysdownloadlist** 表的 **error_message** 列是否存在以下错误消息：  
  
-   “该作业步骤需要代理帐户，但是目标服务器上禁用了代理匹配功能。”  
  
     若要解决此错误，请将 **AllowDownloadedJobsToMatchProxyName** 注册表子项设置为 1。  
  
-   “找不到代理。”  
  
     若要解决此错误，请确保目标服务器上已存在与运行作业步骤的主服务器代理帐户同名的代理帐户。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 默认情况下授予  固定服务器角色的成员执行此过程的权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>生成目标服务器  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”****，指向“多服务器管理”****，然后单击“使其成为目标服务器”****。 **“目标服务器向导”** 会指导您完成生成目标服务器的过程。  
  
3.  从 **“选择主服务器”** 页中，选择此目标服务器将从中接收作业的主服务器。  
  
     **选取服务器**  
     连接到主服务器。  
  
     **此服务器的说明**  
     键入此目标服务器的说明。 目标服务器将此说明上载到主服务器。  
  
4.  从 **“主服务器登录凭据”** 页中，在目标服务器上创建新的登录（如果需要）。  
  
     **在必要时创建新登录名，并为其分配针对 MSX 的权限**  
     如果指定的登录名不存在，则在目标服务器上创建新登录名。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>生成目标服务器  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 本示例将当前服务器登记到 AdventureWorks1 主服务器中。 当前服务器的位置是 Building 21、Room 309、Rack 5。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     有关详细信息，请参阅[&#40;transact-sql&#41;sp_msx_enlist ](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)。  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>使用 SQL Server 管理对象 (SMO)   
  
## <a name="see-also"></a>另请参阅  
 [企业范围的自动化管理](automated-administration-across-an-enterprise.md)  
