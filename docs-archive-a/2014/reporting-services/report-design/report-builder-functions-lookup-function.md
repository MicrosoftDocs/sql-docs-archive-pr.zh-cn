---
title: Lookup 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 053fefff51e4b4e338e262664bd7570280c92540
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586408"
---
# <a name="lookup-function-report-builder-and-ssrs"></a>Lookup 函数（报表生成器和 SSRS）
  从包含名称/值对的数据集返回指定名称的第一个匹配值。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>参数  
 *source_expression*  
 (`Variant`) 在当前作用域中计算结果并指定要查找的名称或键的表达式。 例如，`=Fields!ProdID.Value` 。  
  
 *destination_expression*  
 (`Variant`) 针对数据集中的每行计算结果并指定要匹配的名称或键的表达式。 例如，`=Fields!ProductID.Value` 。  
  
 *result_expression*  
  (`Variant`) 为 dataset 中的行计算的表达式，其中*source_expression*  =  *destination_expression*，并指定要检索的值。 例如，`=Fields!ProductName.Value` 。  
  
 *数据集 (dataset)*  
 指定报表中数据集的名称的常量。 例如，“Products”。  
  
## <a name="return"></a>返回  
 返回 `Variant`，如果没有匹配项，则返回 `Nothing`。  
  
## <a name="remarks"></a>备注  
 使用 `Lookup` 从指定的数据集中为名称-值对（每对具有 1 对 1 关系）检索值。 例如，对于表中的 ID 字段，可以使用 `Lookup` 从未绑定到该数据区域的数据集检索对应的名称字段。  
  
 `Lookup` 执行下列操作：  
  
-   计算当前作用域中源表达式的结果。  
  
-   根据指定数据集的排序规则，在应用筛选器后对指定数据集的每行计算目标表达式的结果。  
  
-   对于源表达式和目标表达式的第一个匹配，计算数据集中该行的结果表达式。  
  
-   返回结果表达式值。  
  
 若要为单个名称或键字段检索多个值（具有 1 对多关系），请使用[LookupSet 函数（报表生成器和 SSRS）](report-builder-functions-lookupset-function.md)。 若要调用 `Lookup` 一组值，请使用[Multilookup 函数 &#40;报表生成器和 SSRS&#41;](report-builder-functions-lookup-function.md)。  
  
 存在以下限制：  
  
-   在应用所有筛选表达式后计算 `Lookup` 的结果。  
  
-   只支持一个级别的查找。 源、目标或结果表达式不能包含对查找函数的引用。  
  
-   源和目标表达式必须对同一数据类型计算结果。 返回类型和计算后的结果表达式的数据类型相同。  
  
-   源、目标和结果表达式不能包含对报表或组变量的引用。  
  
-   `Lookup` 不能作为以下报表项的表达式：  
  
    -   数据源的动态连接字符串。  
  
    -   数据集中的计算字段。  
  
    -   数据集中的查询参数。  
  
    -   数据集中的筛选器。  
  
    -   报表参数。  
  
    -   Report.Language 属性。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
## <a name="example"></a>示例  
 在以下示例中，假定将某个表绑定到包含一个用于产品标识符 ProductID 的字段的数据集。 一个单独的称为“Product”的数据集包含相应的产品标识符“ID”和产品名称“名称”。  
  
 在下面的表达式中，`Lookup` 将 ProductID 的值与名为“Product”的数据集的每行中的 ID 进行比较，当找到匹配项后，为该行返回“名称”字段的值。  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
