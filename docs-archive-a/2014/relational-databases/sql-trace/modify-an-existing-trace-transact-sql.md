---
title: 修改现有跟踪 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], modifying
- modifying traces
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 55b8172ef8e6188059c484ab41f1a719e0e9f8c7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578035"
---
# <a name="modify-an-existing-trace-transact-sql"></a>修改现有跟踪 (Transact-SQL)
  本主题介绍了如何使用存储过程修改现有跟踪。  
  
### <a name="to-modify-an-existing-trace"></a>修改现有跟踪  
  
1.  如果跟踪已在运行，请在执行 **sp_trace_setstatus** 时通过指定 **@status = 0** 停止跟踪。  
  
2.  若要修改跟踪事件，请执行 **sp_trace_setevent** ，并通过参数指定更改。 下面按顺序列出了参数：  
  
    -   **@traceid** (跟踪 ID)   
  
    -   **@eventid** (事件 ID)   
  
    -   **@columnid** (列 ID)   
  
    -   **@on**) 上的 (  
  
     修改 **@on** 参数时，请记住它与参数的交互 **@columnid** ：  
  
    |ON|列 ID|结果|  
    |--------|---------------|------------|  
    |ON (**1**)|Null|事件打开， 所有列被清除。|  
    ||NOT NULL|指定事件的列打开。|  
    |OFF (**0**)|Null|事件关闭， 所有列被清除。|  
    ||NOT NULL|指定事件的列关闭。|  
  
> [!IMPORTANT]
>  与常规的存储过程不同，所有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 存储过程 (<strong>sp_trace_xx</strong>) 参数的类型都受到严格限制，不支持自动的数据类型转换。 如果这些参数不是使用正确的输入参数数据类型（正如参数说明中指定的一样）调用的，则存储过程会返回错误。  

## <a name="see-also"></a>另请参阅  
 [sp_trace_setevent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
