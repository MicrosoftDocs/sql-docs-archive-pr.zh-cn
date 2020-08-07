---
title: 合并数据区域中的单元（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 43551300-89b2-4f4e-af09-69084324afaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c69ce8182bda3e0b644893e97b69280a003f5732
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691079"
---
# <a name="merge-cells-in-a-data-region-report-builder-and-ssrs"></a>合并数据区域中的单元（报表生成器和 SSRS）
  可通过合并数据区域中的单元来合并多个单元、改善数据区域外观或者为列组和行组提供跨越式标签。  
  
> [!NOTE]  
>  只能合并数据区域中同一个区内的单元，这些区包括：角部、列标题、组定义（或行标题）和正文。 不能合并跨区边界的单元。 例如，不能将数据区域角部区中的单元与行组区中的单元合并在一起。 有关 tablix 区域的详细信息，请参阅[列出 &#40;报表生成器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-merge-cells-in-a-data-region"></a>合并数据区域中的单元  
  
1.  在报表设计图面的数据区域中，单击第一个要合并的单元。 按住鼠标左键，垂直或水平拖动以选择相邻单元。 所选单元会突出显示。  
  
2.  右键单击所选单元并选择“合并单元”  。 所选单元将合并为一个单元。  
  
3.  重复步骤 1 和 2 可合并数据区域中的其他相邻单元。  
  
## <a name="see-also"></a>另请参阅  
 [Tablix 数据区域 &#40;报表生成器和 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)   
 [矩阵 &#40;报表生成器和 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [列出 &#40;报表生成器和 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
