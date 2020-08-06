---
title: 断开一些可用性副本的连接 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp7allconnected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: aea808be-6f0f-40c2-9aa2-a2a435ec6443
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bb6535b513770b9b4718a0e8372c0a5bc3cba84
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586985"
---
# <a name="some-availability-replicas-are-disconnected"></a>断开一些可用性副本的连接
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本连接状态|  
|**问题**|断开一些可用性副本的连接。|  
|**类别**|**警告**|  
|**方面**|可用性组 (availability group)|  
  
## <a name="description"></a>说明  
 此策略将汇总所有可用性副本的连接状态，并且检查是否存在处于 DISCONENCTED 状态的任何可用性副本。 当任何可用性副本处于 DISCONNECTED 状态时，此策略处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>   对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [断开一些可用性副本的连接](https://go.microsoft.com/fwlink/p/?LinkId=220855) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 在此可用性组中，至少一个辅助副本未连接到主副本。 连接状态为 DISCONNECTED。  
  
## <a name="possible-solution"></a>可能的解决方法  
 使用可用性副本策略状态查找处于 DISCONNECTED 状态的可用性副本，然后解决该可用性副本上的问题。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
