---
title: 增加或禁用阻塞的进程阈值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a7a90aea3fa8fb4d9c423cea1ec6008b01cde883
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578173"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>增加或禁用阻塞的进程阈值
  此规则检查 blocked process threshold 选项是否已设置为 0（禁用），或者是否已设置为大于或等于 5（秒）的值。 将 blocked process threshold 选项设置为从 1 到 4 的值可能会导致死锁监视器不断运行。 值 1 到 4 应仅用于故障排除，决不应在没有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户服务与支持部门的协助下长期使用或在生产环境中使用。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 若要解决此问题，请将 blocked process threshold 选项设置为 5（秒）或更大的值，或者通过将值设置为 0 来禁用阻塞的进程阈值。 若要将阻塞的进程阈值设置为值 `5` 秒，请执行以下语句：  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>有关详细信息  
 [blocked process threshold 服务器配置选项](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
