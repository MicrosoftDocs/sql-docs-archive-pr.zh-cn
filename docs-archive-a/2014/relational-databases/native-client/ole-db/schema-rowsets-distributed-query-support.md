---
title: 架构行集中的分布式查询支持 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: rothja
ms.author: jroth
ms.openlocfilehash: 48b57bbf40590f8ad5c049268f25fe66d2f94357
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578846"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>架构行集中的分布式查询支持
  为了支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分布式查询， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB provider **IDBSchemaRowset**接口将返回链接服务器上的元数据。  
  
 如果 DBPROPSET_SQLSERVERSESSION 属性 SSPROP_QUOTEDCATALOGNAMES 是 VARIANT_TRUE，则可以为目录名称指定带引号的标识符（例如 "my.catalog"）。 当通过目录限制架构行集输出时， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序将识别包含链接服务器和目录名称的由两部分组成的名称。 对于下表中的架构行集，将两部分组成的目录名称指定为_linked_server_**。**_目录_将输出限制为命名链接服务器的适用目录。  
  
|架构行集|目录限制|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  若要将架构行集限制为来自链接服务器的所有目录，请使用语法 linked_server（其中，句点分隔符是名称规范的一部分）**。 该语法等同于将目录名称限制指定为 NULL，当链接服务器指示有不支持目录的数据源时也使用此语法。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序定义架构行集 LINKEDSERVERS，并返回注册为链接服务器的 OLE DB 数据源的列表。  
  
## <a name="see-also"></a>另请参阅  
 [架构行集支持 &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS 行集 &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  
