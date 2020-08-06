---
title: 升级后日志传送不会运行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b2af60743cb2cbf9bf455397fe052c4e81f5a06d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591101"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>日志传送在升级后将无法运行
  升级顾问已检测您正在使用日志传送。 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的日志传送与 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的日志传送不兼容，因此不能直接升级。 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 后，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或存储过程重新配置日志传送。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理日志传送作业类别导致升级失败](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [升级会将 SQL Server 代理用户代理帐户更改为临时 UpgradedProxyAccount](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
