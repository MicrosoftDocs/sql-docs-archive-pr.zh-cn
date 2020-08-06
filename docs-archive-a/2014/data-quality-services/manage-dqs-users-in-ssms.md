---
title: 在 SSMS 中管理 DQS 用户 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bf8789abb59d168f39562f6486bb5c54bfc0fc50
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590373"
---
# <a name="manage-dqs-users-in-ssms"></a>在 SSMS 中管理 DQS 用户
  本主题介绍如何使用 SQL Server Management Studio 在 SQL Server 实例中创建其他用户，并向这些用户授予针对 DQS_MAIN 数据库的适当 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 角色。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 若要创建 SQL 登录名以及授予适当的 DQS 角色，您的 Windows 用户帐户必须是相应固定服务器角色（例如 securityadmin、serveradmin 或 sysadmin）的成员。  
  
##  <a name="create-a-sql-login-and-grant-dqs-role"></a><a name="GrantRoles"></a>创建 SQL 登录名并授予 DQS 角色  
  
1.  启动 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，展开您的 SQL Server 实例，然后展开 **“安全性”**。  
  
3.  右键单击“安全性”文件夹，指向“新建”，然后单击“登录名”************。  
  
4.  在“登录名 - 新建”对话框中，在“登录名”框中指定 Windows 用户的名称，将身份验证类型指定为“Windows 身份验证”，然后单击“搜索”以验证此用户****************。  
  
    > [!NOTE]  
    >  DQS 只支持 Windows 身份验证；不支持 SQL Server 身份验证。  
  
5.  在验证该用户后，在左侧窗格中单击 **“用户映射”** 。  
  
6.  在右侧窗格中，选中 **DQS_MAIN** 数据库的“映射”**** 列下的复选框，然后根据用户所需的访问级别，在“数据库角色成员身份: DQS_MAIN”**** 窗格中选中 **dqs_administrator**、**dqs_kb_editor** 或 **dqs_kb_operator** 复选框。  
  
7.  在“登录名 - 新建”对话框中，单击“确定”以便应用更改********。  
  
    > [!NOTE]  
    >  如果你向某一用户授予 **dqs_administrator** 角色，应用更改，然后重新选中用户权限，则其他两个 DQS 角色复选框（**dq_kb_editor** 和 **dqs_kb_operator**）也将被选中。  
  
  
