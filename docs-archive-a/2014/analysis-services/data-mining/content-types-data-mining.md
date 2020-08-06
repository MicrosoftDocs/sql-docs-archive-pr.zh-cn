---
title: 数据挖掘)  (内容类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], content types
- KEY SEQUENCE column
- content types [data mining]
- attributes [data mining]
- DISCRETIZED column
- CONTINUOUS column
- CYCLICAL column
- ORDERED column
- discretized columns [data mining]
- discrete columns [Analysis Services]
- DISCRETE column
- KEY column
- KEY TIME column
- continuous columns
- coding [Data Mining]
ms.assetid: 2dacd968-70e8-4993-88b6-a6d36024a4e4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8e3400d904bc857bc282bb1ad9220c1e01fe5a4d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682452"
---
# <a name="content-types-data-mining"></a>内容类型（数据挖掘）
  在中， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 您可以为挖掘结构中的列定义物理数据类型，并在模型中使用该列时定义该列的逻辑内容类型。  
  
 “数据类型 ** ”确定在您创建挖掘模型时算法如何处理这些列中的数据。 定义列的数据类型可为算法提供有关列中的数据类型以及如何处理数据的信息。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的每种数据类型均支持用于数据挖掘的一种或多种内容类型。  
  
 “内容类型 ** ”描述列中包含的内容的行为。 例如，如果列中的内容以特定的间隔（如一周中的某几天）重复，则可以将该列的内容类型指定为循环。  
  
 有些算法要求提供特定的数据类型和特定的内容类型才能正常工作。 例如，Microsoft Naive Bayes 算法的输入不能为连续列，而且不能预测连续值。 某些内容类型（如 Key Sequence）只能由特定算法使用。 有关算法列表和每种算法所支持的内容类型，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](data-mining-algorithms-analysis-services-data-mining.md)。  
  
 下表介绍了数据挖掘中使用的内容类型，并标识了支持每种类型的数据类型。  
  
## <a name="discrete"></a>离散  
 “** ”意味着列包含数值之间没有连续体的有限数量的数值。 例如，性别列是一个典型的离散属性列，这是因为该数据表示特定数量的类别。  
  
 离散属性列中的值不能意味着排序，即使这些值为数值也是如此。 此外，即使用于离散列的值为数值，也无法计算小数值。 电话区号即为数值离散数据的典型示例。  
  
 所有的数据挖掘数据类型均支持 `Discrete` 内容类型。  
  
## <a name="continuous"></a>连续  
 “** ”意味着列包含的值表示某一允许中间值的范围中的数值数据。 与表示有限、可数数据的离散列不同，连续列表示可缩放度量，且数据可能包含无限数目的小数值。 温度列即为连续属性列的示例。  
  
 当一列中包含连续数值数据并且您知道这些数据应如何分布时，则有可能通过指定期望的值分布来提高分析的精确性。 您将在挖掘结构级别指定列分布。 因此，该设置将应用到基于该结构的所有模型。有关详细信息，请参阅[列分布（数据挖掘）](column-distributions-data-mining.md)。  
  
 以下数据类型支持 `Continuous` 内容类型：`Date`、`Double` 和 `Long`。  
  
## <a name="discretized"></a>离散化  
 “离散化”** 是将一组连续数据的值放入存储桶以便得到有限数量的可能值的过程。 只能离散数值数据。  
  
 因此，“discretized ** ”内容类型指示列中包含的值表示其中包括源自连续列的值的组或存储桶。 Bucket 被视为有序的离散值。  
  
 您可以手动离散数据，以确保获取所需的存储桶，也可以使用 SQL Server Analysis Services 中提供的离散化方法。 某些算法自动执行离散化。 有关详细信息，请参阅 [更改挖掘模型中列的离散化](change-the-discretization-of-a-column-in-a-mining-model.md)。  
  
 以下数据类型支持 `Discretized` 内容类型：`Date`、`Double`、`Long` 和 `Text`。  
  
