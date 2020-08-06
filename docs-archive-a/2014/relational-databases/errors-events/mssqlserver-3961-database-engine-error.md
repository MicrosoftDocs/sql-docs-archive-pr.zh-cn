---
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f55be9288b3c2e559633d0f67709829466fc8815
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590214"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3961|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XACT_METADATA_INVALID|  
|消息正文|数据库 '%.*ls' 中的快照隔离事务失败，因为自此事务启动后，该语句所访问的对象已由其他并发事务中的 DDL 语句修改。  禁用它是因为元数据未进行版本控制。 在混合了快照隔离操作的情况下，对元数据进行并发更新可能导致不一致。|  
  
## <a name="explanation"></a>说明  
 如果在快照隔离情况下查询元数据，同时有一个并发 DDL 语句在更新元数据，而该元数据在快照隔离情况下被访问，则可能发生此错误。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持元数据的版本控制。 因此，对于快照隔离情况下在显式事务中能够执行的具体 DDL 操作会存在限制。 根据定义，隐式事务是单个语句，有了该语句就可以强制实施快照隔离的语义，即使在 DDL 语句存在的情况下也是如此。 在快照隔离下，以下 DDL 语句不允许出现在 BEGIN TRANSACTION 语句后：ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME 或任何常用语言运行时(CLR) DDL 语句。 在隐式事务中使用快照隔离时，允许使用这些语句。 根据定义，隐式事务是单个语句，有了该语句就可以强制实施快照隔离的语义，即使在 DDL 语句存在的情况下也是如此。  
  
## <a name="user-action"></a>用户操作  
 在查询元数据之前将快照隔离级别更改为诸如“已提交读”之类的非快照隔离级别。  
  
  
