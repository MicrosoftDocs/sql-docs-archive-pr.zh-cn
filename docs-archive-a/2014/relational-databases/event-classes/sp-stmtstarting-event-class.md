---
title: SP:StmtStarting 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SP:StmtStarting event class
ms.assetid: 73550597-a3f3-4454-8678-0bf39db80a7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: a69956a87414c073a49e5a92e81c6b85ce5bb720
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578237"
---
# <a name="spstmtstarting-event-class"></a>SP:StmtStarting 事件类
  SP:StmtStarting 事件类指示已开始执行存储过程中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
## <a name="spstmtstarting-event-class-data-columns"></a>SP:StmtStarting 事件类的数据列  
  
|数据列名称|数据类型|说明|列 ID|可筛选|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。 此列由应用程序传递的值填充，而不是由所显示的程序名填充。|10|是|  
|ClientProcessID|`int`|主机为运行该客户端应用程序的进程分配的 ID。 如果客户端提供了客户端进程 ID，则填充此数据列。|9|是|  
|DatabaseID|`int`|正在运行存储过程的数据库的 ID。 可使用 DB_ID 函数来确定数据库的值。|3|是|  
|DatabaseName|`nvarchar`|正在运行存储过程的数据库的名称。|35|是|  
|EventClass|`int`|事件类型 = 44。|27|否|  
|EventSequence|`int`|给定事件在请求中的顺序。|51|否|  
|GroupID|`int`|在其中激发 SQL 跟踪事件的工作负荷组的 ID。|66|是|  
|HostName|`nvarchar`|正在运行客户端的计算机的名称。 如果客户端提供了主机名，则填充此数据列。 若要确定主机名，请使用 HOST_NAME 函数。|8|是|  
|IntegerData2|`int`|正在执行的语句的终止偏移量（字节）。|55|是|  
|IsSystem|`int`|指示事件是发生在系统进程中还是发生在用户进程中。 1 = 系统，0 = 用户。|60|是|  
|LineNumber|`int`|正在执行的语句的行号。|5|是|  
|LoginName|`nvarchar`|用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。|11|是|  
|LoginSid|`image`|登录用户的安全标识号 (SID)。 您可以在 sys.server_principals 目录视图中找到此信息。 服务器中的每个登录名都具有唯一的 SID。|41|是|  
|NestLevel|`int`|表示 @@NESTLEVEL 所返回的数据的整数。|29|是|  
|NTDomainName|`nvarchar`|用户所属的 Windows 域。|7|是|  
|NTUserName|`nvarchar`|Windows 用户名。|6|是|  
|ObjectID|`int`|系统分配的对象 ID。|22|是|  
|ObjectName|`nvarchar`|引用的对象名。|34|是|  
|ObjectType|`int`|表示事件中涉及的对象类型的值。 此值对应于 sys.objects 目录视图中的类型列。 有关值的信息，请参阅 [ObjectType 跟踪事件列](objecttype-trace-event-column.md)。|28|是|  
|Offset|`int`|存储过程或批查询中的语句的起始偏移量。|61|是|  
|RequestID|`int`|包含该语句的请求的 ID。|49|是|  
|ServerName|`nvarchar`|所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|26|否|  
|SessionLoginName|`nvarchar`|发起会话的用户的登录名。 例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 SessionLoginName 将显示 Login1，而 LoginName 将显示 Login2。 此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。|64|是|  
|SourceDatabaseID|`int`|对象所在数据库的 ID。|62|是|  
|SPID|`int`|发生该事件的会话的 ID。|12|是|  
|StartTime|`datetime`|该事件（如果存在）的启动时间。|14|是|  
|州省/自治区/直辖市|`int`|指示在重新编译后是否执行语句。<br /><br /> 1 = 已重新编译|30|是|  
|TextData|`ntext`|依赖于跟踪中捕获的事件类的文本值。|1|是|  
|TransactionID|`bigint`|系统分配的事务 ID。|4|是|  
|XactSequence|`bigint`|用于说明当前事务的标记。|50|是|  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../extended-events/extended-events.md)   
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
