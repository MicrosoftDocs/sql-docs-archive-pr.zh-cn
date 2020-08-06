---
title: 监视数据和差异文件对的合并以及排除其故障Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5dc57d08f3db1792a9359b3aa79aaceecd03a025
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590367"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>监视数据与差异文件对的合并以及排除其故障
  内存中 OLTP 使用合并策略自动合并相邻数据和差异文件对。 无法禁用合并活动。  
  
 可按如下方式监视数据和差异文件对：  
  
-   将内存中存储的大小与存储的总大小进行比较。 如果存储大得不成比例，则可能未触发合并。 有关信息  
  
-   使用[sys. dm_db_xtp_checkpoint_files &#40;transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql)查看数据和差异文件中的已用空间，以查看是否在其应该触发 merge。  
  
## <a name="performing-a-manual-merge"></a>执行手动合并  
 您可以使用[sys. sp_xtp_merge_checkpoint_files &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)执行手动合并。  
  
 使用以下查询检索有关数据和差异文件的信息，  
  
```sql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 假设您找到了三个未合并的数据文件。 可使用第一个数据文件的 `lower_bound_tsn` 值和最后一个数据文件的 `upper_bound_tsn` 发出以下命令：  
  
```sql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 假定三个数据和差异文件对的每一对都有 15836 行，并且其中删除了 5279 行。 合并后，新数据文件有 31872 行，未删除行。 新数据文件的大小可远远大于初始分配的 128MB 大小。 这是因为手动合并优先于合并策略，强制合并所请求的文件。  
  
 [具有内存优化表的数据库中检查点文件的博客状态转换](https://cloudblogs.microsoft.com/sqlserver/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables/)说明数据和差异文件对从开始到垃圾回收的状态转换。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化对象的存储](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
