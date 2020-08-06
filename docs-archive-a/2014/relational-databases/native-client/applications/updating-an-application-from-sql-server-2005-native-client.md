---
title: 从 SQL Server 2005 Native Client 更新应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, updating applications
ms.assetid: 1e1e570c-7f14-4e16-beab-c328e3fbdaa8
author: rothja
ms.author: jroth
ms.openlocfilehash: 6db02837b854d237607eba7583d204a4860906b9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692358"
---
# <a name="updating-an-application-from-sql-server-2005-native-client"></a>从 SQL Server 2005 Native Client 更新应用程序
  本主题介绍自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 以来在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client 中的重大更改。  
  
 从 Microsoft 数据访问组件 (MDAC) 升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 时，也会看到一些行为差异。 有关详细信息，请参阅[将应用程序更新为从 MDAC SQL Server Native Client](updating-an-application-to-sql-server-native-client-from-mdac.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 随 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 随 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 附带。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.5 随 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 附带。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 随 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 附带。  
  
|自 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以来 SQL Server Native Client 中已更改的行为|说明|  
|------------------------------------------------------------------------------------|-----------------|  
|OLE DB 仅填充到定义的小数位数。|对于要将转换的数据发送到服务器的转换操作，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client（从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始）在填充数据中的尾随零时，最多仅填充到 `datetime` 值的最大长度。 SQL Server Native Client 9.0 则填充到 9 位数。|  
|验证 ICommandWithParameter::SetParameterInfo 的 DBTYPE_DBTIMESTAMP。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 (从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 中开始实现对 ICommandWithParameter：： SetParameterInfo 中的*bScale*的 OLE DB 要求，将设置为 DBTYPE_DBTIMESTAMP 的秒小数部分。|  
|`sp_columns`对于 IS_NULLABLE 列，该存储过程将返回 **"no"** 而不是 **"no** "。|从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) ， `sp_columns` 存储过程现在为 IS_NULLABLE 列返回 **"no"** ，而不是 **"no"** 。|  
|SQLSetDescRec、SQLBindParameter 和 SQLBindCol 现在会执行一致性检查。|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]在 Native Client 10.0 之前，设置 SQL_DESC_DATA_PTR 不会对 SQLSetDescRec、SQLBindParameter 或 SQLBindCol 中的任何描述符类型进行一致性检查。|  
|SQLCopyDesc 现在执行描述符一致性检查。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，当对特定记录设置 SQL_DESC_DATA_PTR 字段时，SQLCopyDesc 不执行一致性检查。|  
|SQLGetDescRec 不再执行描述符一致性检查。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，在设置 SQL_DESC_DATA_PTR 字段时，SQLGetDescRec 执行了描述符一致性检查。 这不是 ODBC 规范和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]) 以及更高版本所要求的，该一致性检查不再执行。|  
|日期超出范围时返回其他错误。|对于 `datetime` 类型，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client（从 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 开始）将对超出范围的日期返回与更早版本返回错误号不同的错误号。<br /><br /> 具体来说，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 对字符串转换到 `datetime` 时所有超出范围的年份值均返回 22007；而从版本 10.0 ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 开始的 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 则在日期处于 `datetime2` 支持的范围但不处于 `datetime` 或 `smalldatetime` 支持的范围时返回 22008。|  
|如果舍入将更改日期，则 `datetime` 值将截断秒的小数部分，并且不舍入。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，对于发送到服务器的 `datetime` 值的客户端行为是将它们舍入到最接近 1/300 秒的值。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，如果舍入会更改日期，则该方案会导致截断秒的小数部分。|  
|值的可能的且 `datetime` 。|如果您绑定到某一 datetime 列并且其类型标识符为 DBTYPE_DBTIMESTAMP (OLE DB) 或 SQL_TIMESTAMP (ODBC)、小数位数为 0，则使用连接到 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 2005 服务器的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client（或更高版本）生成的应用程序将截断要发送到服务器的时间部分中的秒和秒的小数部分。<br /><br /> 例如：<br /><br /> 输入数据：1994-08-21 21:21:36.000<br /><br /> 插入的数据：1994-08-21 21:21:00.000|  
|从 DBTYPE_DBTIME 到 DBTYPE_DATE 的 OLE DB 数据转换不会再导致日期发生更改。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 之前，如果 DBTYPE_DATE 的时间部分是在距离午夜的半秒内，则 OLE DB 转换代码将导致日期发生更改。 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，日期不会更改（秒的小数部分将截断但不舍入）。|  
|IBCPSession::BCColFmt 转换更改。|从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 开始，当你使用 IBCPSession：： BCOColFmt 将 SQLDATETIME 或 SQLDATETIME 转换为字符串类型时，将导出小数值。 例如，将类型 SQLDATETIME 转换为类型 SQLNVARCHARMAX 时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的更早版本返回<br /><br /> 1989-02-01 00:00:00。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0 及更高版本返回 1989-02-01 00:00:00.0000000。|  
|发送的数据的大小必须与 SQL_LEN_DATA_AT_EXEC 中指定的长度匹配。|使用 SQL_LEN_DATA_AT_EXEC 时，数据的大小必须与用 SQL_LEN_DATA_AT_EXEC 指定的长度匹配。 可以使用 SQL_DATA_AT_EXEC，但使用 SQL_LEN_DATA_AT_EXEC 有潜在的性能好处。|  
|使用 BCP API 的自定义应用程序现在可以看到警告。|对于所有类型，如果数据长度超过某字段的指定长度，则 BCP API 将生成警告消息。 以前，该警告仅针对字符类型，而不会针对所有类型发出。|  
|将空字符串插入到绑定为日期/时间类型的 `sql_variant` 中会生成错误。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 9.0 中，将空字符串插入到绑定为日期/时间类型的 `sql_variant` 中不会生成错误。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 10.0（和更高版本）在这种情况下则会正确地生成错误。|  
|更严格的 SQL_C_TYPE _TIMESTAMP 和 DBTYPE_DBTIMESTAMP 参数验证。|在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client 之前，将 `datetime` 对值进行舍入，以适合和列的小数位数 `datetime` `smalldatetime` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client（和更高版本）现在应用在 ODBC 核心规范中为秒的小数部分定义的更严格的验证规则。 如果无法通过使用由客户端绑定所指定或暗含的小数位数在不截断尾随数字的情况下将参数值转换到 SQL 类型，则返回错误。|  
|当有触发器运行时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可能会返回不同的结果。|[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入的变化可能会导致应用程序得到从 `NOCOUNT OFF` 有效时导致触发器运行的语句返回的不同的结果。 在这种情况下，您的应用程序可能会生成错误。 若要解决此错误，请 `NOCOUNT ON` 在触发器中设置，或调用 SQLMoreResults 来前进到下一个结果。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../sql-server-native-client-programming.md)  
  
  
