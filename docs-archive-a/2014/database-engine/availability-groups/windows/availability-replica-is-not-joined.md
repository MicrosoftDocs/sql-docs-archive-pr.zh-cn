---
title: 可用性副本未联接 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7c4f76e98d373e50124f5ca2b135a9fad8f34226
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690150"
---
# <a name="availability-replica-is-not-joined"></a>可用性副本未联接
    
## <a name="introduction"></a>简介  
  
|||  
|-|-|  
|**策略名称**|可用性副本联接状态|  
|**问题**|可用性副本未联接。|  
|**类别**|**警告**|  
|**方面**|可用性副本|  
  
## <a name="description"></a>说明  
 此策略检查可用性副本的联接状态。 当可用性副本添加到可用性组但未正确联接时，该策略将处于不正常状态。 否则，该策略处于正常状态。  
  
> [!NOTE]  
>  对于此版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，与可能原因和解决方法有关的信息位于 TechNet Wiki 上的 [可用性副本未联接](https://go.microsoft.com/fwlink/p/?LinkId=220859) 中。  
  
## <a name="possible-causes"></a>可能的原因  
 辅助副本未联接到可用性组。 要将某一可用性副本成功联接到可用性组，联接状态必须为“已联接独立实例”(1) 或“已联接故障转移群集”(2)。  
  
## <a name="possible-solution"></a>可能的解决方法  
 使用 Transact-SQL、PowerShell 或 SQL Server Management Studio 将辅助副本联接到可用性组。 有关将辅助副本联接到可用性组的详细信息，请参阅 [将辅助副本联接到可用性组 (SQL Server)](https://msdn.microsoft.com/library/ff878473\(en-us,SQL.110\).aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
