---
title: 将作业状态写入 Windows 应用程序日志 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67bdd7948d1722e49976d5e48b571c684431cd1c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691015"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Write the Job Status to the Windows Application Log
  本主题介绍如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在中配置代理 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，以便通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 、或 SQL Server 管理对象将作业状态写入 Windows 应用程序事件日志 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 作业响应可确保数据库管理员知道作业完成的时间和作业运行频率。 典型的作业响应包括：  
  
-   使用电子邮件、电子寻呼或 **net send** 消息通知操作员。 如果操作员必须执行后续操作，应使用其中的某种作业响应。 例如，当一个备份作业成功地完成之后，必须通知操作员取出备份磁带并将其存放在安全处。  
  
-   将事件消息写入 Windows 应用程序日志。 只能对失败的作业使用这种响应。  
  
-   自动删除作业。 如果确信不需要再次运行该作业，可以使用这种作业响应。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要将作业状态写入 Windows 应用程序日志，请使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>将作业状态写入 Windows 应用程序日志  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，展开 **“作业”**，右键单击要编辑的作业，再单击 **“属性”**。  
  
3.  选择 **“通知”** 页。  
  
4.  请检查 **“写入 Windows 应用程序事件日志”**，然后执行下列操作之一：  
  
    -   单击“当作业成功时”****，以在作业成功完成时记录作业状态。  
  
    -   单击“当作业失败时”****，以在作业未成功完成时记录作业状态。  
  
    -   单击“当作业完成时”****，以便无论完成状态如何，都记录作业状态。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  

### <a name="to-write-job-status-to-the-windows-application-log"></a>将作业状态写入 Windows 应用程序日志
  
 通过使用所选编程语言（如 Visual Basic、Visual C# 或 PowerShell）来调用 `EventLogLevel` 类的 `Job` 属性。  
  
 下列代码示例将作业设置为在作业完成执行时生成操作系统事件日志条目。  
  
```powershell
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
