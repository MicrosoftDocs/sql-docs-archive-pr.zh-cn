---
title: 删除跟踪 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b3551cff36ef6e2c2e9cc6a4d9b7056ae44cb950
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587304"
---
# <a name="delete-a-trace-transact-sql"></a>删除跟踪 (Transact-SQL)
  本主题说明如何使用存储过程删除跟踪。  
  
 有关使用跟踪存储过程的示例，请参阅[创建跟踪 (Transact-SQL)](create-a-trace-transact-sql.md)。  
  
### <a name="to-delete-a-trace"></a>删除跟踪  
  
1.  执行 **sp_trace_setstatus** 时通过指定 **@status = 0** 停止跟踪。  
  
2.  执行 **sp_trace_setstatus** 时通过指定 **@status = 2** 关闭跟踪并从服务器删除其信息。  
  
> [!NOTE]  
>  在关闭跟踪前首先必须先停止它。  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_setstatus (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
