---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b40fe70db8849d09f9296a06cbeed65a9c71e5a5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588548"
---
# <a name="mssqlserver_9002"></a>MSSQLSERVER_9002
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9002|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LOG_IS_FULL|  
|消息正文|数据库 '%.*ls' 的事务日志已满。 若要查明无法重用日志中的空间的原因，请参阅 sys.databases 中的 log_reuse_wait_desc 列。|  
  
## <a name="explanation"></a>说明  
 数据库日志空间不足。 **sys.databases** 中的 **log_reuse_wait_desc** 列说明无法重用日志中的空间的原因。  
  
## <a name="user-action"></a>用户操作  
 使用 **sys.databases** 确定日志已满的原因，然后更正该情况。 有关详细信息，请参阅 Server SQL 联机丛书中的“解决事务日志已满的问题（错误 9002）”。  
  
## <a name="see-also"></a>另请参阅  
 [解决事务日志已满的问题（SQL Server 错误 9002）](../logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
