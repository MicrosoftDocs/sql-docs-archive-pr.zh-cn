---
title: SQL Server 托管备份到 Azure-保持和存储设置 |Microsoft Docs
description: 本主题介绍如何为数据库配置 SQL Server 托管备份以 Microsoft Azure，以及如何配置实例的默认设置。
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: c4aa26ea-5465-40cc-8b83-f50603cb9db1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8ebdb81f8aa9edb9cd9326bcb1d286d5d3fe632c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691860"
---
# <a name="sql-server-managed-backup-to-azure---retention-and-storage-settings"></a>针对 Azure 的 SQL Server 托管备份 - 保留和存储设置
  本主题介绍为数据库配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 以及为实例配置默认设置的基本步骤。 本主题还介绍为实例暂停和恢复 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服务所需的步骤。  
  
 有关设置的完整演练 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，请参阅[设置 SQL Server 托管备份到 azure](../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md) ，并[将 SQL Server 托管备份设置为可用性组的 azure](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)。  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   不要对当前正使用维护计划或日志传送的数据库启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 有关互操作性和与其他 SQL Server 功能共存的详细信息，请参阅[SQL Server 托管备份到 Azure：互操作性和共存](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   SQL Server 代理应运行。  
  
    > [!WARNING]  
    >  如果 SQL Server 代理停止了一段时间然后重新启动，则取决于 SQL 代理停止和启动之间的时间长度，可能会看到备份活动增多，并且可能有日志备份的积压工作等待运行。 应考虑将 SQL Server 代理配置为在启动时自动启动。  
  
-   将身份验证信息存储到存储帐户的 Azure 存储帐户和 SQL 凭据应该在配置之前创建 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 有关详细信息，请参阅 [SQL Server 备份到 URL](../relational-databases/backup-restore/sql-server-backup-to-url.md#intorkeyconcepts) 主题的 **Introduction to Key Components and Concepts** 部分以及 [Lesson 2: Create a SQL Server Credential](../../2014/tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]创建存储备份所需的容器。 使用 "计算机名称-实例名称" 格式创建容器名称。 对于 AlwaysOn 可用性组，使用可用性组的 GUID 为容器命名。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 若要运行启用的存储过程 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，您必须是 `System Administrator` 具有**ALTER ANY CREDENTIAL**权限的**db_backupoperator**数据库角色中的或成员，以及 `EXECUTE` 对**sp_delete_backuphistory**和 `smart_admin.sp_backup_master_switch` 存储过程的权限。  用于查看现有设置的存储过程和函数通常分别需要针对存储过程的 `Execute` 权限以及针对函数的 `Select` 权限。  
  

  
###  <a name="considerations-for-enabling-ss_smartbackup-for-databases-and-instances"></a><a name="Considerations"></a>为 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 数据库和实例启用的注意事项  
 可单独为各个数据库或为整个实例启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 具体选项取决于针对实例上数据库的可恢复性要求，管理多个数据库和实例的要求，以及在战略上使用 Azure 存储。  
  
#### <a name="enabling-ss_smartbackup-at-the-database-level"></a>在数据库级别启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 如果数据库对于备份和保持期（可恢复性 SLA）的具体要求与实例上其他的数据库不同，则为该数据库在数据库级别配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 数据库级别设置将取代实例级别配置设置。 但是，可对同一实例一起使用这两个选项。 下面列出了在数据库级别启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的优点和注意事项。  
  
-   更精细：每个数据库有单独的配置设置。 个别数据库可支持不同的保持期。  
  
-   取代数据库的实例级别设置。  
  
-   可用于通过选择要备份的单独数据库，降低存储成本。  
  
-   需要管理每个数据库  
  
#### <a name="enabling-ss_smartbackup-at-the-instance-level-with-default-settings"></a>使用默认设置在实例级别启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 如果实例中的大多数数据库对备份和保持策略具有相同的要求，或者如果您希望在创建时自动备份新数据库实例，则使用此设置。 仍可单独配置对于策略是例外的几个数据库。 下面是在实例级别启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的好处和注意事项的列表。  
  
-   实例级别的自动化：常用设置自动应用于之后新添加的数据库。  
  
-   在实例上创建新数据库后很快就自动备份这些数据库  
  
-   可应用于保持期要求相同的数据库。  
  
-   即使在实例级别启用了 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 备份并配置了默认设置，也仍可配置需要不同保持期的个别数据库。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]如果不打算使用 Azure 存储进行备份，也可以对数据库禁用。  
  
##  <a name="enable-and-configure-ss_smartbackup-for-a-database"></a><a name="DatabaseConfigure"></a>为数据库启用和配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 系统存储过程 `smart_admin.sp_set_db_backup` 用于为特定数据库启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 首次对数据库启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 时，除了启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之外，还必须指定以下信息：  
  
-   数据库的名称。  
  
-   保持期。  
  
-   用于对 Azure 存储帐户进行身份验证的 SQL 凭据。  
  
-   指定不使用* \@ encryption_algorithm*NO_ENCRYPTION 进行加密，  =  **NO_ENCRYPTION**或指定支持的加密算法。 有关加密的详细信息，请参阅 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)。  
  
 仅通过 Transact-SQL 支持针对数据库级别配置的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
 为数据库启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 后，将保持此信息。 如果要更改配置，则只需要数据库名称和要更改的设置，未指定其他参数的现有值时， [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 保留这些值。  
  
> [!IMPORTANT]  
>  在某一数据库上配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 前，它对于现有配置（如果有）可能会很有用。 在本节的后面将介绍查看数据库的配置设置的步骤。  
  
-   **使用 Transact-sql：**  
  
     如果是 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 首次启用，则所需的参数为： * \@ database_name*、 * \@ credential_name* * \@ encryption_algorithm*， * \@ enable_backup* * \@ storage_url*参数是可选的。 如果未提供参数的值 @storage_url ，则使用 SQL 凭据中的存储帐户信息来派生该值。 如果提供存储 URL，则只应为存储帐户的根提供该 URL，并且该 URL 必须与您指定的 SQL 凭据中的信息相符。  
  
    1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
    2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
    3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。 此示例 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 为数据库 "TestDB" 启用。 保持期设置为 30 天。 本例通过指定加密算法和加密程序信息，使用加密选项。  
  
    ```sql
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@enable_backup=1  
                    ,@retention_days =30   
                    ,@credential_name ='MyCredential'  
                    ,@encryption_algorithm ='AES_256'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
    GO
    ```  
  
    > [!IMPORTANT]  
    >  保持期可设置为从 1 到 30 天之间的任何值。  
    >   
    >  有关如何创建加密证书的详细信息，请参阅 [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)中的“创建备份证书”步骤。  
  
     有关此存储过程的详细信息，请参阅[smart_admin set_db_backup &#40;transact-sql&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)  
  
     若要查看数据库的配置设置，请使用以下查询：  
  
    ```sql
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('TestDB')  
    ```  
  
##  <a name="enable-and-configure-default-ss_smartbackup-settings-for-the-instance"></a><a name="InstanceConfigure"></a>为实例启用和配置默认 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 设置  
 可以 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 通过两种方式在实例级别启用和配置默认设置：使用系统存储过程 `smart_admin.set_instance_backup` 或**SQL Server Management Studio**。 下面说明了这两种方法：  
  
 **smart_admin. set_instance_backup：**。 通过为* \@ enable_backup*参数指定值**1** ，可以启用备份并设置默认配置。 在实例级别应用后，将这些默认设置应用于添加到此实例的任何新数据库。  首次启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 时，除了对实例启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 之外，还必须提供以下信息：  
  
-   保持期。  
  
-   用于对 Azure 存储帐户进行身份验证的 SQL 凭据。  
  
-   加密选项。 指定不使用* \@ encryption_algorithm*NO_ENCRYPTION 进行加密，  =  **NO_ENCRYPTION**或指定支持的加密算法。 有关加密的详细信息，请参阅 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)。  
  
 启用后，这些设置将被保留。 如果要更改配置，则只需要数据库名称和要更改的设置。 未指定现有的值时，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]保留这些值。  
  
