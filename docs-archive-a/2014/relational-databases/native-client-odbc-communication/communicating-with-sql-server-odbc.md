---
title: 与 SQL Server (ODBC) 通信 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: rothja
ms.author: jroth
ms.openlocfilehash: c41ac2dcce9c5bdbdd351148d16bcaa8f067d22f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692402"
---
# <a name="communicating-with-sql-server-odbc"></a>与 SQL Server 通信 (ODBC)
  对于要与实例通信的 ODBC 应用程序 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，它必须分配环境和连接句柄并连接到数据源。 在建立连接后，应用程序可以向服务器发送查询并处理任意结果集。 应用程序使用完数据源后，它断开与数据源的连接并释放连接句柄。 应用程序释放所有连接句柄后，将释放环境句柄。  
  
 一个应用程序可以与任意数目的数据源连接。 该应用程序可以使用多个驱动程序和多个数据源的组合、同一驱动程序和多个数据源的组合，甚至可以使用同一驱动程序和指向同一数据源的多个连接。  
  
 你可以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从 MSDN 上的[SQL Server 下载](https://go.microsoft.com/fwlink/?LinkId=62796)"页下载 Native Client ODBC 示例。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [分配环境句柄](allocating-an-environment-handle.md)  
  
-   [分配连接句柄](allocating-a-connection-handle.md)  
  
-   [SQL Server Native Client ODBC 数据源](../../integration-services/connection-manager/data-sources.md)  
  
-   [&#40;ODBC 连接到数据源&#41;](connecting-to-a-data-source-odbc.md)  
  
-   [与数据源断开连接](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
