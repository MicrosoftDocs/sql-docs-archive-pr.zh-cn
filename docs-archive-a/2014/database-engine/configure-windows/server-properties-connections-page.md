---
title: 服务器属性（“连接”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 80943bc542209fd34cf83e8db7aa76becd04194a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692515"
---
# <a name="server-properties-connections-page"></a>服务器属性（“连接”页）
  使用此页可以查看或修改连接选项。  
  
## <a name="connections"></a>连接  
 **最大并发连接数(0 = 无限制)**  
 如果设置为非零值，则将限制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许的连接数。  
  
> [!CAUTION]  
>  如果将此值设置为较小的值（如 1 或 2），则可能会阻止管理员进行连接以管理该服务器；但是“专用管理员连接”始终可以连接。  
  
## <a name="default-connection-options"></a>默认连接选项  
 **Default connection options**  
 指定默认连接选项，如下表所述：  
  
|配置选项|说明|  
|--------------------------|-----------------|  
|**disable deferred constraint checking**|控制执行期间或延迟的约束检查。|  
|**隐式事务**|控制在运行一条语句时，是否隐式启动一项事务。|  
|**cursor close on commit**|控制执行提交操作后游标的行为。|  
|**ansi warnings**|控制聚合警告中的截断和 NULL。|  
|**ansi padding**|控制固定长度变量的填充。|  
|**ansi nulls**|在使用相等运算符时控制 `NULL` 的处理。|  
|**arithmetic abort**|在查询执行过程中发生溢出或被零除错误时终止查询。|  
|**arithmetic ignore**|在查询过程中出现溢出或被零除错误时返回 NULL。|  
|**quoted identifier**|对表达式进行求值时区别单引号和双引号。|  
|**no count**|关闭执行每个语句后返回的报告受影响的行数的消息。|  
|**ansi null default on**|将会话的行为更改为使用 ANSI 兼容的空性。 未显式定义为空性的新列允许使用空值。|  
|**ansi null default off**|将会话的行为更改为不使用 ANSI 兼容的空性。 未显式定义为空性的新列定义为不允许使用空值。|  
|**concat null yields null**|将 NULL 值与字符串串联时返回 NULL。|  
|**numeric round abort**|表达式中出现精度降低时生成错误。|  
|**xact abort**|如果 Transact-SQL 语句引发运行时错误，则回滚事务。|  
  
 有关连接选项的详细信息，请搜索联机丛书中的特定选项内容。  
  
## <a name="remote-server-connections"></a>远程服务器连接  
 **允许远程连接到此服务器**  
 从运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的远程服务器控制存储过程的执行。 选中此复选框与将 **sp_configureremote access** 选项设置为 1 具有相同的作用。 清除此复选框可阻止从远程服务器执行存储过程。  
  
 **远程查询超时值(秒，0 = 无超时)**  
 指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 超时之前远程操作可以执行的时间（秒）。默认为 600 秒，或等待 10 分钟。  
  
 **需要将分布式事务用于服务器到服务器的通信**  
 通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 事务保护服务器到服务器过程的操作。 有关详细信息，请参阅 [配置远程过程事务服务器配置选项](configure-the-remote-proc-trans-server-configuration-option.md)。  
  
## <a name="property-page-display-options"></a>属性页显示选项  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果尚未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 查看此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [查询执行 &#40;选项： SQL Server： "高级" 页&#41;](../options-query-execution-sql-server-advanced-page.md)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
