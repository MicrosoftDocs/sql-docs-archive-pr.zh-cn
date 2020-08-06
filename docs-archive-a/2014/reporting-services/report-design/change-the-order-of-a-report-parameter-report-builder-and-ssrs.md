---
title: 更改报表参数的顺序（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ad9dd25be7a87fee089a48849fcc716e682e4c64
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692257"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>更改报表参数的顺序（报表生成器和 SSRS）
  当依赖参数位于它所依赖的参数之前时，需要更改报表参数的顺序。 当您有级联参数或希望在用户选择其他参数值之前向他们显示参数的默认值时，参数顺序非常重要。 依赖报表参数在其默认值查询或有效值查询中包含对一个查询参数的引用，该查询参数指向“报表数据”窗格的参数列表中该依赖报表参数之后的报表参数。  
  
 您所看到的报表查看器工具栏上显示参数的顺序由“报表数据”窗格中参数的顺序决定。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-order-of-report-parameters"></a>更改报表参数的顺序  
  
1.  在“报表数据”窗格中，展开“参数”节点。  
  
2.  单击参数，然后使用“报表数据”窗格工具栏上的向上和向下箭头按钮在列表中上下移动该参数。 下图显示报表生成器中的“报表数据”窗格。  
  
     ![“报表数据”窗格](../media/reportdatapane.png "“报表数据”窗格")  
  
## <a name="see-also"></a>另请参阅  
 [报表参数 &#40;报表生成器和报表设计器&#41;](report-parameters-report-builder-and-report-designer.md)   
 [报表生成器对话框、窗格和向导的帮助](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [向报表添加级联参数 &#40;报表生成器和 SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程：向报表添加参数 &#40;报表生成器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器 &#40;报表生成器和 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Parameters 集合引用（报表生成器和 SSRS）](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
