---
title: 删除一个或多个作业 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 436625f9ad629a6b0e574aa046059f4e7e9c2bf2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578006"
---
# <a name="delete-one-or-more-jobs"></a>删除一个或多个作业
  本主题说明如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、或 SQL Server 管理对象在中删除代理作业 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 除非你是 **sysadmin** 固定服务器角色的成员，否则只能删除自己拥有的作业。  
  
 
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>删除作业  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  依次展开“SQL Server 代理”**** 和“作业”****，右键单击要删除的作业，再单击“删除”****。  
  
3.  在“删除对象”**** 对话框中，确认选择了要删除的作业。  
  
4.  单击“确定”  。  
  
#### <a name="to-delete-multiple-jobs"></a>删除多个作业  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**。  
  
3.  右键单击“作业活动监视器”****，然后单击“查看作业活动”****。  
  
4.  在作业活动监视器中，选择要删除的作业，右键单击选择的作业，然后选择“删除作业”****。  
  

  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-job"></a>删除作业  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_delete_job ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)。  

##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  

### <a name="to-delete-multiple-jobs"></a>删除多个作业
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `JobCollection` 类。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
