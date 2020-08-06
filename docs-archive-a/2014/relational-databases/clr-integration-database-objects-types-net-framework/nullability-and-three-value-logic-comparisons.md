---
title: 为空性和三值逻辑比较 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 7b8000c1c28d5a1d3d129b6e8d01c4ab2fbbbc7d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693974"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>为 Null 性和三值逻辑比较
  如果您熟悉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，您会在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中的 `System.Data.SqlTypes` 命名空间中发现类似语义和精度。 但是，这些数据类型之间存在一些不同之处，本主题介绍了这些不同之处中最重要的内容。  
  
## <a name="null-values"></a>NULL 值  
 本机公共语言运行时 (CLR) 数据类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型之间的一个主要不同就是前者不允许 NULL 值，而后者提供了完整 NULL 语义。  
  
 NULL 值对比较会产生影响。 当对 x 和 y 两个值进行比较时，如果 x 或 y 其中一个为 NULL，则某些逻辑比较将为 UNKNOWN 值而不是 True 或 False。  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean 数据类型  
 `System.Data.SqlTypes` 命名空间引入了一个 `SqlBoolean` 类型以表示该三值逻辑。 在任何 `SqlTypes` 之间进行比较将返回一个 `SqlBoolean` 值类型。 UNKNOWN 值由 `SqlBoolean` 类型的 Null 值表示。 提供了属性 `IsTrue`、`IsFalse` 和 `IsNull` 来检查 `SqlBoolean` 类型的值。  
  
## <a name="operations-functions-and-null-values"></a>操作、函数和 NULL 值  
 所有算术运算符 (+、-、 \* 、/、% ) 、按位运算符 (~、& 和 |) ，如果的任何操作数或参数为 null，则大多数函数都返回 NULL `SqlTypes` 。 `IsNull` 属性始终返回一个 True 或 False 值。  
  
## <a name="precision"></a>精度  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中的 decimal 数据类型较 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 numeric 和 decimal 数据类型具有不同的最大值。 另外，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，decimal 数据类型假设具有最大精度。 但是，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 CLR 中，`SqlDecimal` 提供了与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 decimal 数据类型相同的最大精度和小数位数以及相同的语义。  
  
## <a name="overflow-detection"></a>溢出检测  
 在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR 中，两个很大的数字相加可能不会引发异常。 相反，如果未使用检查运算符，则返回的值可能作为负整数“环绕”。 在 `System.Data.SqlTypes` 中，所有上溢和下溢错误以及被零除错误均会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](sql-server-data-types-in-the-net-framework.md)  
  
  
