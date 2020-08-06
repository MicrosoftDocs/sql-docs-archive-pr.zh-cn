---
title: " (DTA) 的索引元素 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 110dcd8ef5f554bdf1c59ab9a15984ec8ca97c65
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690974"
---
# <a name="index-element-dta"></a>索引元素 (DTA)
  包含为用户指定的配置创建或删除的索引的信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>元素属性  
  
|索引属性|数据类型|说明|  
|---------------------|---------------|-----------------|  
|`Clustered`|`boolean`|可选。 指定一个聚集索引。 设置为“true”或“false”，例如：<br /><br /> `<Index Clustered="true">`<br /><br /> 默认情况下，此属性设置为“false”。|  
|`Unique`|`boolean`|可选。 指定唯一索引。 设置为“true”或“false”，例如：<br /><br /> `<Index Unique="true">`<br /><br /> 默认情况下，此属性设置为“false”。|  
|`Online`|`boolean`|可选。 指定可在服务器联机时执行操作的索引，执行这些操作需要临时磁盘空间。 设置为“true”或“false”，例如：<br /><br /> `<Index Online="true">`<br /><br /> 默认情况下，此属性设置为“false”。<br /><br /> 有关详细信息，请参阅 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)。|  
|`IndexSizeInMB`|`double`|可选。 以兆字节为单位指定索引的最大大小，例如：<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> 无默认设置。|  
|`NumberOfRows`|`integer`|可选。 模拟不同的索引大小，这可有效地模拟不同的表大小，例如：<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> 无默认设置。|  
|`QUOTED_IDENTIFIER`|`boolean`|可选。 使 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遵从关于引号分隔标识符和文字字符串的 ISO 规则。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](/sql/t-sql/statements/set-quoted-identifier-transact-sql)。|  
|`ARITHABORT`|`boolean`|可选。 在查询执行过程中发生溢出或被零除错误时终止查询。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET ARITHABORT (Transact-SQL)](/sql/t-sql/statements/set-arithabort-transact-sql)。|  
|`CONCAT_NULL_YIELDS_`<br /><br /> `NULL`|`boolean`|可选。 控制是将串联结果视为空值还是空字符串值。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)。|  
|`ANSI_NULLS`|`boolean`|可选。 指定在与空值一起使用等于 (=) 和不等于 (<>) 比较运算符时，这些运算符遵从 ISO 标准的行为。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET ANSI_NULLS (Transact-SQL)](/sql/t-sql/statements/set-ansi-nulls-transact-sql)。|  
|`ANSI_PADDING`|`boolean`|可选。 控制列对于长度比其定义大小短的值的存储方式。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET ANSI_PADDING (Transact-SQL)](/sql/t-sql/statements/set-ansi-padding-transact-sql)。|  
|`ANSI_WARNINGS`|`boolean`|可选。 对几种错误情况指定 ISO 标准行为。 如果是对计算列或视图建立的索引，则必须打开此属性。 例如，下面的语法可以打开此属性：<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET ANSI_WARNINGS (Transact-SQL)](/sql/t-sql/statements/set-ansi-warnings-transact-sql)。|  
|`NUMERIC_ROUNDABORT`|`boolean`|可选。 指定当表达式中的舍入导致精度损失时生成的错误报告级别。 如果索引位于计算列或视图上，则必须禁用此属性。<br /><br /> 以下语法将启用此属性：<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 默认情况下，关闭此属性。<br /><br /> 有关详细信息，请参阅 [SET NUMERIC_ROUNDABORT (Transact-SQL)](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)。|  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|如果未使用 `Create` 或 `Drop` 元素指定其他物理设计结构，则每个 `Statistics` 或 `Heap` 元素均需出现一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[创建元素 (DTA)](create-element-dta.md)<br /><br /> `Drop`Element. 有关详细信息，请参阅数据库引擎优化顾问 XML 架构。|  
|**子元素**|[索引的名称元素 (DTA)](name-element-for-index-dta.md)<br /><br /> [索引的列元素 (DTA)](column-element-for-index-dta.md)<br /><br /> `PartitionScheme`Element. 有关详细信息，请参阅数据库引擎优化顾问 XML 架构。<br /><br /> `PartitionColumn`Element. 有关详细信息，请参阅数据库引擎优化顾问 XML 架构。<br /><br /> [索引的文件组元素 (DTA)](filegroup-element-for-index-dta.md)<br /><br /> `NumberOfReferences`Element. 有关详细信息，请参阅数据库引擎优化顾问 XML 架构。<br /><br /> `PercentUsage`Element. 有关详细信息，请参阅数据库引擎优化顾问 XML 架构。|  
  
## <a name="example"></a>示例  
 有关此元素的用法示例，请参阅[使用用户指定配置 (DTA) 的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
