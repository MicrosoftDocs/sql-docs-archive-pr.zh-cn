---
title: DAY（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b7acac3f3949cbbd07adbe6382ea3d875f94cb2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689530"
---
# <a name="day-ssis-expression"></a>DAY（SSIS 表达式）
  返回一个整数，表示日期的“日”日期部分。  
  
## <a name="syntax"></a>语法  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 返回有效日期或日期格式的字符串的表达式。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>备注  
 如果参数为空，则 DAY 将返回空结果。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 与 DATEPART("Day", date) 相比，DAY 函数效果相同，但更简洁。  
  
## <a name="expression-examples"></a>表达式示例  
 以下示例返回日期文字中的日期数字。 如果日期格式是“mm/dd/yyyy”格式，则此示例将返回 23。  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示天的整数。  
  
```  
DAY(ModifiedDate)  
```  
  
 以下示例返回表示当前日期的“日”部分的整数。  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD（SSIS 表达式）](dateadd-ssis-expression.md)   
 [DATEDIFF（SSIS 表达式）](datediff-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](datepart-ssis-expression.md)   
 [MONTH（SSIS 表达式）](month-ssis-expression.md)   
 [YEAR（SSIS 表达式）](year-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
