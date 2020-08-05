---
title: SQL Server - Workload Group Stats 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Workload Group Stats object
- 'SQLServer: Workload Group Stats'
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fb363803c562b305687e78e1315f1c4255041b1f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580215"
---
# <a name="sql-server-workload-group-stats-object"></a>SQLServer，Workload Group Stats 对象
  SQLServer:Workload Group Stats 对象包含报告资源调控器工作负荷组统计相关信息的性能计数器。  
  
 每个活动工作负荷组都创建一个 SQLServer:Workload Group Stats 性能对象实例，实例的名称与资源调控器工作负荷组的名称相同。 下表介绍了此实例支持的计数器。  
  
|计数器名称|说明|  
|------------------|-----------------|  
|Queued requests|当前正在等待拾取的排队请求数。 如果达到 GROUP_MAX_REQUESTS 限制后操作中止，则此计数可为非零值。|  
|Active requests|此工作负荷组中当前运行的请求数。 此值应该等于按组 ID 筛选的 sys.dm_exec_requests 的行数。|  
|Requests completed/sec|此工作负荷组中已完成的请求数。 此数值可累计。|  
|CPU usage %|此工作负荷组中所有请求的 CPU 带宽使用量，该值是相对于计算机度量的，并且针对系统中的所有 CPU 进行规范化。 此值将随着可用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的 CPU 量的变化而变化。 它不会针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程接收的信息进行规范化。|  
|Max request CPU time (ms)|此工作负荷组中当前运行的请求所用的最长 CPU 时间，以毫秒为单位。|  
|Blocked requests|工作负荷组中当前被禁止的请求数。 此值可用于确定工作负荷特征。|  
|Reduced memory grants/sec|每秒所获内存量小于理想内存授予量的查询数。|  
|Max request memory grant (KB)|查询的最大内存授予值，以千字节 (KB) 为单位。|  
|Query optimizations/sec|每秒此工作负荷组中发生的查询优化次数。 此值可用于确定工作负荷特征。|  
|Suboptimal plans/sec|每秒此工作负荷组中生成的非最优计划数。|  
|Active parallel threads|当前使用的并行线程数。|  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)   
 [SQL Server，Resource Pool Stats 对象](sql-server-resource-pool-stats-object.md)   
 [资源调控器](../resource-governor/resource-governor.md)  
  
  
