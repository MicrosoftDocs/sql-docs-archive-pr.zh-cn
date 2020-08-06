---
title: 自动删除作业 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- dropping jobs
- SQL Server Agent jobs, removing
- automatic job removal
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 92dbb6da-5919-4bde-9354-d454e9ea3da0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 07a10ec4a31d553a548bfecdcba426e3b46a1782
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588246"
---
# <a name="automatically-delete-a-job"></a>Automatically Delete a Job
  本主题介绍如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在中将代理配置 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 为在作业成功、失败或完成时通过使用或 SQL Server 管理对象自动删除作业 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 作业响应可确保数据库管理员知道作业完成的时间和作业运行频率。 典型的作业响应包括：  
  
-   使用电子邮件、电子寻呼或 **net send** 消息通知操作员。  
  
     如果操作员必须执行后续操作，应使用其中的某种作业响应。 例如，当一个备份作业成功地完成之后，必须通知操作员取出备份磁带并将其存放在安全处。  
  
-   将事件消息写入 Windows 应用程序日志。  
  
     只能对失败的作业使用这种响应。  
  
-   自动删除作业。  
  
     如果确信不需要再次运行该作业，可以使用这种作业响应。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要指定作业响应，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-automatically-delete-a-job"></a>自动删除作业  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  展开 **“SQL Server 代理”**，展开 **“作业”**，右键单击要编辑的作业，再单击 **“属性”**。  
  
3.  选择 **“通知”** 页。  
  
4.  选中 **“自动删除作业”**，并选择以下某项：  
  
    -   单击 **“当作业成功时”** 以在作业成功完成时删除作业状态。  
  
    -   单击 **“当作业失败时”** 以在作业失败时删除作业。  
  
    -   单击 **“当作业完成时”** 以删除作业，而不管完成状态如何。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  
 **自动删除作业**  
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用`DeleteLevel` 类的 `Job` 属性。 有关详细信息，请参阅 [SQL Server 管理对象 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
