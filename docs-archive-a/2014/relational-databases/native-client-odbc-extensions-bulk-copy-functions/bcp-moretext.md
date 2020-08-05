---
title: bcp_moretext |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_moretext
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: rothja
ms.author: jroth
ms.openlocfilehash: 00c0eb1c8739e94380b12034cebc70d8e22b79c6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580251"
---
# <a name="bcp_moretext"></a>bcp_moretext
  将部分较长的可变长度数据类型值发送到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE bcp_moretext (  
HDBC   
hdbc  
,  
DBINT   
cbData  
,  
LPCBYTE   
pData  
);  
  
```  
  
## <a name="arguments"></a>参数  
 *hdbc*  
 是启用大容量复制的 ODBC 连接句柄。  
  
 *cbData*  
 要从*pData*引用的数据复制到 SQL Server 的数据字节数。 SQL_NULL_DATA 的值指示为 NULL。  
  
 *pData*  
 指向要发送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的受支持的较长可变长度数据块区的指针。  
  
## <a name="returns"></a>返回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>备注  
 此函数可与[bcp_bind](bcp-bind.md)和[bcp_sendrow](bcp-sendrow.md)结合使用，以便将长度可变的长数据值复制到多个较小的块区中 SQL Server。 **bcp_moretext**可用于具有以下 SQL Server 数据类型的列： `text` 、 `ntext` 、、、、 `image` `varchar(max)` `nvarchar(max)` `varbinary(max)` 、用户定义类型 (UDT) 和 XML。 **bcp_moretext**不支持数据转换，则提供的数据必须与目标列的数据类型匹配。  
  
 如果使用**bcp_moretext**支持的数据类型的非 null *pData*参数调用**bcp_bind** ，则 `bcp_sendrow` 将发送整个数据值，而不考虑长度。 但是，如果**bcp_bind**具有用于支持的数据类型的 NULL *pData*参数，则在成功返回后，可使用**bcp_moretext**立即复制数据， `bcp_sendrow` 指示已处理包含数据的所有绑定列。  
  
 如果使用**bcp_moretext**在一行中发送一种受支持的数据类型列，则还必须使用它来发送该行中所有其他支持的数据类型列。 不可以跳过任何列。 支持的数据类型为 SQLTEXT、SQLNTEXT、SQLIMAGE、SQLUDT 和 SQLXML。 如果列分别为 varchar(max)、nvarchar(max) 或 varbinary(max)，则 SQLCHARACTER、SQLVARCHAR、SQNCHAR、SQLBINARY 和 SQLVARBINARY 也属于此类别。  
  
 调用**bcp_bind**或[bcp_collen](bcp-collen.md)会设置要复制到 SQL Server 列的所有数据部分的总长度。 尝试发送的字节数 SQL Server 超过调用**bcp_bind**中指定的字节数，或 `bcp_collen` 生成错误。 例如，在以下应用程序中会出现此错误：一个应用程序，该应用程序 `bcp_collen` 将 SQL Server 列的可用数据的长度设置 `text` 为4500，然后调用**bcp_moretext**五次，同时指示每个调用的数据缓冲区长度为1000字节长。  
  
 如果复制的行包含多个长、可变长度的列， **bcp_moretext**首先会将其数据发送到最低的按序号编号列，后跟下一个最低的按序号编号列，依此类推。 正确设置所需的数据的总长度很重要。 无法在长度设置之外发出已通过大容量复制接收某列的所有数据的信号。  
  
 当 `var(max)` 使用 bcp_sendrow 和 bcp_moretext 将值发送到服务器时，无需调用 bcp_collen 来设置列长度。 相反，对于这些类型，将通过调用长度为零的 bcp_sendrow 终止值。  
  
 应用程序通常会 `bcp_sendrow` 在循环中调用并**bcp_moretext** ，以发送多行数据。 下面概述了如何为包含两列的表执行此 `text` 操作：  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>示例  
 此示例演示如何将**bcp_moretext**与**bcp_bind**和结合使用 `bcp_sendrow` ：  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>另请参阅  
 [大容量复制函数](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
