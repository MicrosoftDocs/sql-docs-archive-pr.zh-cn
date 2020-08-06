---
title: 使用 OpenSqlFilestream 访问 FILESTREAM 数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
api_name:
- OpenSqlFilestream
api_location:
- sqlncli11.dll
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1a1416c0104e07c7bd228a723192ecb35bbe9216
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690657"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>使用 OpenSqlFilestream 访问 FILESTREAM 数据
  OpenSqlFilestream API 为文件系统中存储的 FILESTREAM 二进制大型对象 (BLOB) 获取 Win32 兼容的文件句柄。 句柄可以传递给以下任何 Win32 API：[ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、[WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、[TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、[SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、[SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426) 或 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 如果将此句柄传递给其他任何 Win32 API，将返回错误 ERROR_ACCESS_DENIED。 必须首先将此句柄传递给 Win32 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428) API 来关闭它，才能提交或回退事务。 未能关闭句柄将导致服务器端资源泄漏。  
  
 所有 FILESTREAM 数据容器访问都必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务中执行。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句也可以在同一事务中执行。 这样可保持 SQL 数据与 FILESTREAM BLOB 数据之间的一致性。  
  
 若要使用 Win32 访问 FILESTREAM BLOB，必须启用 [Windows 授权](../security/choose-an-authentication-mode.md) 。  
  
> [!IMPORTANT]  
>  打开文件以进行写入访问时，事务由 FILESTREAM 代理所有。 在释放事务之前，仅允许执行 Win32 文件 I/O。 若要释放事务，必须关闭写句柄。  
  
## <a name="syntax"></a>语法  
  
```  
  
  HANDLE OpenSqlFilestream (  
  LPCWSTR  
  FilestreamPath  
  ,  
  SQL_FILESTREAM_DESIRED_ACCESS  
  DesiredAccess,  
ULONGOpenOptions,LPBYTEFilestreamTransactionContext,SIZE_TFilestreamTransactionContextLength,PLARGE_INTEGERAllocationSize);  
```  
  
#### <a name="parameters"></a>参数  
 *FilestreamPath*  
 中`nvarchar(max)` [PathName](/sql/relational-databases/system-functions/pathname-transact-sql)函数返回的路径。 必须从具有 FILESTREAM 表和列的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT 或 UPDATE 权限的帐户的上下文中调用 PathName。  
  
 *DesiredAccess*  
 [in] 设置用于访问 FILESTREAM BLOB 数据的模式。 该值传递到 [DeviceIoControl 函数](https://go.microsoft.com/fwlink/?LinkId=105527)。  
  
|名称|值|含义|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|可从文件中读取数据。|  
|SQL_FILESTREAM_WRITE|1|可将数据写入文件。|  
|SQL_FILESTREAM_READWRITE|2|可从文件读取数据并将数据写入文件。|  
  
> [!NOTE]  
>  这些值在 sqlncli.h 的 SQL_FILESTREAM_DESIRED_ACCESS 枚举中定义。  
  
 *OpenOptions*  
 [in] 文件属性和标志。 此参数还可以包括下列标志的任意组合。  
  
|标志|值|含义|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|文件是未使用任何特殊选项打开或创建的。|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|文件是针对异步 I/O 打开或创建的。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|系统不使用系统缓存来打开文件。|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|系统不通过任何中间缓存来进行写入。 直接将数据写入磁盘。|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|从开头到末尾顺序访问文件。 系统可将此选项用作优化文件缓存的提示。 如果应用程序移动文件指针来进行随机访问，可能不会发生优化缓存。|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|随机访问文件。 系统可将此选项用作优化文件缓存的提示。|  
  
 *FilestreamTransactionContext*  
 [in] [GET_FILESTREAM_TRANSACTION_CONTEXT](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 函数返回的值。  
  
 *FilestreamTransactionContextLength*  
 [in] GET_FILESTREAM_TRANSACTION_CONTEXT 函数返回的 `varbinary(max)` 数据中的字节数。 函数返回 N 个字节数组。 N 由函数决定，是返回的字节数组的一个属性。  
  
 *AllocationSize*  
 [in] 以字节为单位指定数据文件的初始分配大小。 在读取模式下将被忽略。 此参数可以为 NULL，在这种情况下，将使用默认文件系统行为。  
  
## <a name="return-value"></a>返回值  
 如果函数成功，则返回值为指定文件的打开句柄。 如果函数失败，则返回值为 INVALID_HANDLE_VALUE。 要获得更多的错误信息，请调用 GetLastError()。  
  
## <a name="examples"></a>示例  
 下面的示例说明如何使用 `OpenSqlFilestream` API 获取 Win32 句柄。  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
## <a name="remarks"></a>备注  
 必须安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 才能使用此 API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 随同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端工具一起安装。 有关详细信息，请参阅 [安装 SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md)。  
  
## <a name="see-also"></a>另请参阅  
 [二进制大型对象 &#40;Blob&#41; 数据 &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [对 FILESTREAM 数据进行部分更新](make-partial-updates-to-filestream-data.md)   
 [避免与 FILESTREAM 应用程序中的数据库操作冲突](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
