---
title: 监视内存使用量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1986d9576f9b067cad18f27d4febbf097ed52703
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692859"
---
# <a name="monitor-memory-usage"></a>监视内存使用量
  定期监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例以确认内存使用量在正常范围内。  
  
 若要监视内存不足的情况，请使用下列对象计数器：  
  
-   Memory:Available Bytes  
  
-   Memory:Pages/sec  
  
 **Available Bytes** 计数器指示当前有多少内存（以字节为单位）可供进程使用。 **Pages/sec** 计数器指示由于页错误而从磁盘取回的页数，或由于页错误而写入磁盘以释放工作集空间的页数。  
  
 **Available Bytes** 计数器的值低表示计算机总内存不足或应用程序没有释放内存。 **Pages/sec** 计数器的比率高表示分页过多。 监视 **Memory:** Page Faults/sec 计数器以确保磁盘活动不是由分页造成。  
  
 分页率偏低（以及由此产生的页错误）是正常的，即使计算机有大量的可用内存。 Microsoft Windows 虚拟内存管理器 (VMM) 在剪裁 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他进程的工作集大小时会收走这些进程的页。 此 VMM 活动会导致页错误。 若要确定分页过多是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还是由另一个进程导致，请监视 **Process:** Page Faults/sec 计数器，该计数器属于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处理实例。  
  
 有关解决分页过多的详细信息，请参阅 Windows 操作系统文档。  
  
## <a name="isolating-memory-used-by-sql-server"></a>隔离 SQL Server 所用的内存  
 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将根据可用系统资源动态改变其内存要求。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要更多内存，它会查询操作系统以确定是否有可用的空闲物理内存，然后使用可用内存。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 当前不需要分配给它的内存，它会将内存释放给操作系统。 但是，你可以覆盖此选项通过使用 **minservermemory**和 **maxservermemory** 服务器配置选项来动态使用内存。 有关详细信息，请参阅 [服务器内存选项](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
 若要监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的内存量，请检查下列性能计数器：  
  
-   Process:Working Set  
  
-   SQL Server：**Buffer Manager:Buffer Cache Hit Ratio**  
  
-   SQL Server：**Buffer Manager:Database pages**  
  
-   SQL Server：**Memory Manager:Total Server Memory (KB)**  
  
 **WorkingSet** 计数器显示进程所用的内存量。 如果此内存量一直小于 **min server memory** 和 **max server memory** 服务器选项设置的内存量，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 被配置为使用过多内存。  
  
 **Buffer Cache Hit Ratio** 计数器仅适用于应用程序。 但是，90% 或更高的命中率是令人满意的。 添加更多内存，直到该值始终大于 90%。 大于 90% 的值表示数据缓存满足所有数据请求中 90% 以上的请求。  
  
 如果 **TotalServerMemory (KB)** 计数器值相对于计算机的物理内存量而言一直很高，则可能表示需要更多内存。  
  
## <a name="determining-current-memory-allocation"></a>确定当前内存分配  
 以下查询返回有关当前分配内存的信息。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
