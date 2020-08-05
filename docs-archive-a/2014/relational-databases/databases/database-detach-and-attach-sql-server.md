---
title: 数据库分离和附加 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
author: stevestein
ms.author: sstein
ms.openlocfilehash: 54eeeec995e390b71ce8871b680c26138fc88783
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581310"
---
# <a name="database-detach-and-attach-sql-server"></a>数据库分离和附加 (SQL Server)
  可以分离数据库的数据和事务日志文件，然后将它们重新附加到同一或其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 如果要将数据库更改到同一计算机的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例或要移动数据库，分离和附加数据库会很有用。  
  
 在 64 位和 32 位环境中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘存储格式均相同。 因此，可以将 32 位环境中的数据库附加到 64 位环境中，反之亦然。  从运行在某个环境中的服务器实例上分离的数据库可以附加到运行在另一个环境中的服务器实例。  
  
  
  
##  <a name="security"></a><a name="Security"></a> Security  
 文件访问权限可在很多数据库操作过程中设置，其中包括分离或附加数据库。  
  
> [!IMPORTANT]  
>  建议您不要附加或还原来自未知或不可信源的数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。  
  
##  <a name="detaching-a-database"></a><a name="DetachDb"></a> 分离数据库  
 分离数据库是指将数据库从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中删除，但使数据库在其数据文件和事务日志文件中保持不变。 之后，就可以使用这些文件将数据库附加到任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，包括分离该数据库的服务器。  
  
 如果存在下列任何情况，则不能分离数据库：  
  
-   已复制并发布数据库。 如果进行复制，则数据库必须是未发布的。 必须通过运行 [sp_replicationdboption](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)禁用发布后，才能分离数据库。  
  
    > [!NOTE]  
    >  如果无法使用 **sp_replicationdboption**，可以通过运行 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql)删除复制。  
  
-   数据库中存在数据库快照。  
  
     必须首先删除所有数据库快照，然后才能分离数据库。 有关详细信息，请参阅 [删除数据库快照 (Transact-SQL)](drop-a-database-snapshot-transact-sql.md)实例。  
  
    > [!NOTE]  
    >  不能分离或附加数据库快照。  
  
-   该数据库正在某个数据库镜像会话中进行镜像。  
  
     除非终止该会话，否则无法分离该数据库。 有关详细信息，请参阅 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
-   数据库处于可疑状态。 无法分离可疑数据库；必须将数据库设为紧急模式，才能对其进行分离。 有关如何将数据库置于紧急模式下的详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
-   数据库为系统数据库。  
  
### <a name="backup-and-restore-and-detach"></a>备份、还原及分离  
 分离只读数据库将会丢失有关差异备份的差异基准的信息。 有关详细信息，请参阅 [差异备份 (SQL Server)](../backup-restore/differential-backups-sql-server.md)。  
  
### <a name="responding-to-detach-errors"></a>响应分离错误  
 分离数据库时生成的错误会阻止完全关闭数据库和重新生成事务日志。 收到错误消息后，请执行下列更正操作：  
  
1.  重新附加与数据库关联的所有文件，而不仅仅是主文件。  
  
2.  解决导致生成错误消息的问题。  
  
3.  再次分离数据库。  
  
##  <a name="attaching-a-database"></a><a name="AttachDb"></a> 附加数据库  
 您可以附加复制的或分离的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 附加 [!INCLUDE[ssVersion2005](../../includes/sscurrent-md.md)] 服务器实例时，会将目录文件从其以前的位置与其他数据库文件一起附加，这与中相同 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 有关详细信息，请参阅 [全文搜索升级](../search/upgrade-full-text-search.md)。  
  
 附加数据库时，所有数据文件（MDF 文件和 NDF 文件）都必须可用。 如果任何数据文件的路径不同于首次创建数据库或上次附加数据库时的路径，则必须指定文件的当前路径。  
  
