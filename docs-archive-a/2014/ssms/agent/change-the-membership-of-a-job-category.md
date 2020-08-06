---
title: 更改作业类别的成员身份 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
ms.openlocfilehash: d9ed0db394f63594937ad923734b07fed8050955
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591083"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
  本主题介绍如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 SQL Server 管理对象更改作业类别的成员身份。  
  
 作业类别有助于您组织作业，从而更容易筛选和分组。 可以创建自己的作业类别。 还可以更改作业类别中的 Microsoft SQL Server 代理作业成员身份。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要更改作业类别的成员身份，请使用**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理对象](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅[实现 SQL Server 代理安全性](implement-sql-server-agent-security.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>更改作业类别的成员身份  
  
1.  在 **“对象资源管理器”** 中，单击加号以展开您想要在其中编辑作业类别的服务器。  
  
2.  单击加号以展开 **“SQL Server 代理”**。  
  
3.  右键单击 **“作业”** 文件夹，然后选择 **“管理作业类别”**。  
  
4.  在“管理作业类别” ****_server_name_ 对话框中，选择要编辑的作业类别，然后单击“查看作业” ****。  
  
5.  选中 **“显示所有作业”** 复选框。  
  
6.  若要向类别中添加作业，请在主网格中选中与作业对应的 **“选择”** 列中的复选框。 若要从类别中删除作业，请清除该框。 完成后，单击 **“确定”** 。  
  
7.  关闭 "**管理作业类别**_server_name_ " 对话框。  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>更改作业类别的成员身份  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。  
  
    ```sql
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 有关详细信息，请参阅[&#40;transact-sql&#41;sp_update_job ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)。  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理对象  
 **更改作业类别的成员身份**  
  
 通过使用所选的编程语言（如 Visual Basic、Visual C# 或 PowerShell）来使用 `JobCategory` 类。  
