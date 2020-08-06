---
title: 复制的安全角色要求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7eeea09a8dd580870b1d7d5514878172325fe9fe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691644"
---
# <a name="security-role-requirements-for-replication"></a>Security Role Requirements for Replication
  复制限制用户以用户登录名映射到的角色执行的特定操作。 复制向 **sysadmin** 固定服务器角色、 **db_owner** 固定数据库角色和发布访问列表 (PAL) 中的登录名授予了特定权限。  
  
## <a name="security-role-requirements-for-replication-setup"></a>复制设置的安全角色要求  
 下表概述了常见复制设置任务所需的身份验证级别：  
  
|设置任务|成员身份要求|  
|----------------|----------------------------|  
|启用分发服务器、发布服务器或订阅服务器。|发布服务器上的**sysadmin** 服务器角色。|  
|启用数据库进行复制。|发布服务器上的**sysadmin** 服务器角色。|  
|创建发布。|发布服务器的发布数据库上的**db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。|  
|查看发布属性。|发布服务器上的 PAL 成员、发布服务器的发布数据库上的 **db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。|  
|创建订阅。|发布服务器的发布数据库上的**db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。<br /><br /> 订阅服务器的订阅数据库上的**db_owner** 数据库角色或订阅服务器上的 **sysadmin** 服务器角色。|  
|配置代理配置文件。|分发服务器上的**sysadmin** 服务器角色。|  
  
## <a name="security-role-requirements-for-replication-maintenance"></a>复制维护的安全角色要求  
 下表概述了常见复制维护任务所需的身份验证级别：  
  
|维护任务|成员身份要求|  
|----------------------|----------------------------|  
|修改或删除分发服务器、发布服务器或订阅服务器。|相应服务器上的**sysadmin** 服务器角色。|  
|修改或删除发布。|发布服务器的发布数据库上的**db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。|  
|修改或删除发布服务器上的订阅。|发布服务器的发布数据库上的**db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。|  
|修改或删除订阅服务器上的订阅。|订阅服务器的订阅数据库上的**db_owner** 数据库角色或订阅服务器上的 **sysadmin** 服务器角色。|  
|将订阅标记为要重新初始化。|推送订阅：订阅服务器上的发布数据库中的 **db_owner** 数据库角色或发布服务器上的 **sysadmin** 服务器角色。<br /><br /> 请求订阅：订阅服务器上的订阅数据库中的 **db_owner** 数据库角色或订阅服务器上的 **sysadmin** 服务器角色。|  
|使用复制监视器查看复制活动、错误和历史记录。 用户不能修改代理配置文件、计划等，除非用户是 **sysadmin** 服务器角色成员。|分发服务器的分发数据库上的**replmonitor** 数据库角色或分发服务器上的 **sysadmin** 服务器角色。|  
|维护复制代理。|相应数据库上的**db_owner** 数据库角色或相应服务器上的 **sysadmin** 服务器角色。<br /><br /> 如果代理是由 **sysadmin** 角色中的用户创建的，并且未给该代理指定代理帐户，则该代理将在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理帐户上下文运行。 在这种情况下， **db_owner** 角色中的用户不能修改与该代理关联的作业。|  
|启动或停止复制代理。|代理作业的所有者或相应服务器上的 **sysadmin** 服务器角色。|  
  
## <a name="see-also"></a>另请参阅  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server 复制安全性](view-and-modify-replication-security-settings.md)  
  
  
