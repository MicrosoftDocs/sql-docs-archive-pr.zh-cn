---
title: datetime 数据类型转换 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
author: rothja
ms.author: jroth
ms.openlocfilehash: 142e4388cb87055ddbc6faa7d5b1a92a627738c2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589031"
---
# <a name="datetime-data-type-conversions-odbc"></a>datetime 数据类型转换 (ODBC)
  以下转换或者已由 ODBC 定义，或者是 ODBC 的一致扩展。 每个访问接口提供的转换由该访问接口所服务的社区决定，因此，各个访问接口之间通常不一致。 方括号中的值是可选的。  
  
-   日期时间字符串的格式为 'yyyy-mm-dd[ hh:mm:ss[.9999999][ 加/减 hh:mm]]'  
  
-   时间字符串的格式为 'hh:mm:ss[.9999999]'  
  
-   日期字符串的格式为 'yyyy-mm-dd'  
  
 从字符串转换允许更灵活处理空格和字段宽度。 有关详细信息，请参阅[针对 ODBC 日期和时间改进的数据类型支持](data-type-support-for-odbc-date-and-time-improvements.md)中的 "数据格式：字符串和文字" 部分。  
  
 下面是一般的转换规则：  
  
-   如果未提供时间但接收方可存储时间，则将时间设置为零。  
  
-   如果不存在日期但接收方可以存储日期，则使用当前日期。  
  
-   如果客户端正在使用的数据类型中不存在时区，但服务器可以存储时区，则在客户端时区中存储日期。 请注意，此行为与服务器行为不同。  
  
-   如果服务器类型中不存在时区，但客户端类型具有时区，则先将时间转换为 UTC，再将其存储到服务器。  
  
-   如果存在时间但接收方无法存储时间，则忽略时间部分。  
  
-   如果存在日期但接收方无法存储日期，则忽略日期部分。  
  
-   如果在从 C 转换到 SQL 时截断了秒或秒的小数部分，则生成带有 SQLSTATE 22008 的诊断记录和消息“日期时间字段溢出”。  
  
-   如果在从 SQL 转换到 C 时截断了秒或秒的小数部分，则生成带有 SQLSTATE 01S07 的诊断记录和消息“截断小数部分”。  
  
## <a name="in-this-section"></a>本节内容  
 [由 C 转换为 SQL](datetime-data-type-conversions-from-c-to-sql.md)  
 列出了在从 C 类型转换到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/时间类型时要考虑的问题。  
  
 [由 SQL 转换为 C](datetime-data-type-conversions-from-sql-to-c.md)  
 列出了在从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期/时间类型转换到 C 类型时要考虑的问题。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;&#40;的日期和时间改进](date-and-time-improvements-odbc.md)  
  
  
