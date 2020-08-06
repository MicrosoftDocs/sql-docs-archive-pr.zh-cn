---
title: 强制目标服务器轮询主服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: stevestein
ms.author: sstein
ms.openlocfilehash: b37bf19bfe8e8fb55c29c8d94c28a341d06df5da
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577210"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Force a Target Server to Poll the Master Server
  本主题说明如何强制目标服务器轮询主服务器。 目标服务器必须是主服务器上的已注册服务器。  
  
 作业是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理执行的一系列指定操作。 多服务器作业是主服务器在一台或多台目标服务器上运行的作业。 每个目标服务器一次只能运行一个相同作业的实例。 每台目标服务器会定期轮询主服务器，下载分配给目标服务器的任何新作业的一个副本，然后断开连接。 目标服务器在本地运行作业，然后重新连接到主服务器以上载作业结果状态。  
  
> [!NOTE]  
>  如果在目标服务器试图上载作业状态时无法访问主服务器，则作业将处于假脱机状态，直到可以访问主服务器。  
  
-   **开始之前：** [限制和局限](#Restrictions)、[安全性](#Security)  
  
-   **若要强制目标服务器轮询主服务器，使用：**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
 目标服务器必须是主服务器上的已注册服务器。 您必须从主服务器中运行本主题中给出的说明。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关详细信息，请参阅 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) 和 [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> 使用 SQL Server Management Studio  
 **强制目标服务器轮询主服务器**  
  
1.  在 **对象资源管理器**中，展开主服务器。  
  
2.  右键单击“SQL Server 代理”****，指向“多服务器管理”****，再单击“管理目标服务器”****。  
  
3.  单击目标服务器，再单击 **“强制轮询”**。  
  
  
