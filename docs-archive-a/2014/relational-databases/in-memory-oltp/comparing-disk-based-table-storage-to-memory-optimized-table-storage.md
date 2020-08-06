---
title: 比较基于磁盘的表存储与内存优化的表存储 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 47cf84427b2f4f26a29f732575530b384d9c4fc9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693343"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>比较基于磁盘的表存储与内存优化的表存储
  
  
|类别|基于磁盘的表|持久内存优化表|  
|----------------|-----------------------|-------------------------------------|  
|DDL|元数据信息存储在数据库主文件组中的系统表中，可通过目录视图进行访问。|元数据信息存储在数据库主文件组中的系统表中，可通过目录视图进行访问。|  
|结构|行存储在 8K 页中。 页仅存储相同表中的行。|行作为单独的行进行存储。 没有页结构。 数据文件中的两个连续行可以属于不同内存优化表。|  
|索引|索引采用与数据行类似的页结构进行存储。|仅持久保持索引定义（而不是索引行）。 索引保持在内存中，并将在内存优化表在重新启动数据库期间加载到内存中时重新生成。 由于不会持久保持索引行，因此不会针对索引更改进行日志记录。|  
|DML 操作|第一步是查找页，然后将其加载到缓冲池中。<br /><br /> 插入<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会按照聚集索引时的行排序在页上插入行。<br /><br /> 删除<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在页上找到要删除的行，然后将其标记为已删除。<br /><br /> 更新<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在页上查找行。 对于非键列，将会就地进行更新。 键列更新是通过删除和插入操作完成的。<br /><br /> DML 操作完成后，受影响的页会作为缓冲池策略、检查点或事务提交的一部分刷新到磁盘中，以实现具有最少日志记录的操作。 对页进行的读/写操作均导致不必要的 I/O。|对于内存优化表，由于数据驻留在内存中，因此 DML 操作直接在内存中进行。 有一个后台线程读取内存优化表的日志记录，然后这些记录在数据和差异文件中持久化。 一个更新会生成新的行版本。 但是，会将更新记录为先删除再插入。|  
|数据碎片|数据操作碎片数据会导致部分填充的页以及逻辑上连续但磁盘上不连续的页。 这会降低数据访问的性能，需要对数据进行碎片整理。|内存优化数据不存储在页中，因此没有数据碎片。 但是，随着行的更新和删除，需要压缩数据和差异文件。 此任务是由后台 MERGE 线程基于合并策略完成的。|  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化对象的存储](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
