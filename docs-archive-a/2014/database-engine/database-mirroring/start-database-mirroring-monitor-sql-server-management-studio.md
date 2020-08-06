---
title: 启动数据库镜像监视器 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 67c7b393b28d4d400535281c18c637146a5d8da7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576974"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>启动数据库镜像监视器 (SQL Server Management Studio)
  数据库镜像监视器是通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]监视器的一部分。  
  
> [!NOTE]  
>  并非 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个版本都提供数据库镜像监视。 有关各个版本支持的功能列表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请参阅 SQL Server 2014 的各个[版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>启动数据库镜像监视器  
  
1.  连接到主体服务器实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，再选择要监视的数据库。  
  
3.  右键单击数据库，选择“任务” ****，再单击“启动数据库镜像监视器” ****。  
  
4.  在 **“数据库镜像监视器”** 对话框中，单击 **“注册镜像数据库”** 以注册一个或多个镜像数据库。  
  
    > [!NOTE]  
    >  在一个伙伴上注册数据库时，会自动在另一个伙伴上注册此数据库。 如果监视器已具有另一个伙伴实例的连接凭据，则可以使用这些凭据进行连接。 否则，监视器尝试使用 Windows 身份验证进行连接。 如果要更改用于连接到任一服务器实例的凭据，则单击 **“当单击‘确定’后，显示‘管理服务器连接’对话框”**。  
  
 有关数据库镜像监视器的详细信息，请参阅 [数据库镜像监视器概述](database-mirroring-monitor-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)   
 [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
  
