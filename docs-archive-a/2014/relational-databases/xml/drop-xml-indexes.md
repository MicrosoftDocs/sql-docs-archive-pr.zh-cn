---
title: 删除 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- dropping indexes
- XML indexes [SQL Server], dropping
ms.assetid: 7591ebea-34af-4925-8553-b2adb5b487c2
author: rothja
ms.author: jroth
ms.openlocfilehash: b7d4621cf2182b4587b12665a1cfe10ddbe0db3a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577426"
---
# <a name="drop-xml-indexes"></a>删除 XML 索引
  [DROP INDEX (Transact-SQL)](/sql/t-sql/statements/drop-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可用于删除现有的主（或辅助）XML 索引和非 XML 索引。 但是，任何 DROP INDEX 选项都不会应用于 XML 索引。 如果删除主 XML 索引，则会删除任何现有的辅助索引。  
  
 以后将逐步停止使用带有 *TableName.IndexName* 的 DROP 语法，并且 XML 索引不支持该语法。  
  
## <a name="example-creating-and-dropping-a-primary-xml-index"></a>示例：创建和删除主 XML 索引  
 在以下示例中，XML 索引是对 `xml` 类型列创建的。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create Primary XML index   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Verify the index creation.   
-- Note index type is 3 for xml indexes.  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'   
-- Drop the index.  
DROP INDEX PIdx_T_XmlCol ON T  
```  
  
 删除表后，也将自动删除其所有的 XML 索引。 但是，如果 XML 列存在 XML 索引，则不会从表中删除该列。  
  
 在以下示例中，XML 索引是对 `xml` 类型列创建的。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](../xml/compare-typed-xml-to-untyped-xml.md)。  
  
```  
CREATE TABLE TestTable(  
 Col1 int primary key,   
 Col2 xml (Production.ProductDescriptionSchemaCollection))   
GO  
```  
  
 此时，可以对 `Co12`创建主 XML 索引。  
  
```  
CREATE PRIMARY XML INDEX PIdx_TestTable_Col2   
ON TestTable(Col2)  
GO  
```  
  
## <a name="example-creating-an-xml-index-by-using-the-drop_existing-index-option"></a>示例：使用 DROP_EXISTING 索引选项创建 XML 索引  
 在以下示例中，XML 索引是针对列 (`XmlColx`) 创建的。 然后，针对不同的列 (`XmlColy`) 创建同名的另一个 XML 索引。 由于指定了 `DROP_EXISTING` 选项，因此将删除 (`XmlColx)` 现有的 XML 索引并为 (`XmlColy`) 创建新的 XML 索引。  
  
```  
DROP TABLE T  
GO  
CREATE TABLE T(Col1 int primary key, XmlColx xml, XmlColy xml)  
GO  
-- Create XML index on XmlColx.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColx)  
GO  
-- Create same name XML index on XmlColy.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlColy)   
WITH (DROP_EXISTING = ON)  
-- Verify the index is created on XmlColy.d.  
SELECT sc.name   
FROM   sys.xml_indexes si inner join sys.index_columns sic   
ON     sic.object_id=si.object_id and sic.index_id=si.index_id  
INNER  join sys.columns sc on sc.object_id=sic.object_id   
AND    sc.column_id=sic.column_id  
WHERE  si.name='PIdx_T_XmlCol'   
AND    si.object_id=object_id('T')  
```  
  
 此查询返回对其创建指定的 XML 索引的列的名称。  
  
## <a name="see-also"></a>另请参阅  
 [XML 索引 (SQL Server)](xml-indexes-sql-server.md)  
  
  
