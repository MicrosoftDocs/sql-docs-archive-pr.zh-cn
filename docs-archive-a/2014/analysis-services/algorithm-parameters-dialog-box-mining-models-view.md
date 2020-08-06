---
title: "\"算法参数\" 对话框 (挖掘模型 \"视图) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
ms.openlocfilehash: 303d8b5bd3437690c65873e106a94cf2ce8eb9f0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579415"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>“算法参数”对话框（“挖掘模型”视图）
  可以使用 **“算法参数”** 对话框调整专用于选定模型的算法参数。 当更改算法参数时，将通常更改挖掘模型的结果。 每个参数对结果的影响方式取决于您使用的算法和数据。 有关详细信息，请参阅 [自定义挖掘模型和结构](data-mining/customize-mining-models-and-structure.md)。  
  
## <a name="options"></a>选项  
 **参数**  
 列出选定挖掘模型可用的参数。  
  
 下表对可用列进行了说明：  
  
|列|说明|  
|------------|-----------------|  
|**Parameter**|列出参数的名称。|  
|**值**|仅当要更改参数的默认值时才能输入新值。|  
|**Default**|如果没有在 **“值”** 列提供值，将列出算法使用的参数的默认值。|  
|**范围**|列出可以在 **“值”** 列中输入的可能值的范围。 范围可以是以下各项之一：<br /><br /> 离散列表，例如1、2、3<br /><br /> 包含范围，例如 [0，100]<br /><br /> 排他范围，如 (0,... ) <br /><br /> 组合，例如 [0,... ) |  
  
 **说明**  
 说明在“参数”**** 列表中选定的参数。  
  
 **添加**  
 单击此选项可以向列表中添加其他算法的特定参数。 添加参数以后，可以在 **“参数”** 列中输入正确的名称，在 **“值”** 列中提供值。  
  
 **移除**  
 单击此选项可以从列表中删除自定义参数。  
  
 如果从列表删除标准 Analysis Services 算法参数之一，模型仍会使用此参数，但将使用此参数的默认值。 此参数并不会永久删除，并将在下一次打开对话框时显示。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘算法 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [挖掘模型视图 &#40;数据挖掘模型设计器&#41;](mining-models-view-data-mining-model-designer.md)   
 [移动数据挖掘对象](data-mining/moving-data-mining-objects.md)  
  
  
