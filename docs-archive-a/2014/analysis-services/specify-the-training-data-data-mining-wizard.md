---
title: " (数据挖掘向导) 中指定定型数据 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
ms.openlocfilehash: 87a802256d287a3e8e9e7fb65bbd91687cb71a4a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589240"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>指定定型数据（数据挖掘向导）
  可以使用 **“指定定型数据”** 页，确定要在挖掘结构中包括哪些列。 即使在所有模型中都不使用某些列，也可以选择将其包括在结构中。 例如，如果希望从挖掘模型中钻取到列，则您可以将其包括在结构中但不包括在模型中。  
  
 结构中包括的每个表至少需要一个键列。 选作键的列取决于该表是事例表还是嵌套表。 如果该表是嵌套表，则键通常还是可预测列，而不是关系外键。 若要了解嵌套键，请参阅[嵌套表（Analysis Services - 数据挖掘）](data-mining/nested-tables-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  不同的挖掘算法使用键的方式也不同。 若要了解不同种类的键，请参阅[内容类型（数据挖掘）](data-mining/content-types-data-mining.md)。  
  
 **有关详细信息：** [挖掘结构（Analysis Services - 数据挖掘）](data-mining/mining-structures-analysis-services-data-mining.md)、[挖掘模型列](data-mining/mining-model-columns.md)、[数据挖掘向导（Analysis Services - 数据挖掘）](data-mining/data-mining-wizard-analysis-services-data-mining.md)、[创建关系挖掘结构](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>选项  
 **表/列**  
 显示在向导上一页中选择的表和列。  
  
 **\<check box>**  
 选择挖掘结构中要包括的列。  
  
 如果数据源包括嵌套表或多个视图，请展开列列表以查看嵌套的表。  
  
 **Key**  
 选择此选项可将相应的列用作数据的唯一标识符。  
  
 对于事例表，键通常为唯一标识符。  
  
 对于嵌套表， **“键”** 指示关联事例上下文中行的标识符。  
  
 **输入**  
 选择此选项可在创建预测时使用相应的列。  
  
> [!NOTE]  
>  只有在创建挖掘结构的同时创建挖掘模型时，此列才可用。  
  
 **可预测**  
 如果选择此选项，则相应的表或列可以根据将来的额外输入来进行预测。  
  
 如果还将某个嵌套表标记为可预测的，则整个嵌套表都可预测。 如果嵌套表中没有标记为输入列或可预测列的列，则嵌套表将显示在挖掘结构中，但在模型中将被忽略。  
  
 **注意** ：只有在创建挖掘结构的同时创建挖掘模型时，此列才可用。  
  
 **建议**  
 单击此项可打开“提供相关列建议”**** 对话框，该对话框可根据 entropy 对数据样本进行分析，以标识与所选“可预测”**** 列最为相关的输入列。 此分析也适用于嵌套表列或基于 OLAP 源的挖掘结构。  
  
 **注意** ：只有在创建挖掘结构的同时创建挖掘模型时，此列才可用。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘向导 F1 帮助 &#40;Analysis Services 数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [在数据挖掘向导 &#40;建议相关列&#41;](suggest-related-columns-data-mining-wizard.md)   
 [在数据挖掘向导 &#40;指定表类型&#41;](specify-table-types-data-mining-wizard.md)   
 [指定数据挖掘向导 &#40;列的内容和数据类型&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
