---
title: Analysis Services 多维数据) 的 "合并分区" 对话框 (|Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1978c187bfb5097d286f78650b5bda6645c7a054
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589939"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>“合并分区”对话框（Analysis Services - 多维数据）
  可以使用 **SQL Server Management Studio** 中的 **“合并分区”** 对话框合并多维数据中的度量值组的分区。 通过在**对象资源管理器**中右键单击分区文件夹或某个分区并从上下文菜单中选择“合并分区”****，可以显示“合并分区”**** 对话框。  
  
## <a name="options"></a>选项  
 **Server**  
 选择包含目标分区的 Analysis Services 实例的名称。  
  
 **名称**  
 选择要用作目标分区的现有分区的名称。  
  
 **文件夹**  
 如果在“名称”中选择的分区不使用 Analysis Services 实例的默认文件夹，则显示包含目标分区的文件夹的名称。  
  
 **源分区**  
 显示包含可以合并到目标分区中的源分区的网格。  
  
> [!NOTE]  
>  只能合并同一度量值组中共享相同聚合设计的分区。  
  
 该网格包含以下列：  
  
|列|说明|  
|------------|-----------------|  
|**合并**|选择此选项可以将源分区合并到目标分区中。|  
|**分区名称**|显示源分区的名称。|  
|**上次处理时间**|显示上次处理源分区的日期和时间。|  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 多维数据 &#40;分区&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [在 Analysis Services 中合并分区（SSAS - 多维）](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
