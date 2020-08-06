---
title: 将业务逻辑添加到 XML 数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- business logic [XML]
ms.assetid: 0877fb38-f1a2-43d8-86cf-4754be224dc1
author: rothja
ms.author: jroth
ms.openlocfilehash: 5bf8e9edc36e9c420faa92f2db1a92c311194e99
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580069"
---
# <a name="add-business-logic-to-xml-data"></a>将业务逻辑添加到 XML 数据
  可以采用多种方式将业务逻辑添加到 XML 数据中：  
  
-   您可以编写行或列约束，以在插入和修改 XML 数据时强制实施特定于域的约束。  
  
-   您可以在 XML 列上编写插入或更新列中的值时激发的触发器。 该触发器可以包含特定于域的验证规则或填充属性表。  
  
-   数据库引擎具有执行托管代码的能力。 您可以使用此公共语言运行时 (CLR) 集成使用托管代码编写要向其传递 XML 值的函数，并且使用 System.Xml 命名空间提供的 XML 处理功能。 例如，将 XSL 转换应用到 XML 数据。 另外，您可以将 XML 反序列化为一个或多个托管类，并使用托管代码对它们进行操作。  
  
-   您可以编写 Transact-SQL 存储过程和函数，对 XML 列进行处理以满足业务需要。  
  
## <a name="example-applying-xsl-transformation"></a>示例：应用 XSL 转换  
 假设有一个 CLR 函数**TransformXml ( # B1** ，该函数接受 `xml` 数据类型实例和存储在文件中的 XSL 转换，将转换应用于 XML 数据，然后在结果中返回转换的 XML。 以下是用 C# 编写的主干函数：  
  
```  
public static SqlXml TransformXml (SqlXml XmlData, string xslPath) {  
   // Load XSL transformation  
   XslCompiledTransform xform = new XslCompiledTransform();  
   XPathDocument xslDoc = new XPathDocument (xslPath);  
   xform.Load(xslDoc);  
  
   // Load XML data   
   XPathDocument xDoc = new XPathDocument (XmlData.CreateReader());  
  
   // Return the transformed value  
   MemoryStream xsltResult = new MemoryStream();  
   xform.Transform(xDoc, null, xsltResult);  
   SqlXml retSqlXml = new SqlXml(xsltResult);  
   return (retSqlXml);  
}   
```  
  
 注册程序集并创建用户定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数之后（ **SqlXslTransform()** 对应于 **TransformXml()** ），便可从 Transact-SQL 中调用该函数，如以下查询所示：  
  
```  
SELECT SqlXslTransform (xCol, 'C:\MyFile\xsltransform.xsl')  
FROM    T  
WHERE  xCol.exist('/book/title/text()[contains(.,"custom")]') =1;  
```  
  
 查询结果包含转换的 XML 的行集。  
  
 集成到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 CLR 扩展了这样一些可能性：将 XML 数据分解到多个表或属性提升，以及通过使用 System.Xml 命名空间中的托管类查询 XML 数据。 有关详细信息，请参阅 [XML 数据 (SQL Server)](xml-data-sql-server.md)。  
  
  
