---
title: 创建基于域的属性 (MDS Add-in for Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bda0c7f63ad380aaea5d980d2e729822ec9a3d22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576867"
---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>创建基于域的属性（用于 Excel 的 MDS 外接程序）
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，管理员在想要将列中的值限制为一组特定值时可以创建基于域的属性。  
  
 这些值可以已处于工作表中，也可以来自某一现有实体。  
  
> [!NOTE]  
>   如果用户在该约束列键入某个值，而不是从列表中进行选择，则错误在发布时将显示在 **$InputStatus$** 列中。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域和 **“资源管理器”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 &#40;Master Data Services&#41;](../administrators-master-data-services.md)。  
  
-   模型和实体必须已经存在。  
  
### <a name="to-perform-this-procedure"></a>若要执行此过程：  
  
1.  在 Excel 中，加载包含要约束的列（属性）的实体。 有关详细信息，请参阅将[数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
2.  单击要约束的列中的任意单元。  
  
3.  在 **“生成模型”** 组中，单击 **“特性属性”**。  
  
4.  在“特性属性”**** 对话框的“属性类型”**** 列表中，选择“约束列表(基于域)”****。  
  
5.  在 **“使用以下位置的值填充属性”** 列表中：  
  
    -   若要使用工作表中的值，请选择 **“所选列”**。 将使用所选列中的值创建新实体和新的临时表。  
  
    -   若要使用现有实体中的值，请选择该实体的名称。  
  
6.  如果您在前一步骤中选择 **“所选列”** ，则在 **“新实体名称”** 框中键入新实体的名称。 该名称可与列（属性）名称相同。  
  
7.  单击“确定”  。 列中的每个单元现在都有一个可供用户从中选择的值列表。  
  
## <a name="next-steps"></a>后续步骤  
  
-   若要在约束列表中添加和删除值，请加载属性基于的实体。 有关加载实体的详细信息，请参阅将[数据从 MDS 加载到 Excel](export-data-to-excel-from-master-data-services.md)中。  
  
## <a name="see-also"></a>另请参阅  
 [基于域的属性 &#40;Master Data Services&#41;](../domain-based-attributes-master-data-services.md)   
 [创建实体 &#40;MDS Add-in for Excel&#41;](create-an-entity-mds-add-in-for-excel.md)   
 [生成模型（用于 Excel 的 MDS 外接程序）](building-a-model-mds-add-in-for-excel.md)  
  
  
