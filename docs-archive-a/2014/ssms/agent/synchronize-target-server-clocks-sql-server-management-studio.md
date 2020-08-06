---
title: 同步目标服务器时钟 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- clocks [SQL Server]
- master servers [SQL Server], clock synchronization
- synchronization [SQL Server], target server clocks
- target servers [SQL Server], clock synchronization
ms.assetid: 4fb80502-d271-4d06-bcbc-bfbbceb5f2a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8e7150cd42699503ab22cdd89fb6206194bd64e1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682652"
---
# <a name="synchronize-target-server-clocks-sql-server-management-studio"></a>Synchronize Target Server Clocks (SQL Server Management Studio)
  本主题介绍了如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中使目标服务器时钟与主服务器时钟同步。 同步这些系统时钟可以为实现您的作业计划提供支持。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要同步目标服务器的时钟，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-synchronize-target-server-clocks"></a>同步目标服务器的时钟  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开要使目标服务器时钟与主服务器时钟同步的服务器。  
  
2.  右键单击“SQL Server 代理”****，指向“多服务器管理”****，然后选择“管理目标服务器”****。  
  
3.  在 **“管理目标服务器”** 对话框中，单击 **“发布指令”**。  
  
4.  在 **“指令类型”** 列表中，选择 **“同步时钟”**。  
  
5.  在 **“收件人”** 下，执行以下操作之一：  
  
    -   单击 **“所有目标服务器”** 使所有目标服务器时钟与主服务器时钟同步。  
  
    -   单击 **“以下目标服务器”** 同步某些特定的服务器时钟，然后选择要使其时钟与主服务器时钟同步的每台目标服务器。  
  
6.  完成后，单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-synchronize-target-server-clocks"></a>同步目标服务器的时钟  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```  
    USE msdb ;  
    GO  
    -- resynchronizes the SEATTLE1 target server  
    EXEC dbo.sp_resync_targetserver  
        N'SEATTLE1' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_resync_targetserver ](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)。  
  
  
