---
title: DATEADD（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEADD
- dates [Integration Services]
- DATEADD function
ms.assetid: fa5c37b1-2ddc-4857-8f8e-f6d5643b654f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9feb288318bdf9705928cb930f175f5c170c384e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691825"
---
# <a name="dateadd-ssis-expression"></a>DATEADD（SSIS 表达式）
  将表示日期或时间间隔的数值与日期中指定的日期部分相加后，返回一个新的 DT_DBTIMESTAMP 值。 number 参数的值必须为整数，而 date 参数的取值必须为有效日期。  
  
## <a name="syntax"></a>语法  
  
```  
  
DATEADD(datepart, number, date)  
```  
  
## <a name="arguments"></a>参数  
 *datepart*  
 指定要与数值相加的日期部分的参数。  
  
 *数字*  
 用于与 datepart  相加的值。 该值必须是分析表达式时已知的整数值。  
  
 *date*  
 返回有效日期或日期格式的字符串的表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_DBTIMESTAMP  
  
## <a name="remarks"></a>备注  
 下表列出了表达式计算器可以识别的日期部分和缩写形式。 日期部分名称不区分大小写。  
  
|datepart|缩写形式|  
|--------------|-------------------|  
|年龄|yy、yyyy|  
|季度|qq、q|  
|月份|mm、m|  
|Dayofyear|dy、y|  
|日期|dd、d|  
|Week|wk、ww|  
|星期|dw、w|  
|Hour|Hh|  
|Minute|mi、n|  
|秒|ss、s|  
|Millisecond|Ms|  
  
 分拆表达式时必须提供 *number* 参数。 该参数可以是常量，也可以是变量。 由于分析表达式时列值是未知的，因此不能使用列值。  
  
 *datepart* 参数必须用英文引号括起来。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
 如果参数为空，则 DATEADD 返回空结果。  
  
 如果日期无效，日期或时间单元不是字符串，或者增量不是静态整数，则会发生错误。  
  
## <a name="ssis-expression-examples"></a>SSIS 表达式示例  
 以下示例将当前日期加上一个月。  
  
```  
DATEADD("Month", 1,GETDATE())  
```  
  
 以下示例将 **ModifiedDate** 列中的日期加上 21 天。  
  
```  
DATEADD("day", 21, ModifiedDate)  
```  
  
 以下示例将文字日期加上 2 年。  
  
```  
DATEADD("yyyy", 2, (DT_DBTIMESTAMP)"8/6/2003")  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEDIFF（SSIS 表达式）](datediff-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](datepart-ssis-expression.md)   
 [DAY（SSIS 表达式）](day-ssis-expression.md)   
 [MONTH（SSIS 表达式）](month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](year-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
