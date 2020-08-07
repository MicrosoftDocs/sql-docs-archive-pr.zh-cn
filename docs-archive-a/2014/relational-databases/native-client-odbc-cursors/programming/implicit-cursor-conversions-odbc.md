---
title: ODBC)  (的隐式游标转换 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: rothja
ms.author: jroth
ms.openlocfilehash: ff8350c71a853e39ff1d35a1f3fba6e8e1944934
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589039"
---
# <a name="implicit-cursor-conversions-odbc"></a>隐式游标转换 (ODBC)
  应用程序可以通过[SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)请求游标类型，然后执行所请求类型的服务器游标不支持的 SQL 语句。 对**SQLExecute**或**SQLExecDirect**的调用将返回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**返回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 应用程序可以通过调用**SQLGetStmtOption**设置为 SQL_CURSOR_TYPE 来确定目前正在使用的游标类型。 游标类型转换仅适用于一个语句。 下一个**SQLExecDirect**或**SQLExecute**将使用原始语句游标设置完成。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC&#41;的游标编程详细信息 &#40;](cursor-programming-details-odbc.md)  
  
  