## <a name="key"></a>密钥  
 “key ** ”内容类型意味着该列唯一标识一行。 在事例表中，键列通常为数值或文本标识符。 将内容类型设置为 `key` 可指示该列不应该用于分析，而仅应用于跟踪记录。  
  
 嵌套表也有键，但嵌套表键的用法稍有不同。 如果某列是您需要分析的属性，则在嵌套表中将内容类型设置为 `key`。 嵌套表键的值对于每个事例来说都必须唯一，但在整个事例集中可以重复。  
  
 例如，如果分析的是客户购买的产品，则可以对于事例表中 **CustomerID** 列将内容类型设置为键，然后对于嵌套表中 **PurchasedProducts** 列再次将内容类型设置为键。  
  
> [!NOTE]  
>  只有在使用已被定义为 Analysis Services 数据源视图的外部数据源中的数据时，嵌套表才可用。  
  
 以下数据类型支持此内容类型：`Date`、`Double`、`Long` 和 `Text`。  
  
## <a name="key-sequence"></a>键序列  
 “key sequence ** ”内容类型只能在顺序分析和聚类分析模型中使用。 将内容类型设置为 `key sequence` 时，它指示列包含表示一个事件序列的值。 这些值是有序值，但不必按等差排列。  
  
 以下数据类型支持此内容类型：`Double`、`Long`、`Text` 和 `Date`。  
  
## <a name="key-time"></a>键时间  
 “key time ** ”内容类型只能在时序模型中使用。 将内容类型设置为 `key time` 时，它指示值是有序值并表示时间刻度。  
  
 以下数据类型支持此内容类型：`Double`、`Long` 和 `Date`。  
  
## <a name="table"></a>表  
 “table ** ”内容类型指示列包含其中有一列或多列以及一行或多行的另一个数据表。 对于事例表中的任意特定行，此列可以包含多个值，所有的值均与父事例记录相关。 例如，如果主事例表包含一个客户列表，则可能有多个包含嵌套表的列，例如 **ProductsPurchased** 列和 **Hobbies** 列，嵌套表在 ProductsPurchased 列中列出了此客户过去购买的产品，而 Hobbies 列则列出了该客户的兴趣。  
  
 此列的数据类型始终为 `Table`。  
  
## <a name="cyclical"></a>Cyclical  
 “cyclical ** ”内容类型意味着列包含表示循环有序集的值。 例如，一周内顺序编号的七天便是循环有序集，因为第一天紧跟第七天。  
  
 循环列就内容类型而言既有序又离散。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中所有的数据挖掘数据类型都支持此内容类型。 但是，大多数算法将循环值视为离散值，不会进行特殊处理。  
  
## <a name="ordered"></a>已订购  
 “Ordered ** ”内容类型也指示列包含定义序列或顺序的值。 但是，在此内容类型中，用于排序的值并不表示该集中值之间的任何差或量级关系。 例如，如果有序属性列包含按照等级顺序从一到五排列的有关技术等级的信息，则技术等级之间的差并不包含什么暗示信息；技术等级五不一定比技术等级一好五倍。  
  
 有序属性列就内容类型而言是离散的。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中所有的数据挖掘数据类型都支持此内容类型。 但是，大多数算法会将有序值视为离散值，不会进行特殊处理。  
  
## <a name="classified"></a>Classified  
 除了前面列出的可通用于所有模型的内容类型以外，对于某些数据类型，还可以使用已分类列定义内容类型。 有关已分类列的详细信息，请参阅[已分类列（数据挖掘）](classified-columns-data-mining.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内容类型 &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [数据挖掘 &#40;的数据类型&#41;](data-types-data-mining.md)   
 [DMX&#41;的数据类型 &#40;](/sql/dmx/data-types-dmx)   
 [更改挖掘结构的属性](change-the-properties-of-a-mining-structure.md)   
 [挖掘结构列](mining-structure-columns.md)  
  
  
