---
title: 使用 SQL Server 默认结果集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
author: rothja
ms.author: jroth
ms.openlocfilehash: 18cd10dd95329f68a42497d2bea5ce63f345ceff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580257"
---
# <a name="using-sql-server-default-result-sets"></a>使用 SQL Server 默认结果集
  默认的 ODBC 游标属性包括：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 当这些属性设置为默认值时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序将使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认结果集。 默认结果集可用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持的任意 SQL 语句，并且是将整个结果集传输到客户端的最有效的方法。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]引入了对 (MARS) 的多个活动结果集的支持;应用程序现在可以为每个连接设置多个活动的默认结果集。 默认情况下未启用 MARS。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前，默认结果集不支持同一连接上具有多个活动语句。 对连接执行 SQL 语句后，服务器不接受来自该连接上的客户端的命令（取消结果集剩余内容的请求除外），直到结果集中的所有行均处理完毕。 若要取消部分处理的结果集的剩余部分，请调用[SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) ，并将*fOption*参数设置为 SQL_CLOSE。 若要完成部分处理的结果集并测试是否存在另一个结果集，请调用[SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)。 如果在完全处理默认结果集之前，ODBC 应用程序在连接句柄上尝试命令，则调用将生成 SQL_ERROR 并返回对**SQLGetDiagRec**的调用：  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>另请参阅  
 [如何实现游标](how-cursors-are-implemented.md)  
  
  