> [!NOTE]  
>  如果附加的主数据文件是只读的，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 假定数据库也是只读的。  
  
 当加密的数据库首次附加到实例时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，数据库所有者必须通过执行下面的语句打开数据库的主密钥：通过密码 = **' *`password`* '** 打开主密钥解密。 建议您通过执行下面的语句对主密钥启用自动解密：ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY。 有关详细信息，请参阅 [CREATE MASTER KEY (Transact-SQL)](/sql/t-sql/statements/create-master-key-transact-sql) 和 [ALTER MASTER KEY (Transact-SQL)](/sql/t-sql/statements/alter-master-key-transact-sql)。  
  
 附加日志文件的要求在某些方面取决于数据库是读写的还是只读的，如下所示：  
  
-   对于读写数据库，通常可以附加新位置中的日志文件。 不过，在某些情况下，重新附加数据库需要使用其现有的日志文件。 因此，请务必保留所有分离的日志文件，直到在不需要这些日志文件的情况下成功附加了数据库。  
  
     如果读写数据库具有单个日志文件，并且您没有为该日志文件指定新位置，附加操作将在旧位置中查找该文件。 如果找到了旧日志文件，则无论数据库上次是否完全关闭，都将使用该文件。 但是，如果未找到旧文件日志，数据库上次是完全关闭且现在没有活动日志链，则附加操作将尝试为数据库创建新的日志文件。  
  
-   如果附加的主数据文件是只读的，则 [!INCLUDE[ssDE](../../includes/ssnoversion-md.md)] 无法更新主文件中存储的日志位置。  
  
  
  
###  <a name="metadata-changes-on-attaching-a-database"></a><a name="Metadata"></a> 附加数据库时的元数据更改  
 分离再重新附加只读数据库后，会丢失有关当前差异基准的备份信息。 “差异基准”  是数据库或其文件或文件组子集中所有数据的最新完整备份。 如果没有基准备份信息， **master** 数据库会变得与只读数据库不同步，这样之后进行的差异备份可能会产生意外结果。 因此，如果对只读数据库使用差异备份，在重新附加数据库后，应通过进行完整备份来建立新的差异基准。 有关差异备份的信息，请参阅[差异备份 (SQL Server)](../backup-restore/differential-backups-sql-server.md)。  
  
 附加时，数据库会启动。 通常，附加数据库时会将数据库重置为它分离或复制时的状态。 但是，附加和分离操作都会禁用数据库的跨数据库所有权链接。 有关如何启用链接的详细信息，请参阅 [cross db ownership chaining 服务器配置选项](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。 此外，附加数据库时，TRUSTWORTHY 均设置为 OFF。 有关如何将 TRUSTWORTHY 设置为 ON 的详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
### <a name="backup-and-restore-and-attach"></a>备份、还原及附加  
 与任何完全或部分脱机的数据库一样，不能附加正在还原文件的数据库。 如果停止了还原顺序，则可以附加数据库。 然后，可以重新启动还原顺序。  
  
###  <a name="attaching-a-database-to-another-server-instance"></a><a name="OtherServerInstance"></a> 将数据库附加到其他服务器实例  
  
> [!IMPORTANT]  
>  无法在早期版本的 SQL Server 中附加由较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建的数据库。  
  
 将数据库附加到其他服务器实例时，为了给用户和应用程序提供一致的体验，您最好在其他服务器实例上为数据库重新创建部分或全部元数据（例如登录名和作业）。 有关详细信息，请参阅 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
 **分离数据库**  
  
-   [sp_detach_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
-   [分离数据库](detach-a-database.md)  
  
 **附加数据库**  
  
-   [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
-   [附加数据库](attach-a-database.md)  
  
-   [sp_attach_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql)  
  
-   [sp_attach_single_file_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql)  
  
 **使用分离和附加操作升级数据库**  
  
-   [使用分离和附加来升级数据库 (Transact-SQL)](upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **使用分离和附加操作移动数据库**  
  
-   [使用分离和附加来移动数据库 (Transact-SQL)](move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **删除数据库快照**  
  
-   [删除数据库快照 (Transact-SQL)](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据库文件和文件组](database-files-and-filegroups.md)  
  
  
