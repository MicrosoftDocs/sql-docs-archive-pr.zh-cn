---
title: 使用 XML 任务验证 XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- XML validation
- XML, validating
ms.assetid: 224fc025-c21f-4d43-aa9d-5ffac337f9b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 633a269f53c85353c956b33bff8fd3af518dad56
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576898"
---
# <a name="validate-xml-with-the-xml-task"></a>Validate XML with the XML Task
  通过启用 XML 任务的 `ValidationDetails` 属性，验证 XML 文档并获取丰富的错误输出。

 下面的屏幕快照显示 **XML 任务编辑器** ，其中包含具有丰富错误输出的 XML 验证所需的设置。

 ![XML 任务编辑器中的 XML 任务属性](../media/xmltaskproperties.jpg "XML 任务编辑器中的 XML 任务属性")

 在可以使用 `ValidationDetails` 属性之前，XML 任务的 XML 验证仅返回 true 或 false 结果，而不包含关于错误或其位置的详细信息。 现在，当你将 `ValidationDetails` 设置为 true 时，输出文件将包含关于每个错误的详细信息，包括行号和位置。 此信息可用于了解、查找和修复 XML 文档中的错误。

 XML 验证功能可轻松扩展以适应大型 XML 文档和大量错误。 由于输出文件本身采用 XML 格式，你可以查询和分析输出。 例如，如果输出中包含大量错误，你可以按本主题中所述，使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询对错误分组。

> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) `ValidationDetails` 在 Service Pack 2 中引入了属性 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 。 SQL Server 2016 中还提供了 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和中的属性。

## <a name="sample-output-for-xml-thats-valid"></a>有效的 XML 示例输出
 下面是有效 XML 文件的示例输出文件（带有验证结果）。

```xml

<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">
    <metadata>
        <result>true</result>
        <errors>0</errors>
        <warnings>0</warnings>
        <startTime>2015-05-28T10:27:22.087</startTime>
        <endTime>2015-05-28T10:29:07.007</endTime>
        <xmlFile>d:\Temp\TestData.xml</xmlFile>
        <xsdFile>d:\Temp\TestSchema.xsd</xsdFile>
    </metadata>
    <messages />
</root>
```

## <a name="sample-output-for-xml-thats-not-valid"></a>无效的 XML 示例输出
 下面是包含少量错误的 XML 文件的示例输出文件（带有验证结果）。 为便于阅读，\<error> 元素的文本已换行。

```xml

<root xmlns:ns="https://schemas.microsoft.com/xmltools/2002/xmlvalidation">
    <metadata>
        <result>false</result>
        <errors>2</errors>
        <warnings>0</warnings>
        <startTime>2015-05-28T10:45:09.538</startTime>
        <endTime>2015-05-28T10:45:09.558</endTime>
        <xmlFile>C:\Temp\TestData.xml</xmlFile>
        <xsdFile>C:\Temp\TestSchema.xsd</xsdFile>
    </metadata>
    <messages>
        <error line="5" position="26">The 'ApplicantRole' element is invalid - The value 'wer3' is invalid
    according to its datatype 'ApplicantRoleType' - The Enumeration constraint failed.</error>
        <error line="16" position="28">The 'Phone' element is invalid - The value 'we3056666666' is invalid
     according to its datatype 'phone' - The Pattern constraint failed.</error>
    </messages>
</root>
```

## <a name="analyze-xml-validation-output-with-a-transact-sql-query"></a>使用 Transact-SQL 查询分析 XML 验证输出
 如果 XML 验证输出中包含大量错误，你可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中加载输出。 然后可以使用 T-SQL 语言的所有功能（包括 WHERE、GROUP BY、ORDER BY，JOIN 等）对错误列表进行分析。

```sql
DECLARE @xml XML;

SELECT @xml = XmlDoc   
FROM OPENROWSET (BULK N'C:\Temp\XMLValidation_2016-02-212T10-41-00.xml', SINGLE_BLOB) AS Tab(XmlDoc);

-- Query # 1, flat list of errors
-- convert to relational/rectangular
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS
(
SELECT col.value('@line','INT') AS line
     , col.value('@position','INT') AS position
     , col.value('.','VARCHAR(1024)') AS error
FROM @XML.nodes('/root/messages/error') AS tab(col)
)
SELECT * FROM rs;
-- WHERE error LIKE '%whatever_string%'

-- Query # 2, count of errors grouped by the error message
-- convert to relational/rectangular
;WITH XMLNAMESPACES ('https://schemas.microsoft.com/xmltools/2002/xmlvalidation' AS ns), rs AS
(
SELECT col.value('@line','INT') AS line
     , col.value('@position','INT') AS position
     , col.value('.','VARCHAR(1024)') AS error
FROM @XML.nodes('/root/messages/error') AS tab(col)
)
SELECT COALESCE(error,'Total # of errors:') AS [error], COUNT(*) AS [counter]
FROM rs
GROUP BY GROUPING SETS ((error), ())
ORDER BY 2 DESC, COALESCE(error, 'Z');

```

 下面是上述文本中第二个示例查询在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的结果。

 ![用于在 Management Studio 中将 XML 错误分组的查询](../media/queryforxmlerrors.jpg "用于在 Management Studio 中将 XML 错误分组的查询")

## <a name="see-also"></a>另请参阅
 [Xml 任务](xml-task.md) [xml 任务编辑器 &#40;常规页&#41;](../xml-task-editor-general-page.md)


