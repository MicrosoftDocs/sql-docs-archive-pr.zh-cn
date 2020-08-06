---
title: 创建 XML 数据类型的变量和列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- xml data type [SQL Server], columns
ms.assetid: 8994ab6e-5519-4ba2-97a1-fac8af6f72db
author: rothja
ms.author: jroth
ms.openlocfilehash: 08b79888eb47634deaccc910b2ea3c93800b7c78
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692303"
---
# <a name="create-xml-data-type-variables-and-columns"></a>创建 XML 数据类型的变量和列
  `xml` 数据类型是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的内置数据类型，并有些类似于其他内置类型（如 `int` 和 `varchar`）。 与其他内置类型一样，在 `xml` 创建表作为变量类型、参数类型、函数返回类型或在[CAST 和 CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql)中时，可以使用数据类型作为列类型。  
  
## <a name="creating-columns-and-variables"></a>创建列和变量  
 若要创建 `xml` 类型列作为表的一部分，请使用 `CREATE TABLE` 语句，如下例所示：  
  
```  
CREATE TABLE T1(Col1 int primary key, Col2 xml)   
```  
  
 可以使用 `DECLARE statement` 创建 `xml` 类型的变量，如下例所示。  
  
```  
DECLARE @x xml   
```  
  
 可以通过指定 XML 架构集合创建类型化的 `xml` 变量，如下例所示。  
  
```  
DECLARE @x xml (Sales.StoreSurveySchemaCollection)  
```  
  
 若要将 `xml` 类型参数传递给存储过程，请使用 `CREATE PROCEDURE` 语句，如下例所示。  
  
```  
CREATE PROCEDURE SampleProc(@XmlDoc xml) AS ...   
```  
  
 可以使用 XQuery 来查询存储在列、参数或变量中的 XML 实例。 还可以使用 XML 数据操作语言 (XML DML) 对 XML 实例进行更新。 由于开发时 XQuery 标准未定义 XQuery DML，因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将 [XML 数据修改语言](/sql/t-sql/xml/xml-data-modification-language-xml-dml) 扩展插件引入 XQuery。 这些扩展插件使您可以执行插入、更新和删除操作。  
  
## <a name="assigning-defaults"></a>分配默认的 XML 实例  
 在表中，可以为 `xml` 类型的列分配默认 XML 实例。 可以通过两种方式提供默认的 XML：通过使用 XML 常量，或通过使用到 `xml` 类型的显式转换。  
  
 若要提供默认的 XML 作为 XML 常量，请使用下例所示的语法。 请注意，此字符串将显式转换为 `xml` 类型。  
  
```  
CREATE TABLE T (XmlColumn xml default N'<element1/><element2/>')  
```  
  
 若要提供默认的 XML 作为到 `CAST` 的显式 `xml`，请使用下例所示的语法。  
  
```  
CREATE TABLE T (XmlColumn xml   
                  default CAST(N'<element1/><element2/>' AS xml))  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还支持对 `xml` 类型列的 NULL 和 NOT NULL 约束。 例如：  
  
```  
CREATE TABLE T (XmlColumn xml NOT NULL)  
```  
  
## <a name="specifying-constraints"></a>指定约束  
 创建 `xml` 类型的列时，可以定义列级或表级的约束。 在下列情况下，请使用约束：  
  
-   无法在 XML 架构中表达业务规则。 例如，花店的交货地址必须在其营业地点周围 50 英里之内。 这可以编写为 XML 列的约束。 此约束可能涉及 `xml` 数据类型方法。  
  
-   您的约束涉及表中的其他 XML 列或非 XML 列。 例如，强制在 XML 实例中找到的客户 ID (`/Customer/@CustId`) 与 CustomerID 关系列中的值匹配。  
  
 可以为类型化或非类型化的 `xml` 数据类型列指定约束。 但在指定约束时，不能使用 [XML 数据类型方法](/sql/t-sql/xml/xml-data-type-methods) 。 同时，请注意 `xml` 数据类型不支持以下列和表约束：  
  
-   PRIMARY KEY/ FOREIGN KEY  
  
-   UNIQUE  
  
-   COLLATE  
  
     XML 提供了它自己的编码。 排序规则只适用于字符串类型。 `xml` 数据类型不是字符串类型。 但是，它有字符串表示形式并允许与字符串数据类型之间的相互转换。  
  
-   RULE  
  
 除了使用约束外，还可以创建用户定义函数作为包装来包装 `xml` 数据类型方法，并在检查约束中指定用户定义函数，如下例中所示。  
  
 在以下示例中， `Col2` 的约束指定此列中存储的每个 XML 实例都必须具有包含 `<ProductDescription>` 属性的 `ProductID` 元素。 此约束由如下用户定义函数强制执行：  
  
```  
CREATE FUNCTION my_udf(@var xml) returns bit  
AS BEGIN   
RETURN @var.exist('/ProductDescription/@ProductID')  
END  
GO  
```  
  
 注意，如果实例中的 `exist()` 元素包含 `xml` 属性，则 `1` 数据类型的 `<ProductDescription>` 方法返回 `ProductID` 。 否则，将返回 `0`。  
  
 现在，您就可以创建带有列级约束的表，如下所示：  
  
```  
CREATE TABLE T (  
    Col1 int primary key,   
    Col2 xml check(dbo.my_udf(Col2)=1))  
GO  
```  
  
 如下插入操作将成功：  
  
```  
INSERT INTO T values(1,'<ProductDescription ProductID="1" />')  
```  
  
 由于存在约束，因此如下插入操作失败：  
  
```  
INSERT INTO T values(1,'<Product />')  
```  
  
## <a name="same-or-different-table"></a>相同或不同的表  
 `xml`可以在包含其他关系列的表中创建数据类型列，也可以在具有与主表的外键关系的单独表中创建数据类型列。  
  
 `xml`如果满足以下条件之一，则在同一个表中创建数据类型列：  
  
-   您的应用程序对 XML 列执行数据检索，并且不需要 XML 列的 XML 索引。  
  
-   您想要对 `xml` 数据类型列生成 XML 索引，并且主表的主键与它的聚集键相同。 有关详细信息，请参阅 [XML 索引 (SQL Server)](xml-indexes-sql-server.md)。  
  
 如果符合下列条件，则在单独的表中创建 `xml` 数据类型列：  
  
-   您想要对 `xml` 数据类型列生成 XML 索引，但是主表的主键与它的聚集键不同，或者主表没有主键，或者主表为一个堆（没有聚集键）。 如果主表已存在，可能会这样。  
  
-   您不希望因为表中存在 XML 列而降低表扫描的速度。 无论该列是存储在行内还是行外，都会占用空间。  
  
  
