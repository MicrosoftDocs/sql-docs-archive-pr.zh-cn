---
title: 为挖掘模型启用钻取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0a6adfc389776f91132e527130f50f61c9783d9f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577911"
---
# <a name="enable-drillthrough-for-a-mining-model"></a>对挖掘模型启用钻取
  如果为挖掘模型启用了钻取，则可以在浏览模型时检索用于创建模型的事例的详细信息。 若要查看这些信息，则您必须拥有必要的权限，且挖掘结构已经过处理。  
  
 **权限** 如果用户要钻取模型数据或结构数据，则该用户必须是具有挖掘模型或挖掘结构的 [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) 权限的角色成员。 挖掘结构和挖掘模型的钻取权限是分开设置的。  
  
-   即使不具有结构的钻取权限，模型的钻取权限也允许您从模型进行钻取。  
  
-   如果拥有结构的钻取权限，则可通过使用 [StructureColumn (DMX)](/sql/dmx/structurecolumn-dmx) 函数，将结构列包含到模型钻取查询中。 您还可以使用 "选择 ..." 来查询结构中的定型和测试用例。FROM \<structure> 。Case 语法。  
  
 **缓存定型事例** 钻取就是检索挖掘结构中的定型事例的相关信息。 这些信息是在处理结构时缓存的。 因此，如果通过将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 `ClearAfterProcessing`，选择清除了缓存的所有数据，则钻取功能将无法正常工作。  
  
> [!NOTE]  
>  如果没有缓存定型事例，则必须将 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 属性更改为 **KeepTrainingCases** ，并重新处理模型，然后才能查看事例数据。  
  
 有关详细信息，请参阅 [钻取查询（数据挖掘）](drillthrough-queries-data-mining.md)。  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>对挖掘模型启用钻取  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中数据挖掘设计器的“挖掘模型”**** 选项卡上，右键单击要针对其启用钻取的挖掘模型名称，再选择“属性”****。  
  
2.  在 "**属性**" 窗口中，单击 " **AllowDrillthrough**"，然后选择 " **True**"。  
  
3.  在“挖掘模型”选项卡中，右键单击所需的模型，再选择“处理模型”********。  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>启用挖掘结构的缓存功能  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的数据挖掘设计器的“挖掘结构”**** 选项卡上，右键单击挖掘结构的名称。  
  
2.  打开 **“属性”** 窗口。  
  
3.  在 **“属性”** 窗口中，找到 **CacheMode** 属性，然后从列表中选择 **KeepTrainingCases** 。  
  
4.  在 **“数据集”** 菜单上，选择 **“处理”**。  
  
## <a name="see-also"></a>另请参阅  
 [钻取查询（数据挖掘）](drillthrough-queries-data-mining.md)  
  
  
