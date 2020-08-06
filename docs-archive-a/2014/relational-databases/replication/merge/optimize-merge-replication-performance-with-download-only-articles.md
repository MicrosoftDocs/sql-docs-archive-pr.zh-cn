---
title: 使用仅下载项目优化合并复制性能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8414174971792f8a2c256cd564dd1ea224527463
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576677"
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>使用仅下载项目优化合并复制的性能
  合并复制提供了两种不同的项目类型以满足不同的应用程序需要。 根据应用程序的需要，发布可以包含下列项目类型中的一个或多个：  
  
-   标准项目  
  
-   仅下载项目  
  
 仅下载项目比标准项目具有性能优势，应尽可能使用这种项目。  
  
> [!NOTE]  
>  若要使用仅下载项目，发布的兼容级别必须至少为 90RTM。  
  
## <a name="standard-articles"></a>标准项目  
 标准项目是默认项目，可以提供所有合并复制功能，包括丰富的冲突检测和解决。 标准项目适用于由多个订阅服务器更新的表，表以外的对象（如存储过程和视图）始终按标准项目发布。  
  
## <a name="download-only-articles"></a>仅下载项目  
 仅下载项目是为数据不在订阅服务器上更新的应用程序设计的，如包含在产品目录中的一组项目。 产品目录通常在发布服务器上更新，而不是在订阅服务器上更新。 因为仅供下载的项目不能在订阅服务器上更新，所以跟踪元数据不会发送到订阅服务器。 这可以减少订阅服务器上的存储量并提高性能，特别是当网络连接较慢时。  
  
 仅下载项目与客户端订阅一起使用：如果项目设计为仅下载项目，则不能在使用客户端订阅的订阅服务器上插入、更新或删除该项目的行。 使用服务器订阅类型的发布服务器和订阅服务器（通常是指将数据重新发布到其他订阅服务器的订阅服务器）可以插入、更新和删除数据。 有关客户端订阅的详细信息，请参阅[订阅发布](../subscribe-to-publications.md)。  
  
 若要将某个项目指定为仅下载项目，请参阅 [指定合并表项目仅用于下载](../publish/specify-merge-replication-properties.md#download-only)。  
  
## <a name="using-different-article-types-in-your-applications"></a>在应用程序中使用不同的项目类型  
 通过了解应用程序的要求，可以在最大灵活性和最佳性能之间找到平衡点。 例如，在发布服务器和订阅服务器上都存在大量冲突和更改的应用程序将使用由标准项目组成的发布。 有些应用程序（如销售人员自动化应用程序）可能包含存在潜在冲突的项目以及作为查找表的其他项目，这些项目可以指定为仅下载项目。 数据输入应用程序（如销售点系统和现场人员自动化应用程序）通常以消除冲突的方式对数据进行严格的分区，使一个订阅服务器上的数据永远不会到另一个订阅服务器上。 在这些情况下，不重叠的分区、仅下载项目和预计算分区的组合可以提供最好的性能和最大的伸缩性。 有关不重叠分区和预计算分区的详细信息，请参阅 [参数化行筛选器](parameterized-filters-parameterized-row-filters.md)。  
  
## <a name="see-also"></a>另请参阅  
 [用于合并复制的项目选项](article-options-for-merge-replication.md)   
 [用条件性删除跟踪优化合并复制的性能](optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
