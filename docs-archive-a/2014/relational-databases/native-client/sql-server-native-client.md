---
title: SQL Server Native Client&#39;的新增功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: rothja
ms.author: jroth
ms.openlocfilehash: f7a8fdd6716f7ba571ed8d1d8b5f959666961aa8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591318"
---
# <a name="what39s-new-in-sql-server-native-client"></a>&#39;中的新增功能 SQL Server Native Client
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 会安装 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client。 没有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client。  
  
 未来 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 驱动程序将不会再更新。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中 ODBC 驱动程序的后继版本（在 Windows 上称为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）将随 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 一同安装。 有关 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 上的 ODBC driver 11 for 的详细信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请参阅[Microsoft odbc driver 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36434)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 最近更新了 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 中的 OLE DB Provider。 想要使用 OLE DB 访问接口连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最新版本的开发人员必须使用在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 中随附的 OLE DB 访问接口。  
  
 下列主题说明 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中新增的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 重要功能。  
  
-   [SQL Server Native Client 对 LocalDB 的支持](features/sql-server-native-client-support-for-localdb.md)  
  
-   [元数据发现](features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 中的 UTF-16 支持](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [访问扩展事件日志中的诊断信息](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 现在支持添加到 Windows 7 SDK 中的标准 ODBC 的三项功能：  
  
-   异步执行与连接相关的操作。 有关详细信息，请参阅[异步执行](https://go.microsoft.com/fwlink/?LinkID=191493)。  
  
-   C 数据类型扩展能力。 有关详细信息，请参阅[ODBC 中的 C 数据类型](https://go.microsoft.com/fwlink/?LinkID=191495)。  
  
     若要在 Native Client 中支持此功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， `SQL_C_SS_TIME2` `time` `SQL_C_SS_TIMESTAMPOFFSET` `datetimeoffset` `SQL_C_BINARY` 如果应用程序使用 ODBC 3.8，则 SQLGetDescField 可以返回类型) 为) 或 (的 (，而不是。 有关详细信息，请参阅[对 ODBC 日期和时间改进的数据类型支持](features/date-and-time-improvements.md)。  
  
-   用小缓冲区多次调用 `SQLGetData` 来检索一个大型参数值。 有关详细信息，请参阅[使用 SQLGetData 检索输出参数](https://go.microsoft.com/fwlink/?LinkID=191494)。  
  
 下列主题描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 行为更改。  
  
-   调用时 `ICommandWithParameters::SetParameterInfo` ，传递给*pwszName*参数的值必须是有效的标识符。 有关详细信息，请参阅[ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md)。  
  
-   `SQLDescribeParam` 现在将一致地返回符合 ODBC 规范的值。 有关详细信息，请参阅[SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md)。  
  
-   [处理字符转换时 ODBC 驱动程序行为的变化](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](features/sql-server-native-client-features.md)  
  
  
