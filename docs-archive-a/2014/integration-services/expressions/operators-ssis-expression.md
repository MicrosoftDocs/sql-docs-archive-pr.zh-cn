---
title: 运算符（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 652f53ef639e63e4868dabeea3f49b9303336043
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691820"
---
# <a name="operators-ssis-expression"></a>运算符（SSIS 表达式）
  本部分介绍了表达式语言提供的运算符和表达式计算器使用的运算符优先级及结合性。  
  
 下表列出了本部分中有关运算符的主题。  
  
|操作员|说明|  
|--------------|-----------------|  
|[Cast（SSIS 表达式）](cast-ssis-expression.md)|将表达式从一种数据类型转换为另外一种数据类型。|  
|[()（括号）（SSIS 表达式）](parentheses-ssis-expression.md)|标识表达式的计算顺序。|  
|[+（相加）(SSIS)](add-ssis.md)|将两个数值表达式相加。|  
|[+（连接）（SSIS 表达式）](concatenate-ssis-expression.md)|连接两个表达式。|  
|[-（相减）（SSIS 表达式）](subtract-ssis-expression.md)|从第一个数值表达式的值中减去第二个数值表达式的值。|  
|[-（求反）（SSIS 表达式）](negate-ssis-expression.md)|对一个数值表达式求反。|  
|[*（相乘）（SSIS 表达式）](multiply-ssis-expression.md)|将两个数值表达式相乘。|  
|[除（SSIS 表达式）](divide-ssis-expression.md)|用第一个数值表达式除以第二个数值表达式。|  
|[（取模）（SSIS 表达式）](modulo-ssis-expression.md)|将第一个数据表达式的值除以第二个数据表达式的值后，提供整数余数。|  
|[&#124;&#124; &#40;逻辑或&#41; &#40;SSIS 表达式&#41;](logical-or-ssis-expression.md)|执行“逻辑或”运算。|  
|[&&（逻辑 AND）（SSIS 表达式）](logical-and-ssis-expression.md)|执行“逻辑与”运算。|  
|[\!（逻辑非）（SSIS 表达式）](logical-not-ssis-expression.md)|对布尔操作数求反。|  
|[&#124;（位异或）（SSIS 表达式）](bitwise-inclusive-or-ssis-expression.md)|对两个整数值执行“位或”运算。|  
|[^（位异或）（SSIS 表达式）](bitwise-exclusive-or-ssis-expression.md)|对两个整数值执行“位异或”运算。|  
|[&（位与）（SSIS 表达式）](bitwise-and-ssis-expression.md)|对两个整数值执行“位与”运算。|  
|[~ &#40;按位 Not&#41; &#40;SSIS 表达式&#41;](bitwise-not-ssis-expression.md)|对整数执行位求反运算。|  
|[==（等于）（SSIS 表达式）](equal-ssis-expression.md)|执行比较来确定两个表达式是否相等。|  
|[\!=（不等于）（SSIS 表达式）](unequal-ssis-expression.md)|通过比较来确定两个表达式是否不相等。|  
|[>（大于）（SSIS 表达式）](greater-than-ssis-expression.md)|通过比较来确定第一个表达式是否大于第二个表达式。|  
|[>（小于）（SSIS 表达式）](less-than-ssis-expression.md)|通过比较确定第一个表达式是否小于第二个表达式。|  
|[>=（大于或等于）（SSIS 表达式）](greater-than-or-equal-to-ssis-expression.md)|执行比较来确定第一个表达式是否大于或等于第二个表达式。|  
|[<=（小于或等于）（SSIS 表达式）](less-than-or-equal-to-ssis-expression.md)|通过比较确定第一个表达式是否小于或等于第二个表达式。|  
|[?:（条件）（SSIS 表达式）](conditional-ssis-expression.md)|根据布尔表达式的计算结果，返回两个表达式之一。|  
  
 有关优先级层次结构中各个运算符的位置的信息，请参阅 [Operator Precedence and Associativity](operator-precedence-and-associativity.md)。  
  
## <a name="see-also"></a>另请参阅  
 [函数（SSIS 表达式）](functions-ssis-expression.md)   
 [高级 Integration Services 表达式的示例](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services (SSIS) 表达式](integration-services-ssis-expressions.md)  
  
  
