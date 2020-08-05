---
title: SQLForeignKeys |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: rothja
ms.author: jroth
ms.openlocfilehash: a61e80867abb8ecb4d2628b74dc9956051c8e4ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580272"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过外键约束机制支持级联更新和删除操作。 如果在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 CASCADE 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_CASCADE。 如果未在 FOREIGN KEY 约束的 ON UPDATE 和/或 ON DELETE 子句中指定 NO ACTION 选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 则为 UPDATE_RULE 和/或 DELETE_RULE 列返回 SQL_NO_ACTION。  
  
 当任何**SQLForeignKeys**参数中存在无效值时， **SQLForeignKeys**将在执行时返回 SQL_SUCCESS。 当在这些参数中使用了无效值时， **SQLFetch**将返回 SQL_NO_DATA。  
  
 可以对静态服务器游标执行**SQLForeignKeys** 。 尝试对可更新的 (动态或键集) 游标执行**SQLForeignKeys**返回 SQL_SUCCESS_WITH_INFO，指示游标类型已更改。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驱动程序支持链接服务器上表的报告信息，方法是接受由两部分组成的*FKCatalogName*和*PKCatalogName*参数的名称： *Linked_Server_Name。 Catalog_Name*。  
  
## <a name="see-also"></a>另请参阅  
 [SQLForeignKeys 函数](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
