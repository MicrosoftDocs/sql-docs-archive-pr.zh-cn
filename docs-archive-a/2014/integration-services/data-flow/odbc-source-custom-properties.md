---
title: ODBC 源自定义属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f828bbf5394a2474aaa9367f9c31ab66941564a8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579678"
---
# <a name="odbc-source-custom-properties"></a>ODBC Source Custom Properties
  下表介绍 ODBC 源的自定义属性。 所有属性都可以从 SSIS 属性表达式设置。  
  
|属性名称|数据类型|说明|  
|-------------------|---------------|-----------------|  
|连接|ODBC 连接|用于访问源数据库的 ODBC 连接。|  
|AccessMode|Integer（枚举）|用来访问数据库的模式。 可能的值为表名 (0) 和 SQL 命令 (1)。<br /><br /> 默认值为表名 (0)。|  
|BatchSize|Integer|用于大容量提取的批处理的大小。 这是作为数组提取的记录数。 如果所选的 ODBC 访问接口不支持数组，则批处理大小为 1。|  
|BindCharColumnAs|Integer（枚举）|此属性确定 ODBC 源如何绑定具有多字节字符串类型的列，例如 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR。<br /><br /> 可能值为 Unicode (0)，这是将列绑定为 SQL_C_WCHAR；值还可以是 ANSI (1)，这是将列绑定为 SQL_C_CHAR。 默认值为 Unicode (0)。<br /><br /> **注意**：此属性未在 **“OLE 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。|  
|BindNumericAs|Integer（枚举）|此属性确定 ODBC 源如何将具有数字数据的列与数据类型 SQL_TYPE_NUMERIC 和 SQL_TYPE_DECIMAL 进行绑定。<br /><br /> 可能选项为 Char (0)，这是将列绑定为 SQL_C_CHAR；选项还可以是 Numeric (1)，这是将列绑定为 SQL_C_NUMERIC。 默认值为 Char (0)。<br /><br /> **注意**：此属性未在 **“OLE 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。|  
|DefaultCodePage|Integer|要用于字符串输出列的代码页。<br /><br /> **注意**：此属性未在 **“OLE 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。|  
|ExposeCharColumnsAsUnicode|Boolean|此属性确定组件如何公开 CHAR 列。 默认值为 False，指示 CHAR 列作为多字节字符串 (DT_STR) 公开。 如果为 True，则 CHAR 列将作为宽字符串 (DT_WSTR) 公开。<br /><br /> **注意**：此属性未在 **“OLE 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。|  
|FetchMethod|Integer（枚举）|用于获取数据的方法。 可能的选项为逐行 (0) 和批处理 (1)。 默认值为批处理 (1)。<br /><br /> 有关这些选项的详细信息，请参阅 [ODBC Source](odbc-source.md)。<br /><br /> **注意**：此属性未在 **“OLE 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。|  
|SqlCommand|String|在 AccessMode 设置为“SQL 命令”时要执行的 SQL 命令。|  
|StatementTimeout|Integer|在无错返回应用程序之前等待 SQL 语句执行的秒数。 默认值为 0。 值为 0 时指示系统不会超时。|  
|TableName|String|具有在 AccessMode 设置为“表名”时要使用的数据的表的名称。|  
|LobChunckSize|Integer|针对 LOB 列的块大小分配。|  
||||  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Source](odbc-source.md)   
 [ODBC 源编辑器（“连接管理器”页）](../odbc-source-editor-connection-manager-page.md)  
  
  
