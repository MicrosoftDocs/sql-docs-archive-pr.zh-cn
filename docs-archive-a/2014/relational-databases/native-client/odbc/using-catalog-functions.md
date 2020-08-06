---
title: 使用目录函数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, functions
- SQLLinkedCatalogs function
- SQL Server Native Client ODBC driver, catalog functions
- SQLLinkedServers function
- catalog functions [ODBC]
- functions [ODBC]
ms.assetid: 7773fb2e-06b5-4c4b-88e9-0ad9132ad273
author: rothja
ms.author: jroth
ms.openlocfilehash: 6cac35e658343f606c1953f265c752335c70d81f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590177"
---
# <a name="using-catalog-functions"></a>使用目录函数
  所有数据库都具有一个包含该数据中存储的数据的结构。 此结构的定义以及权限等其他信息存储在目录（作为一组系统表实现）中，也称为数据字典。  
  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序，应用程序可以通过调用 ODBC 目录函数来确定数据库结构。 目录函数返回结果集中的信息，这些函数是使用目录存储过程实现的，用于查询该目录中的系统表。 例如，应用程序可以请求包含系统上所有表的相关信息的结果集或包含特定表中的所有列的相关信息的结果集。 标准 ODBC 目录函数用于获取连接应用程序的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的目录信息。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持通过一个查询访问多个异类 OLE DB 数据源的数据的分布式查询。 访问远程 OLE DB 数据源的一种方法是将数据源定义为链接服务器。 可以通过使用[sp_addlinkedserver](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)来完成此操作。 定义链接服务器后，使用由四个部分组成的名称可以在 Transact-SQL 语句中引用该服务器上的对象：  
  
 *linked_server_name。 object_name*。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持两个有助于获取链接服务器的目录信息的特定于驱动程序的函数：  
  
-   **SQLLinkedServers**  
  
     返回定义到本地服务器的链接服务器列表。  
  
-   **SQLLinkedCatalogs**  
  
     返回链接服务器包含的目录的列表。  
  
 使用链接服务器名称和目录名称后， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序支持通过使用由两部分组成的名称来获取目录中的信息_linked_server_name_**。** 以下 ODBC 目录函数的*CatalogName* _目录_：  
  
-   **SQLColumnPrivileges**  
  
-   **SQLColumns**  
  
-   **SQLPrimaryKeys**  
  
-   **SQLStatistics**  
  
-   **SQLTablePrivileges**  
  
-   **SQLTables**  
  
 由两部分组成的_linked_server_name_**。**[SQLForeignKeys](../../native-client-odbc-api/sqlforeignkeys.md)上的*FKCatalogName*和*PKCatalogName*也支持_目录_。  
  
 使用 SQLLinkedServers 和 SQLLinkedCatalogs 需要以下文件：  
  
-   sqlncli.h  
  
     包括用于链接服务器目录函数的函数原型和常量定义。 必须在 ODBC 应用程序中包括 sqlncli.h，并且在编译应用程序时必须将其放在 include 路径中。  
  
-   sqlncli11.lib  
  
     必须放在链接器的库路径中，并将其指定为要链接的文件。 sqlncli11.lib 随 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序一起分发。  
  
-   sqlncli11.dll  
  
     在执行时必须存在。 sqlncli11.dll 随 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序一起分发。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)   
 [SQLColumnPrivileges](../../native-client-odbc-api/sqlcolumnprivileges.md)   
 [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)   
 [SQLPrimaryKeys](../../native-client-odbc-api/sqlprimarykeys.md)   
 [SQLTablePrivileges](../../native-client-odbc-api/sqltableprivileges.md)   
 [SQLTables](../../native-client-odbc-api/sqltables.md)   
 [SQLStatistics](../../statistics/statistics.md)  
  
  
