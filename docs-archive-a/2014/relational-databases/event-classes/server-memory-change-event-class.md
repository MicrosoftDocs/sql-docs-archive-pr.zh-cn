---
title: Server Memory Change 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Server Memory Change event class
ms.assetid: c9836484-39c5-4a89-b080-3567783b6fff
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4dfa610b7632455c5d7d7a84efcb6101ffc7575b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591356"
---
# <a name="server-memory-change-event-class"></a>Server Memory Change 事件类
  当   的内存使用量增加或减少了 1 MB 或最大服务器内存的 5%（以较大者为准）时，会出现 Server Memory Change 事件类[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="server-memory-change-event-class-data-columns"></a>Server Memory Change 事件类的数据列  
  
|数据列名称|数据类型|说明|列 ID|是|  
|----------------------|---------------|-----------------|---------------|---------|  
|**EventClass**|**int**|事件类型 = 81。|27|否|  
|**EventSequence**|**int**|给定事件在请求中的顺序。|51|否|  
|**EventSubClass**|**int**|事件子类的类型。<br /><br /> 1= 内存增加<br /><br /> 2= 内存减少|21|是|  
|**IntegerData**|**int**|新内存大小 (MB)。|25|是|  
|**IsSystem**|**int**|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|是|  
|**RequestID**|**int**|包含该语句的请求的 ID。|49|是|  
|**ServerName**|**nvarchar**|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|**SessionLoginName**|**nvarchar**|发起会话的用户的登录名。 例如，如果你使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 **SessionLoginName** 将显示 Login1，而 **LoginName** 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|是|  
|**SPID**|**int**|发生该事件的会话的 ID。|12|是|  
|**StartTime**|**datetime**|该事件（如果存在）的启动时间。|14|是|  
|**TransactionID**|**bigint**|系统分配的事务 ID。|4|是|  
|**XactSequence**|**bigint**|用于说明当前事务的标记。|50|是|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../extended-events/extended-events.md)   
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [“服务器内存”服务器配置选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
