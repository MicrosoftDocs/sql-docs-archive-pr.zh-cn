---
title: XTP (内存中 OLTP) 性能计数器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4363a526ada3694e92d18cac0d7abe8a26f6a92f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688859"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>XTP（内存中 OLTP）性能计数器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了对象和计数器，性能监视器可以使用它们来监视内存中 OLTP 活动。  
  
##  <a name="xtp-in-memory-oltp-performance-objects"></a><a name="SQLServerPOs"></a>XTP (内存中 OLTP) 性能对象  
 下表介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象：  
  
|性能对象|说明|  
|------------------------|-----------------|  
|[XTP 游标](../cursors.md)|XTP 游标性能对象包含与内部 XTP 引擎游标相关的计数器。 游标是 XTP 引擎用于处理 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询的低级构建基块。 因此，您通常不能直接控制游标。|  
|[XTP 垃圾收集](sql-server-xtp-garbage-collection.md)|XTP 垃圾收集性能对象包含与 XTP 引擎的垃圾收集器相关的计数器。|  
|[XTP 虚拟处理器](sql-server-xtp-phantom-processor.md)|XTP 虚拟处理器性能对象包含与 XTP 引擎的虚拟处理子系统相关的计数器。 此组件用于检测在 SERIALIZABLE 隔离级别运行的事务中的虚拟行。|  
|[XTP 存储](sql-server-xtp-storage.md)|XTP 存储性能对象包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XTP 存储相关的计数器。|  
|[XTP 事务日志](sql-server-xtp-transaction-log.md)|XTP 事务日志性能对象包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XTP 事务日志记录相关的计数器。|  
|[XTP 事务](sql-server-xtp-transactions.md)|XTP 事务性能对象包含与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 XTP 引擎事务相关的计数器。|  
  
  
