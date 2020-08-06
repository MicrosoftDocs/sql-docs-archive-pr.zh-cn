---
title: 使用内存优化表的要求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ecb9d388fd0e1362bb8844e874cd89162912e93e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692936"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>使用内存优化表的要求
  除了[安装 SQL Server 2014 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)以外，还需要满足以下要求才能使用内存中 OLTP：  
  
-   64 位 Enterprise、Developer 或 Evaluation 版 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要有足够的内存来保留内存优化表和索引中的数据。 若要容纳行版本，您应当提供两倍于内存优化表和索引预期大小的内存量。 但是，所需的实际内存量将依赖于您的工作负荷。 您应当监视内存用量并根据需要进行调整。 内存优化表中数据的大小不能超过允许的池百分比。 若要发现内存优化表的大小，请参阅[&#40;transact-sql&#41;dm_db_xtp_table_memory_stats ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)。  
  
     如果您在数据库具有基于磁盘的表，则需要为这些表上的缓冲池和查询处理提供足够的内存。  
  
     知道您的内存中 OLTP 应用程序将要求的内存量十分重要。 有关详细信息，请参阅 [估算内存优化表的内存需求](memory-optimized-tables.md) 。  
  
-   释放是您的持久内存优化表大小的两倍的磁盘空间。  
  
-   处理器必须支持指令 **cmpxchg16b** 才能使用内存中 OLTP。 所有新式 64 位处理器都支持 **cmpxchg16b**。  
  
     如果你使用的是 VM 主机应用程序，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 显示因处理器较旧而生成的错误消息，请检查应用程序是否将配置选项设置为允许使用 **cmpxchg16b**。 如果没有设置，你可以使用支持 **cmpxchg16b** 的 Hyper-V，而无需修改配置选项。  
  
-   要安装内存中 OLTP，请在安装 **时选择** “数据库引擎服务” [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
     若要 ([确定表或存储过程是否应移植到内存中 oltp](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 并 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (通过对象资源管理器) 来管理内存中 oltp [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，请选择安装报表生成（"**管理工具-基本**" 或 "**管理工具-高级**" [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。  
  
## <a name="important-notes-on-using-hek_2"></a>有关使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]的重要说明  
  
-   数据库中所有持久表在内存中的总大小不应超过 250 GB。 有关详细信息，请参阅[内存优化表的持续](durability-for-memory-optimized-tables.md)性。  
  
-   此版本的 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 的目标是在具有 2 或 4 个插槽和少于 60 个内核的系统上实现最佳执行。  
  
-   不得手动删除检查点文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动对不需要的检查点文件执行垃圾回收。 有关详细信息，请参阅针对[内存优化表的持久性](durability-for-memory-optimized-tables.md)合并数据和差异文件的讨论。  
  
-   在内存中 OLTP 的第一个版本中（ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中），只有删除数据库才能删除内存优化的文件组。  
  
-   如果在有并发插入或更新工作负荷会影响要删除行范围时尝试删除大量行，删除可能失败。 解决方法是先停止插入或更新工作负荷，然后再删除。 或者，也可以将事务配置为较小的事务，这样会减小被并发工作负荷中断的可能性。 像对所有内存优化表的写入操作一样，使用重试逻辑（[Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)）。  
  
-   如果创建一个或多个包含内存优化表的数据库，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用即时文件初始化（授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务启动帐户 SE_MANAGE_VOLUME_NAME 用户权限）。 如果没有即时文件初始化，内存优化存储文件（数据和差异文件）将在创建时初始化，这会对工作负荷性能产生负面影响。 有关即时文件初始化的详细信息，请参阅 [数据库文件初始化](../databases/database-instant-file-initialization.md)。 有关如何启用即时文件初始化的信息，请参阅 [启用即时文件初始化的方法和原因](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)。  
  
## <a name="did-this-article-help-you-were-listening"></a>本文是否对你有帮助？ 正在侦听  
 你正在查找哪些信息，是否已经找到？ 我们正在倾听你的反馈来改进内容。 请将你的评论提交到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page) 。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](in-memory-oltp-in-memory-optimization.md)  
  
  
