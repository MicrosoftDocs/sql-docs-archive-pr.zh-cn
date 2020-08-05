---
title: 更改数据库镜像会话中的事务安全 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d8bc9d0fb639770d33507c29a6ec67f60bd0434a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579776"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>更改数据库镜像会话中的事务安全 (Transact-SQL)
  事务安全是控制会话运行模式的属性。 但是，数据库所有者可以随时更改事务安全。 默认情况下，事务安全级别的设置为 FULL（同步运行模式）。  
  
 关闭事务安全可将会话切换到异步运行模式，该模式可使性能达到最佳。 主体不可用时镜像将停止，但它可以作为备用使用（故障转移需要使用可能会丢失数据的强制服务）。  
  
### <a name="to-turn-on-transaction-safety"></a>打开事务安全  
  
1.  连接到主体服务器。  
  
2.  发出以下 Transact-SQL 语句：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     其中，\<database> 为镜像数据库的名称。  
  
### <a name="to-turn-off-transaction-safety"></a>关闭事务安全  
  
1.  连接到主体服务器。  
  
2.  发出以下语句：  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     其中，\<database> 是镜像数据库。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE 数据库镜像 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [数据库镜像运行模式](database-mirroring-operating-modes.md)  
  
  
