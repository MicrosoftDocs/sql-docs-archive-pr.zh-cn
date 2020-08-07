---
title: MSSQLSERVER_1203 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3cea816a60ccd1b90d849194766edebd2d64d0b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589137"
---
# <a name="mssqlserver_1203"></a>MSSQLSERVER_1203
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1203|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LK_NOT|  
|消息正文|进程 ID %d 尝试对不归它所有的资源进行解锁: %.*ls。 请重试该事务，因为此错误可能是计时条件导致的。 如果该问题仍然存在，请与数据库管理员联系。|  
  
## <a name="explanation"></a>说明  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行的活动不是普通的后处理清除活动，并且发现它试图解锁的特定页已经解锁时，将产生此错误。  
  
### <a name="possible-causes"></a>可能的原因  
 此错误的基本原因可能与受影响数据库中存在结构问题相关。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以通过管理页的获取和释放维护多用户环境中的并发控制。 此机制的维护是通过使用各种内部锁结构来实现的，这些内部锁结构标识了当前的页和当前的锁类型。 处理受影响页时获取锁，处理完成后则释放锁。  
  
## <a name="user-action"></a>用户操作  
 对对象所属数据库执行 DBCC CHECKDB。 如果 DBCC CHECKDB 未报告错误，则尝试重新建立连接并执行此命令。  
  
> [!IMPORTANT]  
>  如果执行 DBCC CHECKDB 时有一个 REPAIR 子句未更正索引问题，或者如果不确定执行具有 REPAIR 子句的 DBCC CHECKDB 会对数据有何影响，请与主要支持提供商联系。  
  
  
