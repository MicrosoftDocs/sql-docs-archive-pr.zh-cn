---
title: 合并数据 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bc2d5bffb6d7a12164a8643e9a790b32538f8979
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688973"
---
# <a name="combine-data-mds-add-in-for-excel"></a>合并数据（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，当你在发布前想要比较数据时，合并来自两个工作表的数据。 在此过程中，您将来自两个工作表中的数据合并到一个工作表中。 然后可以进行进一步的比较，并确定哪些数据（如果有）将发布到 MDS 存储库。  
  
## <a name="prerequisites"></a>先决条件  
  
-   必须具有包含 MDS 管理的数据的工作表。 有关详细信息，请参阅将[数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
-   必须具有包含要与 MDS 管理的数据合并的数据的工作表。 此工作表必须具有标题行。  
  
### <a name="to-combine-non-managed-data-into-an-mds-managed-sheet"></a>将非托管数据合并到 MDS 管理的工作表  
  
1.  在包含 MDS 管理的数据的工作表上，在 **“发布并验证”** 组中，单击 **“合并数据”**。  
  
2.  在 **“合并数据”** 对话框中的 **“要与 MDS 数据组合的范围”** 文本框旁，单击图标。 该对话框将收缩。  
  
3.  单击包含要合并的数据的工作表。  
  
4.  突出显示工作表上要合并的所有单元，包括标题行。  
  
5.  在 **“合并数据”** 对话框中，单击图标。 该对话框将展开。  
  
6.  对于为 MDS 实体列出的列，选择 **“相应列”** 下的列。 所有 MDS 列都不需要相应列。  
  
7.  单击 **“合并”**。 **SOURCE** 列将显示，指示数据是来自 MDS 还是外部源。  
  
## <a name="next-steps"></a>后续步骤  
  
-   若要查找 MDS 管理和外部数据之间的相似之处，请参阅[匹配相似数据 &#40;MDS Add-in for Excel&#41;](match-similar-data-mds-add-in-for-excel.md)。  
  
## <a name="see-also"></a>另请参阅  
 [MDS Add-in for Excel&#41;中加载数据 &#40;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [用于 Excel 的 MDS 外接程序中的数据质量匹配](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  
