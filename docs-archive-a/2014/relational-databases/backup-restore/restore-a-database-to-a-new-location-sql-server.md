---
title: 将数据库还原到新位置 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 89b42f439b5622074327506b9f2ca2b2358cd12f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589165"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>将数据库还原到新位置 (SQL Server)
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中将 [!INCLUDE[tsql](../../includes/tsql-md.md)]数据库还原到一个新位置并且可以选择重命名该数据库。 您可以在同一服务器实例或不同服务器实例上将数据库移到新的目录路径或者创建数据库的副本。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要将数据库还原到一个新位置并且可以选择重命名该数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   还原完整数据库备份的系统管理员必须是当前使用要还原的数据库的唯一人员。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   在完整恢复模式或大容量日志恢复模式下，必须先备份活动事务日志，然后才能还原数据库。 有关详细信息，请参阅 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)数据库还原到一个新位置并且可以选择重命名该数据库。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
  
-   若要还原已加密的数据库，您必须有权访问用于对数据库进行加密的证书或非对称密钥。 如果没有证书或非对称密钥，数据库将无法还原。 因此，只要需要该备份，就必须保留用于对数据库加密密钥进行加密的证书。 有关详细信息，请参阅 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)。  
  
-   有关移动数据库的其他注意事项的信息，请参阅[通过备份和还原来复制数据库](../databases/copy-databases-with-backup-and-restore.md)。  
  
-   如果您将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本的数据库还原为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，将自动升级该数据库。 通常，该数据库将立即可用。 但是，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库具有全文检索，则升级过程将导入、重置或重新生成它们，具体取决于  **upgrade_option** 服务器属性的设置。 如果将升级选项设置为“导入”(**upgrade_option** = 2) 或“重新生成”(**upgrade_option** = 0)，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，如果将升级选项设置为“导入”，并且全文目录不可用，则会重新生成关联的全文索引。 若要更改 **upgrade_option** 服务器属性的设置，请使用 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 出于安全性考虑，我们建议您不要从未知或不信任的源附加或还原数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 使用来自未知源或不可信源的数据库前，请在非生产服务器上针对数据库运行 [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) ，然后检查数据库中的代码，例如存储过程或其他用户定义代码。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 如果不存在要还原的数据库，则用户必须有 CREATE DATABASE 权限才能执行 RESTORE。 如果该数据库存在，则 RESTORE 权限默认授予 **sysadmin** 和 **dbcreator** 固定服务器角色成员以及该数据库的所有者 (**dbo**)。  
  
 RESTORE 权限被授予那些成员身份信息始终可由服务器使用的角色。 因为只有在固定数据库可以访问且没有损坏时（在执行 RESTORE 时并不会总是这样）才能检查固定数据库角色成员身份，所以 **db_owner** 固定数据库角色成员没有 RESTORE 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>将数据库还原到一个新位置并且可以选择重命名该数据库  
  
1.  连接到相应的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例，然后在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  右键单击“数据库”，然后单击“还原数据库”   。 **“还原数据库”** 对话框随即打开。  
  
3.  在 **“常规”** 页上，使用 **“源”** 部分指定要还原的备份集的源和位置。 选择以下选项之一：  
  
    -   **Database**  
  
         从下拉列表中选择要还原的数据库。 此列表仅包含已根据 **msdb** 备份历史记录进行备份的数据库。  
  
    > [!NOTE]  
    >  如果备份是从另一台服务器执行的，则目标服务器不具有指定数据库的备份历史记录信息。 这种情况下，请选择 **“设备”** 以手动指定要还原的文件或设备。  
  
    1.  **设备**  
  
         单击“浏览”按钮 ( **...** ) 以打开“选择备份设备”  对话框。 在 **“备份介质类型”** 框中，从列出的设备类型中选择一种。 若要为 **“备份介质”** 框选择一个或多个设备，请单击 **“添加”** 。  
  
         将所需设备添加到 **“备份介质”** 列表框后，单击 **“确定”** 返回到 **“常规”** 页。  
  
         在“源:设备:数据库”列表框中，选择应还原的数据库名称 **。**  
  
         **注意** ：此列表仅在选择了 **“设备”** 时才可用。 只有在所选设备上具有备份的数据库才可用。  
  
4.  在 **“目标”** 部分中， **“数据库”** 框自动填充要还原的数据库的名称。 若要更改数据库名称，请在 **“数据库”** 框中输入新名称。  
  
5.  在 **“还原到”** 框中，保留默认选项 **“至最近一次进行的备份”** ，或者单击 **“时间线”** 访问 **“备份时间线”** 对话框以手动选择要停止恢复操作的时间点。 请参阅 [Backup Timeline](backup-timeline.md) 以获取有关指定特定时间点的详细信息。  
  
