---
title: 合并复制的项目选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d4f9e6391962d5755983322073f738ba84f02633
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576704"
---
# <a name="article-options-for-merge-replication"></a>合并复制的项目选项
  有许多用于合并表项目的选项，可以使用这些选项自定义复制行为以满足应用程序的需要。 使用合并复制可执行以下操作：  
  
-   使用行筛选器、联接筛选器和列筛选器。 通过筛选表项目，可以为要发布的数据创建分区。 有关详细信息，请参阅[筛选已发布数据](../publish/filter-published-data.md)。  
  
-   指定是否将订阅服务器上的更改上载到发布服务器。 对于其中部分或全部数据在订阅服务器上应为只读的应用程序，仅用于下载的项目提供性能收益。 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   指定复制触发器和系统表不能跟踪一个或多个项目的删除操作。 此选项在许多应用方案中都非常有用。 其中包括那些使用不需要复制的批处理删除操作的应用方案。 有关详细信息，请参阅[使用条件性删除跟踪优化合并复制性能](optimize-merge-replication-performance-with-conditional-delete-tracking.md)。  
  
-   指定项目的处理顺序以确保项目按照应用程序要求的顺序处理。 有关详细信息，请参阅[指定合并复制属性](../publish/specify-merge-replication-properties.md)。  
  
-   指定应将一组相关记录作为一个单元进行处理（默认情况下，合并复制逐行处理对表的更改）。 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](group-changes-to-related-rows-with-logical-records.md)。  
  
-   在一个拓扑中的多个节点上更改相同数据的情况下使用冲突检测和解决方法。 有关详细信息，请参阅 [检测并解决合并复制冲突](advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
-   指定架构选项（例如，是否将约束和触发器复制到订阅服务器）。 有关详细信息，请参阅 [指定架构选项](../publish/specify-schema-options.md)。  
  
-   使用业务逻辑处理程序来对同步期间出现的许多情况进行响应。 这些情况包括发生数据更改、冲突和错误。 有关详细信息，请参阅[合并同步期间执行业务逻辑](execute-business-logic-during-merge-synchronization.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../publish/publish-data-and-database-objects.md)  
  
  
