---
title: MONTH（SSIS 表达式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d1f56906b4d25f2ba01f54fbdbc404d2c9ae4704
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581391"
---
# <a name="month-ssis-expression"></a>MONTH（SSIS 表达式）
  返回一个表示日期中的“月份”日期部分的整数。  
  
## <a name="syntax"></a>语法  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>参数  
 *date*  
 是任意日期格式的日期。  
  
## <a name="result-types"></a>结果类型  
 DT_I4  
  
## <a name="remarks"></a>备注  
 如果参数为空，则 MONTH 返回的结果为空。  
  
 日期文字必须显式转换为日期数据类型之一。 有关详细信息，请参阅 [Integration Services 数据类型](../data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  在日期文本显式转换为以下日期数据类型之一时，表达式验证失败：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 MONTH 函数更为简要，但等价于使用 DATEPART("Month", date)。  
  
## <a name="expression-examples"></a>表达式示例  
 此示例返回日期文字中表示月份的数字。 如果日期是“mm/dd/yyyy”格式，则此示例返回 11。  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 此示例返回 **ModifiedDate** 列中表示月份的整数。  
  
```  
MONTH(ModifiedDate)  
```  
  
 此示例返回表示当前日期中的月份的整数。  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>另请参阅  
 [DATEADD（SSIS 表达式）](dateadd-ssis-expression.md)   
 [DATEDIFF（SSIS 表达式）](datediff-ssis-expression.md)   
 [DATEPART（SSIS 表达式）](datepart-ssis-expression.md)   
 [DAY（SSIS 表达式）](day-ssis-expression.md)   
 [YEAR（SSIS 表达式）](year-ssis-expression.md)   
 [函数（SSIS 表达式）](functions-ssis-expression.md)  
  
  
