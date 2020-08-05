---
title: 聚合转换编辑器 (聚合 "选项卡) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 30cafb68a69a061fe4b79e832f356b82926c9761
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579721"
---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>聚合转换编辑器（“聚合”选项卡）
  可以使用 **“聚合转换编辑器”** 对话框的 **“聚合”** 选项卡指定聚合的列以及聚合属性。 可以应用多个聚合。 此转换不生成错误输出。  
  
> [!NOTE]  
>  对于键计数、键范围、非重复键计数和非重复键范围的选项来说，如果是在“高级”**** 选项卡中指定的，则会应用于组件级；如果是在“聚合”**** 选项卡的高级显示部分中指定的，则会应用于输出级；而如果是在“聚合”**** 选项卡底部的列列表中指定的，则会应用于列级。  
>   
>  在聚合转换中， **“键”** 和 **“键范围”** 是指期望 **“分组依据”** 操作产生的组数。 **“非重复键计数”** 和 **“非重复键数范围”** 是指期望 **“非重复计数”** 操作产生的非重复值的数量。  
  
 若要了解有关聚合转换的详细信息，请参阅 [Aggregate Transformation](data-flow/transformations/aggregate-transformation.md)。  
  
## <a name="options"></a>选项  
 **高级/基本**  
 显示或隐藏为多个输出配置多个聚合的选项。 默认情况下，隐藏“高级”选项。  
  
 **聚合名**  
 在“高级”显示中，键入聚合的友好名称。  
  
 **按列分组**  
 在“高级”显示中，通过使用下面描述的“可用输入列”**** 列表，选择用于分组的列。  
  
 **键范围**  
 在“高级”显示中，根据需要指定聚合可写入的键的大致数目。 默认情况下，此选项的值为 **“未指定”**。 如果同时设置了 **“键范围”** 和 **“键”** 属性，则 **“键”** 的值优先。  
  
|值|说明|  
|-----------|-----------------|  
|未指定|不使用“键范围”属性。|  
|低|聚合可以写入大约 500,000 个键。|  
|中型|聚合可以写入大约 5,000,000 个键。|  
|高|聚合可以写入 25,000,000 个以上的键。|  
  
 **“键”**  
 在“高级”显示中，根据需要指定聚合可写入的键的精确数目。 如果同时指定了 **“键范围”** 和 **“键”** ，则 **“键”** 优先。  
  
 **可用输入列**  
 通过使用此表中的复选框，从可用输入列列表中选择。  
  
 **输入列**  
 从可用输入列的列表中进行选择。  
  
 **输出别名**  
 为每一列键入一个别名。 默认值为输入列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **操作**  
 参照下表，从可用操作列表中选择。  
  
|Operation|说明|  
|---------------|-----------------|  
|**GroupBy**|将数据集划分为组。 可以将任何数据类型的列用于分组。 有关详细信息，请参阅 GROUP BY。|  
|**长度**|对列中的值求和。 只能对数值数据类型的列求和。 有关详细信息，请参阅 SUM。|  
|**平均值**|返回列中值的平均值。 只能对数值数据类型的列求平均值。 有关详细信息，请参阅 AVG。|  
|**Count**|返回组中的项数。 有关详细信息，请参阅 COUNT。|  
|**CountDistinct**|返回组中的唯一非空值的数量。 有关详细信息，请参阅 COUNT 和 DISTINCT。|  
|**最低**|返回组中的最小值。 只限于数值数据类型。|  
|最大值|返回组中的最大值。 只限于数值数据类型。|  
  
 **比较标志**  
 如果选择“分组依据”****，请使用复选框来控制转换如何执行比较。 有关字符串比较选项的信息，请参阅 [Comparing String Data](data-flow/comparing-string-data.md)。  
  
 **Count Distinct Scale**  
 根据需要，可以指定聚合能够写入的非重复值的大致数目。 默认情况下，此选项的值为 **“未指定”**。 如果同时 `CountDistinctScale` 指定了和**CountDistinctKeys** ，则**CountDistinctKeys**优先。  
  
|值|说明|  
|-----------|-----------------|  
|未指定|不使用 `CountDistinctScale` 属性。|  
|低|聚合可以写入大约 500,000 个非重复值。|  
|中型|聚合可以写入大约 5,000,000 个非重复值。|  
|高|聚合可以写入 25,000,000 个以上的非重复值。|  
  
 **Count Distinct Keys**  
 根据需要，可以指定聚合能够写入的非重复值的精确数目。 如果同时 `CountDistinctScale` 指定了和**CountDistinctKeys** ，则**CountDistinctKeys**优先。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [聚合转换编辑器 &#40;高级 "选项卡&#41;](../../2014/integration-services/aggregate-transformation-editor-advanced-tab.md)   
 [使用聚合转换来聚合数据集中的值](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