> [!IMPORTANT]  
>  在某一实例上配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 前，它对于检查现有配置（如果有）可能会很有用。 在本节的后面将介绍查看数据库的配置设置的步骤。  
  
 **SQL Server Management Studio：** 若要在 SQL Server Management Studio 中执行此任务，请转到对象资源管理器，展开 **“管理”** 节点，然后右键单击 **“托管备份”**。 选择“配置” 。 这将打开 **“托管备份”** 对话框。 使用此对话框可指定保持期、SQL 凭据、存储 URL 和加密设置。 有关此对话框的特定帮助，请参阅[配置托管备份 &#40;SQL Server Management Studio&#41;](configure-managed-backup-sql-server-management-studio.md)。  
  
#### <a name="using-transact-sql"></a>“使用 Transact-SQL”  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。  
  
```sql
Use msdb;  
Go  
   EXEC smart_admin.sp_set_instance_backup  
                @retention_days=30   
                ,@credential_name='sqlbackuptoURL'  
                ,@encryption_algorithm ='AES_128'  
                ,@encryptor_type= 'Certificate'  
                ,@encryptor_name='MyBackupCert'  
                ,@enable_backup=1;  
GO  
  
```  
  
> [!IMPORTANT]  
>  保持期可设置为从 1 到 30 天之间的任何值。  
>   
>  有关如何创建加密证书的详细信息，请参阅 [Create an Encrypted Backup](../relational-databases/backup-restore/create-an-encrypted-backup.md)中的“创建备份证书”步骤。  
  
 若要查看实例的默认配置设置，请使用以下查询：  
  
```sql
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_instance_config ();
```  
  
#### <a name="using-powershell"></a>使用 PowerShell  
  
1.  启动 PowerShell 实例  
  
2.  在修改后运行以下脚本以便适合您的设置  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    $encryptionOption = New-SqlBackupEncryptionOption -EncryptionAlgorithm Aes128 -EncryptorType ServerCertificate -EncryptorName "MyBackupCert"  
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -BackupEnabled $True -BackupRetentionPeriodInDays 10 -EncryptionOption $encryptionOption  
    ```  
  
> [!IMPORTANT]  
>  在您在配置默认设置后创建新的数据库时，最多需要用 15 分钟以便使用默认设置配置该数据库。 这也将应用于从 **Simple** 更改为 **Full** 或 **Bulk-Logged** 恢复模型的数据库。  
  
##  <a name="disable-ss_smartbackup-for-a-database"></a><a name="DatabaseDisable"></a> 为数据库禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 可通过使用 `sp_set_db_backup` 系统存储过程，禁用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]设置。 * \@ Enableparameter*用于启用和禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 特定数据库的配置; 其中，1启用，0禁用配置设置。  
  
#### <a name="to-disable-ss_smartbackup-for-a-specific-database"></a>为特定数据库禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ：  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。  
  
```sql
Use msdb;  
Go  
EXEC smart_admin.sp_set_db_backup   
                @database_name='TestDB'   
                ,@enable_backup=0;  
GO
```  
  
##  <a name="disable-ss_smartbackup-for-all-the-databases-on-the-instance"></a><a name="DatabaseAllDisable"></a> 为实例上的所有数据库禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 下面的过程适用于要从实例上当前启用了 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 的所有数据库禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 配置设置的情形。  存储 URL、保持和 SQL 凭据之类的配置设置将在元数据中保留；并且如果以后为数据库启用了 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，则可以使用这些设置。 如果您要暂停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服务，则可以使用在本主题后面的以下部分中说明的主开关。  
  
#### <a name="to-disable-ss_smartbackupfor-all-the-databases"></a>为所有数据库禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]：  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。 下例确定是否在实例级别配置了[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]以及是否所有启用了[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的数据库都在实例上，并且执行系统存储过程 `sp_set_db_backup` 以禁用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
```sql
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM
  
       smart_admin.fn_backup_db_config (NULL)  
       WHERE is_smart_backup_enabled = 1  
  
       --Select DBName from @DBNames 
       select @rowid = min(RowID) FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC smart_admin.sp_set_db_backup    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END
```  
  
 若要查看实例上所有数据库的配置设置，请使用以下查询：  
  
```sql
Use msdb;  
GO  
SELECT * FROM smart_admin.fn_backup_db_config (NULL);  
GO
```  
  
##  <a name="disable-default-ss_smartbackup-settings-for-the-instance"></a><a name="InstanceDisable"></a> 禁用实例的默认 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 设置  
 实例级别的默认设置适用于在该实例上创建的所有新数据库。  如果不再需要默认设置，则可以通过使用 **smart_admin.sp_set_instance_backup** 系统存储过程，禁用此配置。 禁用并不会删除存储 URL、保持设置或 SQL 凭据名称之类的其他配置设置。 如果以后为该实例启用了 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，将使用这些设置。  
  
#### <a name="to-disable-ss_smartbackup-default-configuration-settings"></a>禁用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 默认配置设置：  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。  
  
    ```sql
    Use msdb;  
    Go  
    EXEC smart_admin.sp_set_instance_backup  
                    @enable_backup=0;  
    GO
    ```  
  
#### <a name="using-powershell"></a>使用 PowerShell  
  
1.  启动 PowerShell 实例  
  
2.  运行以下脚本：  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Set-SqlSmartAdmin -BackupEnabled $False  
    ```  
  
##  <a name="pause-ss_smartbackup-at-the-instance-level"></a><a name="InstancePause"></a> 在实例级别暂停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 有时可能需要在短期内临时暂停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服务。  通过 `smart_admin.sp_backup_master_switch` 系统存储过程，可在实例级别禁用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]服务。  使用相同的存储过程恢复 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 @state 参数用于定义是应禁用还是启用 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
#### <a name="to-pause-ss_smartbackup-services-using-transact-sql"></a>使用 Transact-SQL 暂停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服务：  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击`Execute`  
  
```sql
Use msdb;  
GO  
EXEC smart_admin.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-pause-ss_smartbackup-using-powershell"></a>使用 PowerShell 暂停 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
  
1.  启动 PowerShell 实例  
  
2.  在修改后运行以下脚本以便适合您的设置  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $False  
    ```  
  
#### <a name="to-resume-ss_smartbackup-using-transact-sql"></a>使用 Transact-SQL 恢复 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ：  
  
1.  连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击 `Execute` 。  
  
```sql
Use msdb;  
Go  
EXEC smart_admin. sp_backup_master_switch @new_state=1;  
GO
```  
  
#### <a name="to-resume-ss_smartbackup-using-powershell"></a>使用 PowerShell 恢复 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
  
1.  启动 PowerShell 实例  
  
2.  在修改后运行以下脚本以便适合您的设置  
  
    ```powershell
    cd SQLSERVER:\SQL\Computer\MyInstance
    Get-SqlSmartAdmin | Set-SqlSmartAdmin -MasterSwitch $True  
    ```  
