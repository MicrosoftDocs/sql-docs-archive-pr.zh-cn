---
title: SQL Server 属性（“文件流”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.filestream.f1
helpviewer_keywords:
- FILESTREAM [SQL Server], properties page
ms.assetid: 8a8d38d3-e97a-4b09-a40b-659b2e3a5c47
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ca13877a195a0f829c3fd0a628c446626819e14a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692512"
---
# <a name="sql-server-properties-filestream-page"></a>SQL Server 属性（FILESTREAM 页）
  使用此页可针对此 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装启用 FILESTREAM。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 **针对 Transact-SQL 访问启用 FILESTREAM**  
 选中此项可针对 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问启用 FILESTREAM。 必须选中此控制选项，才能使用其他控制选项。  
  
 **针对文件 I/O 流访问启用 FILESTREAM**  
 选中此项可针对 FILESTREAM 启用 Win32 流访问。  
  
 **Windows 共享名**  
 使用此控制选项可输入将用来存储 FILESTREAM 数据的 Windows 共享的名称。  
  
 **允许远程客户端针对 FILESTREAM 数据启用流访问**  
 选中此控制选项可允许远程客户端访问此服务器上的此 FILESTREAM 数据。  
  
## <a name="see-also"></a>另请参阅  
 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
