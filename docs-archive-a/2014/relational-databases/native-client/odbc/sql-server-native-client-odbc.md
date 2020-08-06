---
title: SQL Server Native Client (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: rothja
ms.author: jroth
ms.openlocfilehash: 16c73966e318ed1e7d326fa77f56195ebbd830df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690587"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client (ODBC)
  ODBC 是应用程序编程接口 (API) 的标准定义，可用于访问关系型数据库或索引的顺序访问方法 (ISAM) 数据库中的数据。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持 ODBC，并将其作为可用于编写与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 通信的 C 和 C++ 应用程序的本机 API 之一。  
  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序编写的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 程序通过 C 函数调用与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进行通信。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序中实现了特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ODBC 函数版本。 驱动程序将 SQL 语句传递给 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并将语句的结果返回给应用程序。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序符合 Microsoft Win32 ODBC 3.51 规范。 驱动程序按照 ODBC 3.51 规范中定义的方式支持使用 ODBC 早期版本编写的应用程序。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [数据源名称和 64 位操作系统](data-source-names-and-64-bit-operating-systems.md)  
  
-   [创建 SQL Server Native Client ODBC 驱动程序应用程序](creating-a-driver-application.md)  
  
-   [与 SQL Server &#40;ODBC&#41;通信](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [&#40;ODBC&#41;执行查询](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [&#40;ODBC&#41;处理结果](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [使用游标 &#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [&#40;ODBC&#41;执行事务](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [处理错误和消息](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [运行存储过程](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [使用目录函数](using-catalog-functions.md)  
  
-   [&#40;ODBC&#41;执行大容量复制操作](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [管理 Text 和 Image 列](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC 驱动程序性能事件探查](profiling-odbc-driver-performance.md)  
  
-   [ODBC&#41;&#40;表值参数](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [ODBC&#41;&#40;的日期和时间改进](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [&#40;ODBC&#41;的大型 CLR 用户定义类型](large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM 支持 &#40;ODBC&#41;](filestream-support-odbc.md)  
  
-   [客户端连接中的服务主体名称 (SPN) (ODBC)](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [稀疏列支持 &#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; 引用](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [ODBC 操作指南主题](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../sql-server-native-client-programming.md)   
 [安装 SQL Server Native Client](../applications/installing-sql-server-native-client.md)  
  
  
