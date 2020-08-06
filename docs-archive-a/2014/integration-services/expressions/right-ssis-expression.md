---
title: RIGHT（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2584ee33ecbf0436c4e3dc6e92b957e60ae396ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689980"
---
# <a name="right-ssis-expression"></a>RIGHT（SSIS 表达式）
  返回从给定字符表达式最右侧开始的指定数量的字符。  
  
## <a name="syntax"></a>语法  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>参数  
 *character_expression*  
 是从中提取字符的字符表达式。  
  
 *integer_expression*  
 指示要返回的字符数的整数表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_WSTR  
  
## <a name="remarks"></a>备注  
 如果 integer_expression 大于 character_expression 的长度，则该函数将返回 character_expression    。  
  
 如果 integer_expression 为 0，则该函数返回零长度的字符串  。  
  
 如果 integer_expression 为负数，则该函数返回一个错误  。  
  
 integer_expression 参数可使用变量和列  。  
  
 RIGHT 只能用于 DT_WSTR 数据类型。 如果 character_expression  参数是字符串文字或数据类型为 DT_STR 的数据列，则它在 RIGHT 执行操作前隐式转换为 DT_WSTR 数据类型。 其他数据类型必须显式转换为 DT_WSTR 数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)和[转换（SSIS 表达式）](cast-ssis-expression.md)。  
  
 如果任一参数为 Null，则 RIGHT 返回的结果为 Null。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例使用字符串文字。 返回结果为 `"Bike"`。  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 以下示例从 `Times` 列返回在 `Name` 变量中指定的最右边字符数。 如果 `Name` 为 `Touring Front Wheel` 且 `Times` 为 5，则返回结果为 `"Wheel"`。  
  
```  
RIGHT(Name, @Times)  
```  
  
 以下示例也从 `Times` 列中返回在 `Name` 变量中指定的最右边字符数。 `Times` 有非整数数据类型，而表达式包含到 DT_I2 数据类型的显式转换。 如果 `Name` 为 `Touring Front Wheel` ，并且 `Times` 为 `4.32`，返回结果将是 `"heel"` ，因为 RIGHT 函数将值 4.32 转换为 4，然后返回最右边的四个字符。  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>另请参阅  
 [LEFT（SSIS 表达式）](left-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
