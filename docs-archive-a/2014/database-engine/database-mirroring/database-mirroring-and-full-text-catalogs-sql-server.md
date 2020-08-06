---
title: 数据库镜像和全文目录 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 39929f4bed6edbd1e8ec5c1b72dbe8f7aefeec68
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579765"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>数据库镜像和全文目录 (SQL Server)
  若要对带有全文目录的数据库进行镜像，请使用常规备份创建主体数据库的完整数据库备份，然后还原备份，以便将数据库复制到镜像服务器。 有关详细信息，请参阅 [为镜像准备镜像数据库 (SQL Server)](prepare-a-mirror-database-for-mirroring-sql-server.md)的各版本中均未提供见证服务器实例。  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>故障转移前的全文目录和索引  
 新建镜像数据库中的全文目录与数据库备份时的全文目录相同。 数据库镜像开始后，对 DDL 语句（CREATE FULLTEXT CATALOG、ALTER FULLTEXT CATALOG、DROP FULLTEXT CATALOG）所做的任意目录级更改都会被记录下来，发送到镜像服务器，在镜像数据库中进行重播。 但是，镜像数据库中不会重新生成索引级更改，因为镜像数据库没有登录到主体服务器上。 因此，当主体数据库中的全文目录内容发生变化时，镜像数据库中的全文目录内容便不再同步。  
  
## <a name="full-text-indexes-after-failover"></a>故障转移后的全文索引  
 故障转移后，在下列情况下，可能需要对新主体服务器上的全文索引进行完全爬网，即便不是必需，也会有所帮助：  
  
-   如果全文索引的更改跟踪功能处于关闭状态，则必须使用下面的语句对该索引启动完全爬网：  
  
     ALTER FULLTEXT INDEX ON *table_name* START FULL POPULATION  
  
-   如果全文索引被配置为自动跟踪更改，则将自动同步全文索引。 但是，同步过程多少会降低全文索引的性能。 如果性能太低，则可以通过关闭更改跟踪然后将其重置为自动的方式来启动完全爬网：  
  
    -   关闭更改跟踪：  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING OFF  
  
    -   开启自动更改跟踪：  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  若要查看是否已开启自动更改跟踪，可以使用 [OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql) 函数查询表的 **TableFullTextBackgroundUpdateIndexOn** 属性。  
  
 有关详细信息，请参阅 [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
> [!NOTE]  
>  在故障转移后启动爬网与在还原后启动爬网相似。  
  
## <a name="after-forcing-service"></a>强制服务后  
 对镜像服务器强制运行服务后（可能造成数据丢失），启动完全爬网。 启动完全爬网的方法取决于是否对全文索引启动了更改跟踪。 有关详细信息，请参阅本主题前面的“故障转移后的全文索引”。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [DROP FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-index-transact-sql)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)   
 [备份和还原全文目录和索引](../../relational-databases/indexes/indexes.md)  
  
  
