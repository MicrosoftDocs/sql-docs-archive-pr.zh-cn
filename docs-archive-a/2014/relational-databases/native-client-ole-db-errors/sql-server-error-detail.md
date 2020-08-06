---
title: SQL Server 错误详细信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c03cf62dd274f9bcca213d33fb8969b26c9d980
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589537"
---
# <a name="sql-server-error-detail"></a>SQL Server 错误详细信息
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序定义特定于访问接口的错误接口[ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md)。 该接口返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误的更多详细信息，在命令执行或行集操作失败时这些信息很有用。  
  
 可以用两种方式访问 ISQLServerErrorInfo 接口****。  
  
 使用者可调用 IErrorRecords::GetCustomerErrorObject 以获得 ISQLServerErrorInfo 指针，如以下代码示例所示********。 （不需要获得 ISQLErrorInfo。）ISQLErrorInfo 和 ISQLServerErrorInfo 都是自定义的 OLE DB 错误对象，并以 ISQLServerErrorInfo 作为用于获得服务器错误信息（包括诸如过程名称和行号这样的详细信息）的接口****************。  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 获得 ISQLServerErrorInfo 指针的另一个方式是调用已经获得的 ISQLErrorInfo 指针的 QueryInterface 方法************。 注意，由于 ISQLServerErrorInfo 包含从 ISQLErrorInfo 获得的信息的超集，因此通过 GetCustomerErrorObject 直接转到 ISQLServerErrorInfo 是有意义的****************。  
  
 ISQLServerErrorInfo 接口公开了一个成员函数 [ISQLServerErrorInfo::GetErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md)****。 该函数返回 SSERRORINFO 结构的指针和字符串缓冲区的指针。 两个指针都引用使用者必须使用 IMalloc::Free 方法释放的内存****。  
  
 SSERRORINFO 结构成员由使用者解释如下。  
  
|成员|描述|  
|------------|-----------------|  
|pwszMessage**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息。 与在 IErrorInfo::GetDescription 中返回的字符串相同****。|  
|pwszServer**|会话的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|pwszProcedure**|如果适用，则为产生错误的过程的名称。 否则为空字符串。|  
|lNative**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机错误号。 与在 ISQLErrorInfo::GetSQLInfo 的 plNativeError 参数中返回的值相同******。|  
|bState**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的状态。|  
|bClass**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息的严重性。|  
|wLineNumber**|如果适用，则为发生错误的存储过程的行号。|  
  
## <a name="see-also"></a>另请参阅  
 [错误](errors.md)   
 [RAISERROR (Transact-SQL)](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
