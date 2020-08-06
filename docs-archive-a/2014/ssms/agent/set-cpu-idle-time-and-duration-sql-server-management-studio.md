---
title: 设置 CPU 空闲时间和持续时间 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CPU [SQL Server], idle conditions
- time [SQL Server], CPU idle and duration
- duration of CPU idle [SQL Server]
- SQL Server Agent, CPU idle conditions
- idle time [SQL Server]
ms.assetid: 8647b465-d899-4cc7-9640-134a506d0a2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1660f6d70977b8f590a18adf952a6a19f32a26cf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694206"
---
# <a name="set-cpu-idle-time-and-duration-sql-server-management-studio"></a>设置 CPU 空闲时间和持续时间 (SQL Server Management Studio)
  本主题说明如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]定义服务器的 CPU 空闲条件。 CPU 空闲定义会影响 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理对事件的响应方式。 例如，假设将 CPU 空闲条件定义为 CPU 平均使用率低于 10% 并在此级别保持 10 分钟。 那么，如果将作业定义为在服务器 CPU 达到空闲条件时执行，则当 CPU 使用率低于 10% 并在该级别保持 10 分钟后，作业将开始执行。 如果作业对服务器的性能具有显著影响，如何定义 CPU 空闲条件将变得非常重要。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-cpu-idle-time-and-duration"></a>设置 CPU 空闲时间和持续时间  
  
1.  在**对象资源管理器中，** 连接到的实例 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ，然后展开该实例。  
  
2.  右键单击“SQL Server 代理”****，再单击“属性”****，然后选择“高级”**** 页。  
  
3.  在 **“空闲 CPU 条件”** 下，执行下列操作：  
  
    -   选中 **“定义空闲 CPU 条件”**。  
  
    -   在“CPU 平均使用率低于”****（对于所有 CPU 而言）框中指定百分比。 此选项设置 CPU 必须低于什么使用率级别才能变为空闲状态。  
  
    -   在 **“并且保持低于此级别”** 框中指定秒数。 此选项设置 CPU 最小使用率必须保持多长时间 CPU 才能变为空闲状态。  
  
  
