---
title: 移动数据库文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5491f3c4dfd47cac4047d0409c78001be80d6f13
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691735"
---
# <a name="move-database-files"></a>移动数据库文件
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以通过在 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 语句的 FILENAME 子句中指定新的文件位置来移动系统数据库和用户数据库。 数据、日志和全文目录文件也可以通过此方法进行移动。 这在下列情况下可能很有用：  
  
-   故障恢复。 例如，由于硬件故障，数据库处于可疑模式或被关闭。  
  
-   预先安排的重定位。  
  
-   为预定的磁盘维护操作而进行的重定位。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[移动用户数据库](move-user-databases.md)|说明将用户数据库文件和全文目录文件移动到新位置的过程。|  
|[移动系统数据库](system-databases.md)|说明将系统数据库文件移动到新位置的过程。|  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [数据库分离和附加 (SQL Server)](database-detach-and-attach-sql-server.md)  
  
  
