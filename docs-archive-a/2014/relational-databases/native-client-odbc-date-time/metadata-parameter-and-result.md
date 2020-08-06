---
title: 参数和结果元数据 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
ms.assetid: 1518e6e5-a6a8-4489-b779-064c5624df53
author: rothja
ms.author: jroth
ms.openlocfilehash: 62cc3ef8121dd17a07874a805ae2c49587107829
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692398"
---
# <a name="parameter-and-result-metadata"></a>参数和结果元数据
  本主题介绍在日期和时间数据类型的实现参数描述符 (IPD) 和实现行描述符 (IRD) 字段中返回的内容。  
  
## <a name="information-returned-in-ipd-fields"></a>在 IPD 字段中返回的信息  
 在 IPD 字段中返回以下信息：  
  
|参数类型|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8，10，16|16|23|19、21..27|26、28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8，10，16|16|23|19、21..27|26、28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|`date`|`time`|在 IRD 中为 `smalldatetime`，在 IPD 中为 `datetime2`|在 IRD 中为 `datetime`，在 IPD 中为 `datetime2`|`datetime2`|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|空值|空值|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|空值|  
  
 有时，值范围中存在不连贯性。 例如，8,10..16 中缺少 9。 这是因为当小数精度大于零时添加了小数点。  
  
 会返回 `datetime2` 作为 `smalldatetime` 和 `datetime` 的类型名称，因为驱动程序将此类型用作常见类型以将所有 `SQL_TYPE_TIMESTAMP` 值传送到服务器。  
  
 SQL_CA_SS_VARIANT_SQL_TYPE 是一个新的描述符字段。 将此字段添加到 IRD 和 IPD 中是为了使应用程序能够指定与 `sqlvariant` (SQL_SSVARIANT) 列和参数关联的值类型。  
  
 SQL_CA_SS_SERVER_TYPE 是一个新的仅适用于 IPD 的字段，用于使应用程序能够控制如何将作为 SQL_TYPE_TYPETIMESTAMP（或具有 C 类型 SQL_C_TYPE_TIMESTAMP 的 SQL_SS_VARIANT）绑定的参数的值发送到服务器。 如果在调用 SQLExecute 或 SQLExecDirect 时，SQL_DESC_CONCISE_TYPE SQL_TYPE_TIMESTAMP (或 SQL_SS_VARIANT 并且 C 类型 SQL_C_TYPE_TIMESTAMP) ，则 SQL_CA_SS_SERVER_TYPE 的值将确定表格格式数据流 (的参数值类型，如下所示：  
  
|SQL_CA_SS_SERVER_TYPE 的值|SQL_DESC_PRECISION 的有效值|SQL_DESC_LENGTH 的有效值|TDS 类型|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19、21..27|`datetime2`|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|`smalldatetime`|  
|SQL_SS_TYPE_DATETIME|3|23|`datetime`|  
  
 SQL_CA_SS_SERVER_TYPE 的默认设置为 SQL_SS_TYPE_DEFAULT。 SQL_DESC_PRECISION 和 SQL_DESC_LENGTH 的设置用 SQL_CA_SS_SERVER_TYPE 的设置进行验证，如上表所述。 如果此验证失败，将返回 SQL_ERROR 并生成具有 SQLState 07006 和消息“受限制的数据类型属性冲突”的诊断记录。 如果将 SQL_CA_SS_SERVER_TYPE 设置为 SQL_SS_TYPE DEFAULT 之外的值并且 DESC_CONCISE_TYPE 不是 SQL_TYPE_TIMESTAMP，则也会返回此错误。 当在诸如以下的条件下进行描述符一致性验证时，将执行上述验证：  
  
-   当更改 SQL_DESC_DATA_PTR 时。  
  
-   在准备或执行时间（当调用 SQLExecute、SQLExecDirect、SQLSetPos 或 SQLBulkOperations 时）。  
  
-   当应用程序通过调用已禁用延迟准备的 SQLPrepare 来强制执行非延迟准备，或对已准备但未执行的语句调用 SQLNumResultCols、SQLDescribeCol 或 SQLDescribeParam。  
  
 如果 SQL_CA_SS_SERVER_TYPE 通过调用 SQLSetDescField 进行设置，则其值必须为 SQL_SS_TYPE_DEFAULT、SQL_SS_TYPE_SMALLDATETIME 或 SQL_SS_TYPE_DATETIME。 如果不是这样，将返回 SQL_ERROR 并生成具有 SQLState HY092 和消息“属性/选项标识符无效”的诊断记录。  
  
 依赖于 `datetime` 和 `smalldatetime` 而非 `datetime2` 支持的功能的应用程序可以使用 SQL_CA_SS_SERVER_TYPE 属性。 例如， `datetime2` 需要使用 `dateadd` 和**datediif**函数，而 `datetime` 和 `smalldatetime` 也允许使用算术运算符。 大多数应用程序将不需要使用此属性，而且应当避免使用此属性。  
  
## <a name="information-returned-in-ird-fields"></a>在 IRD 字段中返回的信息  
 在 IRD 字段中返回以下信息：  
  
|列类型|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8，10，16|16|23|19、21..27|26、28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8，10，16|16|23|19、21..27|26、28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8，10，16|16|2|19、21..27|26、28..34|  
|SQL_DESC_LITERAL_PREFIX|'|'|'|'|'|'|  
|SQL_DESC_LITERAL_SUFFIX|'|'|'|'|'|'|  
|SQL_DESC_LOCAL_TYPE_NAME|`date`|`time`|`smalldatetime`|`datetime`|`datetime2`|datetimeoffset|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|SQL_DESC_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|`date`|`time`|`smalldatetime`|`datetime`|`datetime2`|datetimeoffset|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|  
  
## <a name="see-also"></a>另请参阅  
 [Metadata &#40;ODBC&#41;](../../database-engine/dev-guide/metadata-odbc.md)  
  
  
