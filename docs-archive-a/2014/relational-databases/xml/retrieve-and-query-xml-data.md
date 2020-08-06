---
title: 检索和查询 XML 数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: rothja
ms.author: jroth
ms.openlocfilehash: d387d1b96a57dcc7100368779f8ec6078fad5c7e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688632"
---
# <a name="retrieve-and-query-xml-data"></a>检索和查询 XML 数据
  本主题说明查询 XML 数据必须指定的查询选项。 它还说明了当 XML 实例存储在数据库中时未保留的部分。  
  
##  <a name="features-of-an-xml-instance-that-are-not-preserved"></a><a name="features"></a> 未保留的 XML 实例的功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可保留 XML 实例的内容，但不会保留 XML 数据模型中认为是不重要的 XML 实例的某些方面。 这意味着检索到的 XML 实例可能与服务器中存储的实例不相同，但将包含同样的信息。  
  
### <a name="xml-declaration"></a>XML 声明  
 当将某个实例存储在数据库中时，不会保留该实例中的 XML 声明。 例如：  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 结果为 `<doc/>`。  
  
 当在 `xml` 数据类型实例中存储 XML 数据时，不会保留 XML 声明（如 `<?xml version='1.0'?>`）。 这是设计的结果。 将数据转换为类型后，XML 声明 ( # A1 及其特性 (版本/编码/独立) 会丢失 `xml` 。 XML 声明被视为对 XML 分析器的指令。 XML 数据在内部存储为 ucs-2。 XML 实例中所有其他 PI 均被保留。  
  
  
### <a name="order-of-attributes"></a>属性的顺序  
 不保留 XML 实例中的属性顺序。 查询存储在 `xml` 类型列中的 XML 实例时，所得 XML 中的属性顺序可能与原 XML 实例中的顺序不同。  
  
  
### <a name="quotation-marks-around-attribute-values"></a>属性值前后的引号  
 不保留属性值前后的单引号和双引号。 属性值作为名称和值对存储在数据库中。 不存储引号。 对 XML 实例执行 XQuery 时，将用属性值前后的双引号对所得 XML 进行序列化。  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 两个查询都返回 `<root a="1" />`。  
  
  
### <a name="namespace-prefixes"></a>命名空间前缀  
 不保留命名空间前缀。 对 `xml` 类型列指定 XQuery 时，序列化的 XML 结果可能会返回不同的命名空间前缀。  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 结果中的命名空间前缀可能会有所不同。 例如：  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="setting-required-query-options"></a><a name="query"></a> 设置所需的查询选项  
 `xml`使用数据类型方法查询类型列或变量时 `xml` ，必须按所示设置以下选项。  
  
|SET 选项|所需值|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 如果未按所示方式设置这些选项，则对数据类型方法的查询和修改 `xml` 将失败。  
  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 数据的实例](create-instances-of-xml-data.md)  
  
  
