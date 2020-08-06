---
title: 使用 SQLXMLOLEDB 提供程序 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sample applications [SQLXML]
- SQLXMLOLEDB Provider, samples
- ClientSideXML property
ms.assetid: fbcefac5-29c9-478b-b0e0-d510b593f446
author: rothja
ms.author: jroth
ms.openlocfilehash: 74e3c53eecd657d610c2fe90e108e0290e9b05b2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587302"
---
# <a name="using-the-sqlxmloledb-provider-sqlxml-40"></a>使用 SQLXMLOLEDB 访问接口 (SQLXML 4.0)
  本节中的主题提供 ADO 示例应用程序，这些应用程序说明 SQLXMLOLEDB 访问接口特有的属性的用法。  
  
## <a name="application-requirements-for-sqlxmloledb-40-provider"></a>SQLXMLOLEDB 4.0 访问接口的应用程序要求  
 若要创建使用 SQLXMLOLEDB 4.0 的工作示例，必须执行以下操作：  
  
1.  创建 Microsoft Visual Basic .exe 应用程序，并添加以下引用之一：  
  
    -   Microsoft ActiveX 数据对象2.6 库  
  
    -   Microsoft ActiveX 数据对象2.7 库  
  
    -   Microsoft ActiveX Data Objects 2.8 Library  
  
2.  部署和安装 SQLXML 4.0 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
     有关详细信息，请参阅[SQLXML 4.0 编程概念](../../sqlxml/sqlxml-4-0-programming-concepts.md)和[安装 SQL Server Native Client](../../native-client/applications/installing-sql-server-native-client.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [&#40;SQLXMLOLEDB 提供程序执行 SQL 查询&#41;](executing-sql-queries-sqlxmloledb-provider.md)  
 说明如何使用 ClientSideXML 和 xml 根属性来执行 SQL 查询。  
  
 [&#40;SQLXMLOLEDB 提供程序执行包含 SQL 查询的模板&#41;](executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md)  
 说明如何使用 ClientSideXML 属性。  
  
 [&#40;SQLXMLOLEDB 提供程序执行 XPath 查询&#41;](executing-xpath-queries-sqlxmloledb-provider.md)  
 阐释 ClientSideXML、基路径和映射架构属性的用法。  
  
 [通过命名空间 &#40;SQLXMLOLEDB 提供程序执行 XPath 查询&#41;](executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md)  
 说明如何针对已限定命名空间的架构进行查询。  
  
 [&#40;SQLXMLOLEDB 提供程序执行包含 XPath 查询的模板&#41;](executing-templates-that-contain-xpath-queries-sqlxmloledb-provider.md)  
 说明如何使用 ClientSideXML、基路径和映射架构属性执行包含 SQL 查询的模板。  
  
 [&#40;SQLXMLOLEDB 提供程序应用 XSL 转换&#41;](applying-an-xsl-transformation-sqlxmloledb-provider.md)  
 说明如何使用 ClientSideXML 和 xsl 属性来应用 XSL 转换。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 的系统要求](../../native-client/system-requirements-for-sql-server-native-client.md)  
  
  
