---
title: 第5课：创建关系 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: abac1a00-f827-4c3e-a473-6db5c8a3a66f
author: minewiskan
ms.author: owend
ms.openlocfilehash: f622f88d4d400fedf24e99059eda94882b1bcc3f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690849"
---
# <a name="lesson-5-create-relationships"></a>第 5 课：创建关系
  在本课中，将验证导入数据时自动创建的关系并在不同表之间添加新关系。 关系是在两个表之间建立的连接，用于确立这些表中的数据应该如何相关。 例如，Product 表和 Product Subcategory 表基于每个产品属于某个子类别的事实具有某种关系。 有关详细信息，请参阅[关系（SSAS 表格）](tabular-models/relationships-ssas-tabular.md)  
  
 本课预计完成时间：**10 分钟**  
  
## <a name="prerequisites"></a>必备条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 执行本课中的任务之前，应已完成上一课： [第 3 课：重命名列](rename-columns.md)。  
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>查看现有关系并添加新关系  
 当您使用“表导入向导”导入数据时，从 AdventureWorksDW 数据库导入了七个表。 通常，如果您从关系源中导入数据，则将自动导入现有关系以及数据。 但是，在继续创作模型之前，应验证是否已正确创建表之间的这些关系。 对于本教程，您还会添加三个新关系。  
  
#### <a name="to-review-existing-relationships"></a>查看现有关系  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”**** 菜单，然后指向“模型视图”****，再单击“关系图视图”****。  
  
     模型设计器现在以关系图视图显示，这是一种图形格式，显示已导入的所有表，并在这些表之间添加线条。 表之间的线条指示当您导入数据时自动创建的关系。  
  
     使用模型设计器右上角的 minimap 控件可调整此视图，以包括尽可能多的表。 还可以单击表并将其拖放到不同的位置，使表更加相互靠近，或者按特定的顺序排列它们。 移动表不会影响表之间已存在的关系。 若要查看特定表中的所有列，请单击并拖动表边缘以展开或使其变小。  
  
2.  单击 **Customer** 表与 **Geography** 表之间的实线。 这两个表之间的实线表明此关系处于活动状态，也即，当计算 DAX 公式时，默认情况下将使用此关系。  
  
     请注意， **Customer** 表中的 **Geography Id** 列和 **Geography** 表中的 **Geography Id** 列现在同时出现在一个框中。 这表明这些列是在关系中使用的列。 关系的属性现在也显示在 "**属性**" 窗口中。  
  
    > [!TIP]  
    >  除了在关系图视图中使用模型设计器以外，还可以使用 "**管理关系**" 对话框以表格格式显示所有表之间的关系。 单击“表”**** 菜单，然后单击“管理关系”****。 “管理关系”**** 对话框显示导入数据时自动创建的关系。  
  
3.  使用 "关系图" 视图中的模型设计器或 "**管理关系**" 对话框，验证在从 AdventureWorksDW 数据库导入每个表时创建的以下关系：  
  
    |活动|表|相关查找表|  
    |------------|-----------|--------------------------|  
    |是|**Customer [Geography Id]**|**Geography [Geography Id]**|  
    |是|**Product [Product Subcategory Id]**|**Product Subcategory [Product Subcategory Id]**|  
    |是|**Product Subcategory [Product Category Id]**|**Product Category [Product Category Id]**|  
    |是|**Internet Sales [Customer Id]**|**Customer [Customer Id]**|  
    |是|**Internet Sales [Product Id]**|**Product [Product Id]**|  
  
 如果上述表中的任何关系缺失，请验证您的模型包括以下各表：Customer、Date、Geography、Product、Product Category、Product Subcategory 和 Internet Sales。 如果将同一数据源连接中的表导入为独立的项，则不会创建这些表之间的任何关系，而必须手动创建。  
  
 在某些情况下，可能需要在模型中的表之间创建更多关系，以支持特定的业务逻辑。 对于本教程，您需要在 Internet Sales 表与 Date 表之间创建三个其他关系。  
  
#### <a name="to-add-new-relationships-between-tables"></a>在表之间添加新关系  
  
1.  在模型设计器中，在 **Internet Sales** 表中单击并按住 **Order Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条实线，说明已在 **Internet Sales** 表的 **Order Date** 列与 **Date** 表的 **Date** 列之间创建了活动的关系。  
  
    > [!NOTE]  
    >  当创建关系时，将自动正确地排列主表与相关查找表之间的顺序。  
  
2.  在 **Internet Sales** 表中单击并按住 **Due Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条点划线，说明已在 **Internet Sales** 表的 **Due Date** 列与 **Date** 表的 **Date** 列之间创建了非活动的关系。 可以在表之间创建多个关系，但每次只能有一个关系处于活动状态。  
  
3.  最后，再创建一个关系；在 **Internet Sales** 表中单击并按住 **Ship Date** 列，将光标拖到 **Date** 表中的 **Date** 列，然后松开。  
  
     将显示一条点划线，说明已在 **Internet Sales** 表的 **Ship Date** 列与 **Date** 表的 **Date** 列之间创建了非活动的关系。  
  
## <a name="next-step"></a>下一步  
 若要继续学习本课程，请转到下一课： [第 6 课：创建计算列](lesson-5-create-calculated-columns.md)。  
  
  
