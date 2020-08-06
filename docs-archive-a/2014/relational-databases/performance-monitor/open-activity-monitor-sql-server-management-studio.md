---
title: 打开活动监视器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ea74122ad18a0a1ede5eef1e09684606ca0ce073
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692857"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>打开活动监视器 (SQL Server Management Studio)
  本主题介绍如何打开活动监视器以便获取有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的信息，并了解这些进程如何影响当前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 本主题还介绍如何设置活动监视器的刷新间隔。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **使用以下工具打开活动监视器：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **使用以下工具设置刷新间隔：**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
 活动监视器将在被监视的实例上运行查询以获取有关活动监视器显示窗格的信息。 当刷新间隔设置为小于 10 秒时，运行这些查询所用的时间可能会对服务器性能产生影响。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 若要查看活动监视器，用户必须拥有 VIEW SERVER STATE 权限。 若要查看活动监视器的“数据文件 I/O”部分，除了 VIEW SERVER STATE 之外，您还必须具有 CREATE DATABASE、ALTER ANY DATABASE 或 VIEW ANY DEFINITION 权限。  
  
 若要终止进程，用户必须是 sysadmin 或 processadmin 固定服务器角色的成员。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>打开 SQL Server Management Studio 中的活动监视器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 标准工具栏上，单击 **“活动监视器”**。  
  
2.  在 **“连接到服务器”** 对话框中，选择服务器名和身份验证模式，然后单击 **“连接”**。  
  
 还可随时通过按 CTRL+ALT A 打开活动监视器。  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>在对象资源管理器中打开活动监视器  
  
-   在对象资源管理器中，右键单击实例名称，然后选择 "**活动监视器**"。  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>在打开 SQL Server Management Studio 时打开活动监视器  
  
1.  在“工具”  菜单上，单击“选项”  。  
  
2.  在 **“选项”** 对话框中，展开 **“环境”**，再选择 **“常规”**。  
  
3.  在 **“启动时”** 框中，选择 **“打开对象资源管理器和活动监视器”**。  
  
4.  若要激活更改，请先关闭再重新打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
###  <a name="to-set-the-activity-monitor-refresh-interval"></a><a name="Refresh"></a>设置活动监视器刷新间隔  
  
-   打开活动监视器。  
  
-   右键单击“概述”，选择“刷新间隔”，然后选择活动监视器获取新实例信息所用的间隔。  
  
  
