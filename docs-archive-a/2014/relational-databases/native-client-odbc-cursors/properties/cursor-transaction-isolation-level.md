---
title: 游标事务隔离级别 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: rothja
ms.author: jroth
ms.openlocfilehash: 30f3dc8a9136a7cbe1d5897cb0bcc9fff8c35ab2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692400"
---
# <a name="cursor-transaction-isolation-level"></a>游标事务隔离级别
  游标的完整锁定行为基于由客户端设置的并发属性和事务隔离级别之间的交互。 ODBC 客户端使用[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION 或 SQL_COPT_SS_TXN_ISOLATION 属性设置事务隔离级别。 通过将并发和事务隔离级别选项的锁定行为进行组合，可以确定特定游标环境的锁定行为。  
  
 Native Client ODBC 驱动程序支持以下游标事务隔离级别 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ：  
  
-   已提交读 (SQL_TXN_READ_COMMITTED)  
  
-   未提交读 (SQL_TXN_READ_UNCOMMITTED)  
  
-   可重复读 (SQL_TXN_REPEATABLE_READ)  
  
-   可序列化 (SQL_TXN_SERIALIZABLE)  
  
-   快照 (SQL_TXN_SS_SNAPSHOT)  
  
 请注意，ODBC API 指定了其他事务隔离级别，但不支持这些级别 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驱动程序。  
  
## <a name="see-also"></a>另请参阅  
 [游标属性](cursor-properties.md)  
  
  
