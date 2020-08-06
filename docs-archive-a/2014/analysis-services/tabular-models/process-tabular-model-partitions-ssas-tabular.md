---
title: " (SSAS 表格) 处理表格模型分区 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 496874707bd4030a98b1794fe7513d1d857390ae
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87683087"
---
# <a name="process-tabular-model-partitions-ssas-tabular"></a>处理表格模型分区（SSAS 表格）
  分区将表分成多个逻辑部分。 然后，每个分区可独立于其他分区进行处理（刷新）。 本主题中的任务说明如何使用 **中的** “处理分区” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]对话框在模型数据库中处理分区。  
  
###  <a name="to-process-a-partition"></a><a name="bkmk_create_new"></a> 处理分区  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，右键单击包含要处理的分区的表，然后单击“分区”****。  
  
2.  在 **“分区”** 对话框的 **“分区”** 中，单击“处理”按钮。  
  
3.  在 "**处理分区 (s) ** " 对话框的 "**模式**" 列表框中，选择以下处理模式之一：  
  
    |“模式”|说明|  
    |----------|-----------------|  
    |**处理默认值**|检测分区对象的处理状态，执行必要的处理，将未处理的分区对象或部分处理的分区对象交付为已完全处理的分区对象。 为空表和分区加载数据；生成或重新生成层次结构、计算列和关系。|  
    |**处理全部**|处理分区对象及其包含的所有对象。 对已处理的对象运行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。 在对对象进行结构更改后，需要这种类型的处理。|  
    |**处理数据**|将数据加载到分区或表中，而无需重新生成层次结构或关系或重新计算计算列和度量值。|  
    |**处理清除**|删除分区中的所有数据。|  
    |**处理添加**|以增量方式用新数据更新分区。|  
  
4.  在 **“处理”** 复选框列中，选择要用所选模式处理的分区，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的表格模型分区](partitions-ssas-tabular.md)   
 [创建和管理表格模型分区（SSAS 表格）](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