6.  在 **“要还原的备份集”** 网格中，选择要还原的备份。 此网格将显示对于指定位置可用的备份。 默认情况下，系统会推荐一个恢复计划。 若要覆盖建议的恢复计划，可以更改网格中的选择。 当取消选择某个早期备份时，将自动取消选择那些需要还原该早期备份才能进行的备份。  
  
     有关“用于还原的备份集”  网格中的列的信息，请参阅[还原数据库（“常规”页）](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
7.  若要指定数据库文件的新位置，请选择 **“文件”** 页，然后单击 **“将所有文件重新定位到文件夹”** 。 为 **“数据文件的文件夹”** 和 **“日志文件的文件夹”** 提供一个新位置。 有关该网格的详细信息，请参阅[还原数据库（“文件”页）](restore-database-files-page.md)。  
  
8.  在 **“选项”** 页上，根据要求调整选项。 有关这些选项的详细信息，请参阅[还原数据库（“选项”页）](restore-database-options-page.md)。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>将数据库还原到一个新位置并且可以选择重命名该数据库  
  
1.  （可选）确定包含要还原的完整数据库备份的备份集中文件的逻辑名称和物理名称。 此语句返回备份集内包含的数据库和日志文件的列表。 基本语法如下：  
  
     RESTORE FILELISTONLY FROM *<backup_device>* WITH FILE = *backup_set_file_number*  
  
     其中，*backup_set_file_number* 指示备份在介质集中的位置。 您可以通过使用 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 语句来获取备份集的位置。 有关详细信息，请参阅 [RESTORE 参数 (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql) 中的“指定备份集”。  
  
     此语句还支持多个 WITH 选项。 有关详细信息，请参阅 [RESTORE FILELISTONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)。  
  
2.  使用 [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) 语句还原完整数据库备份。 默认情况下，数据文件和日志文件还原到它们的原位置。 若要重新定位数据库，请使用 MOVE 选项重新定位每个数据库文件并避免与现有文件发生冲突。  
  
     将数据库还原到新位置并使其具有新名称的基本 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法如下：  
  
     RESTORE DATABASE *new_database_name*  
  
     FROM *backup_device* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** |NORECOVERY  
  
     [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
     [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > [!NOTE]  
    >  准备将数据库重新定位到其他磁盘上时，应当验证是否有足够的可用空间并确定与现有文件之间的任何潜在冲突。 这涉及到使用 [RESTORE VERIFYONLY](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql) 语句，该语句指定您计划在 RESTORE DATABASE 语句中使用的相同 MOVE 参数。  
  
     下表介绍了此 RESTORE 语句在将数据库还原到新位置时所涉及的参数。 有关这些参数的详细信息，请参阅 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)数据库还原到一个新位置并且可以选择重命名该数据库。  
  
     *new_database_name*  
     数据库的新名称。  
  
    > [!NOTE]  
    >  如果要将数据库还原到其他服务器实例，则可以使用原始数据库名称而不是新名称。  
  
     *backup_device* [ `,` ...*n* ]  
     指定包含 1 到 64 个备份设备的逗号分隔的列表，数据库备份将从这些备份设备中还原。 您可以指定物理备份设备，也可以指定对应的逻辑备份设备（如果已定义）。 若要指定物理备份设备，请使用 DISK 或 TAPE 选项：  
  
     { DISK | TAPE } `=` *physical_backup_device_name*  
  
     有关详细信息，请参阅 [备份设备 (SQL Server)](backup-devices-sql-server.md)。  
  
     { **RECOVERY** | NORECOVERY }  
     如果数据库使用完整恢复模式，则可能需要在还原该数据库后应用事务日志备份。 在这种情况下，请指定 NORECOVERY 选项。  
  
     否则，请使用默认值 RECOVERY 选项。  
  
     FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
     标识要还原的备份集。 例如， *backup_set_file_number* 为 **1** 指示备份介质中的第一个备份集， *backup_set_file_number* 为 **2** 指示第二个备份集。 你可以通过使用 *RESTORE HEADERONLY* 语句来获取备份集的 [backup_set_file_number](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 。  
  
     未指定此选项时，默认为使用备份设备上的第一个备份集。  
  
     有关详细信息，请参阅 [RESTORE 参数 (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql) 中的“指定备份集”。  
  
     将 **" *`logical_file_name_in_backup`* "** 移动到 **" *`operating_system_file_name`* "** [ `,` .。。*n* ]  
     指定由 *logical_file_name_in_backup* 指定的数据或日志文件将还原到 *operating_system_file_name*指定的位置。 请为每个要从备份集还原到新位置的逻辑文件指定 MOVE 语句。  
  
    |选项|说明|  
    |------------|-----------------|  
    |*logical_file_name_in_backup*|指定备份集中数据文件或日志文件的逻辑名称。 创建备份集时，备份集中的数据或日志文件的逻辑文件名与其在数据库中的逻辑名称匹配。<br /><br /> 注意：若要从备份集中获取逻辑文件列表，请使用 [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)。|  
    |*operating_system_file_name*|指定由 *logical_file_name_in_backup*指定的文件的新位置。 文件将还原到此位置。<br /><br /> 或者， *operating_system_file_name* 指定已还原文件的新文件名。 如果您在相同服务器实例上创建现有数据库的副本，则此操作是必需的。|  
    |*n*|是指示可以指定其他 MOVE 语句的占位符。|  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例通过还原 `MyAdvWorks` 示例数据库的备份创建名为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 的一个新数据库，该数据库包括两个文件： [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data 和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log。 此数据库使用简单恢复模式。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库已经存在于服务器实例上，因此备份中的文件必须还原到一个新位置。 RESTORE FILELISTONLY 语句用于确定数据库中要还原的文件数和名称。 该数据库备份是备份设备上的第一个备份集。  
  
> [!NOTE]  
>  备份和还原事务日志的示例（包括时点还原）使用从 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 创建的 `MyAdvWorks_FullRM` 数据库的方式与下面的 `MyAdvWorks` 示例相同。 但是，必须通过使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句对最终生成的 `MyAdvWorks_FullRM` 数据库进行更改，以便使用完整恢复模式：ALTER DATABASE <database_name> SET RECOVERY FULL。  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 有关如何创建 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的完整数据库备份的示例，请参阅 [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)数据库还原到一个新位置并且可以选择重命名该数据库。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [还原数据库备份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
-   [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](../databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [通过备份和还原来复制数据库](../databases/copy-databases-with-backup-and-restore.md)  
  
  
