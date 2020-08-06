---
title: 对 FILESTREAM 数据进行部分更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 696c1a6421e14568877e24f015e5094395f1051b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692957"
---
# <a name="make-partial-updates-to-filestream-data"></a>对 FILESTREAM 数据进行部分更新
  应用程序使用 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 对 FILESTREAM BLOB 数据进行部分更新。 [DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527) 函数将此值和从 [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) 返回的句柄传递到 FILESTREAM 驱动程序。 然后，该驱动程序将当前的 FILESTREAM 数据从服务器端强制复制到该句柄所引用的文件。 如果应用程序在已写入句柄后发出 FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT 值，则保留最后一个写入操作，但之前对该句柄执行的写入操作将丢失。  
  
> [!NOTE]  
>  FILESTREAM 依赖于 [SMB 协议](https://go.microsoft.com/fwlink/?LinkId=112454) 进行远程访问。  
  
## <a name="example"></a>示例  
 下面的示例显示如何使用 `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` 值对插入的 FILESTREAM BLOB 执行部分更新。  
  
> [!NOTE]  
>  本示例需要在 [创建启用 FILESTREAM 的数据库](create-a-filestream-enabled-database.md) 和 [创建表以存储 FILESTREAM 数据](create-a-table-for-storing-filestream-data.md)中创建的启用了 FILESTREAM 的数据库和表。  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>另请参阅  
 [使用 OpenSqlFilestream 访问 FILESTREAM 数据](access-filestream-data-with-opensqlfilestream.md)   
 [为 FILESTREAM 数据创建客户端应用程序](create-client-applications-for-filestream-data.md)  
  
  
