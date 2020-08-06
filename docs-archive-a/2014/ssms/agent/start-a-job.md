---
title: 启动作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4d5af895df518a915dacd953331b9139471933aa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692084"
---
# <a name="start-a-job"></a>启动作业
  本主题说明如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理对象在中开始运行代理作业 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 作业是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的一系列指定操作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业可以在一个本地服务器上运行，也可以在多个远程服务器上运行。  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要启动作业，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
### <a name="to-start-a-job"></a>启动作业  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”** ，再展开 **“作业”**。 根据您希望作业以何种方式启动，执行下列操作之一：  
  
    -   如果使用的是单台服务器或目标服务器，或者正在一台主服务器上运行一个本地服务器作业，请右键单击要启动的作业，然后单击“启动作业”****。  
  
    -   若要启动多个作业，请右键单击“作业活动监视器”****，然后单击“查看作业活动”****。 在作业活动监视器中，可以选择多个作业，右键单击所选作业，再单击“启动作业”****。  
  
    -   如果使用的是主服务器并且希望所有目标服务器同时运行作业，请右键单击要启动的作业、单击“启动作业”****，然后单击“在所有目标服务器上启动”****。  
  
    -   如果使用的是主服务器并且希望指定运行作业的目标服务器，请右键单击要启动的作业、单击“启动作业”****，然后单击“在特定的目标服务器上启动”****。 在 **“发布下载指令”** 对话框中，选中 **“以下目标服务器”** 复选框，然后选择运行该作业的每台目标服务器。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
### <a name="to-start-a-job"></a>启动作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```sql
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 有关详细信息，请参阅 [sp_start_job (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  

### <a name="to-start-a-job"></a>启动作业
  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 `Start` 类的 `Job` 方法。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
