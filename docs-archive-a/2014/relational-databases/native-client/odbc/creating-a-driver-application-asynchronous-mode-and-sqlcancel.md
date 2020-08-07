---
title: 异步模式和 SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- asynchronous operations [SQL Server Native Client]
- SQLCancel function
- SQLSetConnectAttr function
- SQL Server Native Client, asynchronous operations
- ODBC functions
- ODBC applications, asynchronous operations
- SQL Server Native Client ODBC driver, asynchronous mode
ms.assetid: f31702a2-df76-4589-ac3b-da5412c03dc2
author: rothja
ms.author: jroth
ms.openlocfilehash: 9071c6821e6edeb577b639223e42899d2927bced
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588999"
---
# <a name="asynchronous-mode-and-sqlcancel"></a>异步模式和 SQLCancel
  某些 ODBC 函数既可同步操作，也可以异步操作。 应用程序可以为语句句柄或连接句柄启用异步操作。 如果为连接句柄设置了该选项，它将影响连接句柄上的所有语句句柄。 应用程序使用以下语句启用或禁用异步操作：  
  
```  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetConnectAttr(hdbc, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_ON, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ASYNC_ENABLE,  
                        SQL_ASYNC_ENABLE_OFF, SQL_IS_INTEGER);  
```  
  
 当某个应用程序以异步模式调用 ODBC 函数，在得到服务器已完成命令的通知之前，驱动程序不向应用程序返回控制权。  
  
 异步操作时，驱动程序立即向应用程序返回控制权，甚至在向服务器发送命令之前也可以。 驱动程序将返回代码设置为 SQL_STILL_EXECUTING。 应用程序随后可执行其他工作。  
  
 当应用程序测试命令是否完成时，它会向驱动程序发出带有相同参数的相同函数调用。 如果驱动程序尚未从服务器接收到回复，它将再次返回 SQL_STILL_EXECUTING。 应用程序必须定期测试该命令，直到返回 SQL_STILL_EXECUTING 之外的代码。 当应用程序收到其他任何返回代码（甚至是 SQL_ERROR）后，它可以确定命令是否已完成。  
  
 有时某个命令长时间未完成。 如果应用程序需要在不等待答复的情况下取消命令，则可以通过使用与未完成的命令相同的语句句柄调用**SQLCancel**来执行此操作。 这是唯一应该使用的**SQLCancel** 。 某些程序员在通过结果集处理部分方法时使用**SQLCancel** ，并希望取消结果集的其余部分。 应使用[SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md)或[SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md)来取消未完成的结果集的剩余部分，而不是**SQLCancel**。  
  
## <a name="see-also"></a>另请参阅  
 [创建 SQL Server Native Client ODBC 驱动程序应用程序](creating-a-driver-application.md)  
  
  
