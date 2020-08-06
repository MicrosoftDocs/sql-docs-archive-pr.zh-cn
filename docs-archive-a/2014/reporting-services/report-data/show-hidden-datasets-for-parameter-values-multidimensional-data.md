---
title: 为多维数据 (报表生成器和 SSRS) 的参数值显示隐藏的数据集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eb01c4ca-4fd6-4629-b595-f0d2565915df
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6f9c005b6e7c8927316c19a3302e32f4407f9885
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694265"
---
# <a name="show-hidden-datasets-for-parameter-values-for-multidimensional-data-report-builder-and-ssrs"></a>为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS）
  报表可能包括默认在“报表数据”窗格中不显示的自动生成的数据集（也称为隐藏数据集）。 这些数据集是用下列方法创建的：  
  
-   在用于多维数据库的某些查询设计器中，可以在查询窗格的筛选区域中指定要筛选的字段，并选择是否为筛选器创建查询参数。 如果选择参数选项，会自动创建报表数据集以便为报表参数提供有效的值。  
  
-   如果导入基于多维数据库的查询，则还可能将隐藏数据集包括在报表中。  
  
 无法通过向导使用隐藏数据集。  
  
 可以更改“报表数据”窗格中的视图以显示报表中的所有数据集。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-hidden-datasets"></a>显示隐藏数据集  
  
-   在“报表数据”窗格中，右键单击“数据集”文件夹，然后单击“显示隐藏数据集”  。  
  
## <a name="see-also"></a>另请参阅  
 [查询设计器 &#40;报表生成器&#41;](../query-designers-report-builder.md)   
 [Reporting Services 查询设计器](../reporting-services-query-designers.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)  
  
  
