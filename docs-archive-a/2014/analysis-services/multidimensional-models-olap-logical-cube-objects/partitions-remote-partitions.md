---
title: 远程分区 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 32fdf05d061d4e1c1da6ec0ef9179ecd12bda172
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690193"
---
# <a name="remote-partitions"></a>远程分区
  远程分区的数据存储在 Microsoft 的不同实例上，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含分区和其父多维数据集的定义 (元数据) 的实例。 远程分区在对其以及其父多维数据集进行定义的同一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中进行管理。  
  
> [!NOTE]  
>  若要存储远程分区，计算机必须安装的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，并且该实例与定义该分区的实例运行相同的 Service Pack 级别。 在更早版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上的远程分区不支持。  
  
 如果度量值组中包括多个远程分区，则多维数据集的内存和 CPU 使用率会分散给度量值组内的所有分区。 例如，当处理远程分区（单独处理或作为其父多维数据集的一部分加以处理）时，该分区的内存和 CPU 使用率的大部分都发生在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 远程实例中。  
  
> [!NOTE]  
>  包含远程分区的多维数据集可以包含启用写入操作的维度，但这可能会影响该多维数据集的性能。 有关启用了写功能的维度的详细信息，请参阅[启用写功能的维度](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
## <a name="storage-modes-for-remote-partitions"></a>远程分区的存储模式  
 远程分区可以使用本地分区所使用的任何存储类型：多维 OLAP (MOLAP)、混合 OLAP (HOLAP) 或关系 OLAP (ROLAP)。 远程分区还可以使用主动缓存。 根据远程分区的存储模式，下列数据将存储到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的远程实例中。  
  
|||  
|-|-|  
|存储类型|数据|  
|MOLAP|分区的聚合和分区源数据的副本|  
|HOLAP|分区聚合|  
|ROLAP|无分区数据|  
  
 如果度量值组包含的多个 MOLAP 或 HOLAP 分区存储在多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中，则多维数据集会将数据分散到这些 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的度量值组数据中。  
  
## <a name="merging-remote-partitions"></a>合并远程分区  
 远程分区只能与存储在同一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 远程实例上的其他远程分区进行合并。 有关合并分区的详细信息，请参阅[Analysis Services &#40;SSAS-多维&#41;中的合并分区](../multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)。  
  
## <a name="archiving-and-restoring-remote-partitions"></a>存档和还原远程分区  
 存档或还原存储远程分区的数据库时，远程分区中的数据也随之一起存档或还原。 如果还原了数据库而没有还原远程分区，则必须先处理此远程分区，然后才能使用该分区中的数据。 有关存档和还原数据库的详细信息，请参阅[Analysis Services 数据库的备份和还原](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理远程分区 &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [处理 Analysis Services 对象](../multidimensional-models/processing-analysis-services-objects.md)  
  
  
