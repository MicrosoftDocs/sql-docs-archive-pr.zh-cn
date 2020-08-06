---
title: 使用 sql：映射 (SQLXML 4.0) 从生成的 XML 文档中排除架构元素 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c79ae005b9630fcbfcd16bfc22c2aeb21b7bf9e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586600"
---
# <a name="excluding-schema-elements-from-the-resulting-xml-document-using-sqlmapped-sqlxml-40"></a>使用 sql:mapped 从生成的 XML 文档中排除架构元素 (SQLXML 4.0)
  由于是默认映射，XSD 架构中的每个元素和属性都映射到数据库表/视图和列。 如果要在 XSD 架构中创建不映射到任何数据库表（视图）或列并且不在 XML 中显示的元素，可以指定 `sql:mapped` 批注。  
  
 如果架构不能修改或者架构用于验证来自其他源的 XML，并且架构还包含尚未存储在数据库中的数据，则 `sql:mapped` 批注尤为有用。 `sql:mapped` 批注不同于 `sql:is-constant`，因为未映射的元素和属性不出现在 XML 文档中。  
  
 `sql:mapped` 批注接受布尔值（0 = false，1 = true）。 可接受的值为 0、1、true 和 false。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>A. 指定 sql:mapped 批注  
 假定您有来自其他源的 XSD 架构。 此 XSD 架构由元素组成，该 **\<Person.Contact>** 元素具有**ContactID**、 **FirstName**、 **LastName**和**HomeAddress**属性。  
  
 将此 XSD 架构映射到 AdventureWorks 数据库中的 Contact 表时，将 `sql:mapped` 在**HomeAddress**特性上指定，因为 employees 表不会存储员工的家庭地址。 因此，在针对映射架构指定 XPath 查询时，此属性不会映射到数据库，并且不会在生成的 XML 文档中返回此属性。  
  
 为架构的其余部分进行默认映射。 **\<Person.Contact>** 元素映射到 person 表，所有属性都映射到 person 表中具有相同名称的列。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>针对架构测试示例 XPath 查询  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 sql-mapped.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 sql-mapped.xml 的相同目录中将该文件另存为 sql-mappedT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (MySchema.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 查询](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 结果集如下：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 请注意，结果中包含 ContactID、FirstName 和 LastName 但不包含 HomeAddress，因为映射架构为 `sql:mapped` 属性指定了值 0。  
  
## <a name="see-also"></a>另请参阅  
 [XSD 元素和属性到表和列的默认映射 &#40;SQLXML 4.0&#41;](default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  
