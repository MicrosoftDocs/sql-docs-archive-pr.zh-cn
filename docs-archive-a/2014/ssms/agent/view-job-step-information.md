---
title: 查看作业步骤信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5d9fc6a006884bc564b5db2bfa8b168c8ae59149
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576527"
---
# <a name="view-job-step-information"></a>View Job Step Information
  本主题说明如何在“作业步骤属性”对话框中查看作业步骤的详细信息。 它还包括有关查看作业步骤输出的信息。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要查看作业步骤信息，可使用：**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
 如果已将作业步骤配置为将其输出写入到表或文件，并且作业已经至少运行过一次，则可以在 **“作业步骤属性”** 对话框的 **“高级”** 页上查看其输出。 作业或作业步骤删除时，输出日志也将自动删除。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您只能查看自己拥有的那些作业，除非您是 **sysadmin** 固定服务器角色的成员。 此角色的成员可以查看所有作业和作业步骤的详细信息。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-job-step-information"></a>查看作业步骤信息  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  依次展开“SQL Server 代理”**** 和“作业”****，右键单击包含要查看的作业步骤的作业，再单击“属性”****。  
  
3.  在 **“作业属性”** 对话框中，单击 **“步骤”** 页。  
  
4.  单击要查看的作业步骤，再单击 **“编辑”**。  
  
5.  在 **“作业步骤属性”** 对话框的 **“常规”** 页上，可以查看作业步骤的类型和用途。  
  
6.  单击 **“高级”** 页以查看作业步骤成功或失败时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理所执行的操作、该作业步骤应尝试的次数、该作业步骤输出的位置以及运行该作业步骤的用户。  
  
#### <a name="to-view-job-step-output"></a>查看作业步骤输出  
  
1.  在 **“作业步骤属性”** 对话框中，单击 **“高级”** 页。  
  
2.  根据所连接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本，可以查看作业步骤输出文件或表，如下所示：  
  
    -   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或更高版本时，只有选中 **“记录到表”** ，才能单击 **“查看”** 。 在这种情况下，作业步骤输出将写入 **msdb** 数据库的 **sysjobstepslogs** 表中。  
  
    -   在作业步骤输出写入到文件时，禁用 **“查看”** 按钮。 若要查看作业步骤输出文件，请使用记事本。  
  
  
