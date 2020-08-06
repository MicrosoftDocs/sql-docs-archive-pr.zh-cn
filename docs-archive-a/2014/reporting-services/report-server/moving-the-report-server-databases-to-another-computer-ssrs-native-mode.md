---
title: 将报表服务器数据库移动到其他计算机（SSRS 本机模式）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 44a9854d-e333-44f6-bdc7-8837b9f34416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 49fd35f57cf783b262b3c690e3047e5f479ab193
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682667"
---
# <a name="moving-the-report-server-databases-to-another-computer-ssrs-native-mode"></a>将报表服务器数据库移至其他计算机（SSRS 本机模式）
  可以将安装中使用的 Report Server 数据库移动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 到其他计算机上的实例。 必须一同移动或复制数据库 reportserver 和数据库 reportservertempdb。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装需要这两个数据库；reportservertempdb 数据库必须按名称与将要移动的 reportserver 主数据库相关。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。  
  
 移动数据库不会影响当前为报表服务器项定义的计划操作。  
  
-   首次重新启动报表服务器服务时会重新创建计划。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业。 您不必将作业移到新计算机上，不过您可能需要删除计算机上不再使用的作业。  
  
-   订阅、缓存报表和快照将保留在移动的数据库中。 如果在数据库移动之后快照不选取刷新的数据，则在报表管理器中清除快照选项，单击“应用”保存更改，重新创建计划，然后再次单击“应用”保存所做的更改********。  
  
-   移动数据库时，会保留 reportservertempdb 中存储的临时报表和用户会话数据。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了多种移动数据库的方法，包括备份和还原、附加和分离以及复制。 并不是所有的方法都适用于将现有数据库重新定位到新的服务器实例。 根据您的系统可用性要求，移动报表服务器数据库的方法会有所不同。 移动报表服务器数据库的最简单方法是附加和分离数据库。 但是，此方法要求您在分离数据库的同时使报表服务器脱机。 如果要最大程度地减少服务中断，则备份和还原是最佳选择，但是必须运行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令以执行操作。 建议不要复制数据库（特别是不要使用复制数据库向导）；这样做将不保留数据库中的权限设置。  
  
> [!IMPORTANT]  
>  当重新定位报表服务器数据库是对现有安装的唯一更改时，建议执行本主题中提供的步骤。 若要迁移整个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装（即，移动数据库并更改使用该数据库的报表服务器 Windows 服务的标识），需要重新配置连接并重置加密密钥。  
  
## <a name="detaching-and-attaching-the-report-server-databases"></a>分离和附加报表服务器数据库  
 如果可使报表服务器脱机，则可分离数据库，以将其移至要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 此方法将保留数据库中的权限。 如果在使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 数据库，则必须将其移至另一个 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例。 移动数据库后，必须重新配置报表服务器与报表服务器数据库的连接。 如果您运行的是扩展部署，则必须为部署中的每个报表服务器重新配置报表服务器数据库连接。  
  
 请使用下列步骤来移动数据库：  
  
1.  为要移动的报表服务器数据库备份加密密钥。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具来备份密钥。  
  
2.  停止报表服务器服务。 可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具停止该服务。  
  
3.  启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 并打开与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 承载 Report Server 数据库的实例的连接。  
  
4.  右键单击该报表服务器数据库，指向“任务”，并单击“分离”****。 对报表服务器临时数据库重复此步骤。  
  
5.  将 .mdf 和 .ldf 文件复制或移至要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 Data 文件夹中。 由于要移动两个数据库，因此请确保移动或复制所有四个文件。  
  
6.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开与将承载报表服务器数据库的新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接。  
  
7.  右键单击“数据库”节点，然后单击“附加”****。  
  
8.  单击 **“添加”** 以选择要附加的报表服务器数据库 .mdf 和 .ldf 文件。 对报表服务器临时数据库重复此步骤。  
  
9. 附加数据库后，验证 `RSExecRole` 是否是 Report Server 数据库和临时数据库中的数据库角色。 `RSExecRole`必须对 Report Server 数据库表具有 select、insert、update、delete 和 reference 权限，以及对存储过程的 execute 权限。 有关详细信息，请参阅 [创建 RSExecRole](../security/create-the-rsexecrole.md)。  
  
10. 启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具并打开与报表服务器的连接。  
  
11. 在“数据库”页上，选择新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，然后单击 **“连接”**。  
  
12. 选择刚才移动的报表服务器数据库，然后单击 **“应用”**。  
  
13. 在“加密密钥”页上，单击“还原”。 指定包含密钥备份副本的文件以及该文件的解锁密码。  
  
14. 重新启动报表服务器服务。  
  
## <a name="backing-up-and-restoring-the-report-server-databases"></a>备份和还原报表服务器数据库  
 如果不能使报表服务器脱机，则可使用备份和还原来重新定位报表服务器数据库。 您必须使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句执行备份和还原。 还原数据库后，必须将报表服务器配置为使用新服务器实例上的数据库。 有关详细信息，请参阅本主题结尾的说明。  
  
### <a name="using-backup-and-copy_only-to-backup-the-report-server-databases"></a>使用 BACKUP 和 COPY_ONLY 备份报表服务器数据库  
 备份数据库时，请设置 COPY_ONLY 参数。 请确保备份数据库和日志文件。  
  
```  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServer  
   SET RECOVERY FULL  
  
-- If the ReportServerData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerData',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerData.bak'  
  
-- Create a logical backup device, ReportServerLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerLog.bak'  
  
-- Back up the full ReportServer database.  
BACKUP DATABASE ReportServer  
   TO ReportServerData  
   WITH COPY_ONLY  
  
-- Back up the ReportServer log.  
BACKUP LOG ReportServer  
   TO ReportServerLog  
   WITH COPY_ONLY  
  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServerTempdb  
   SET RECOVERY FULL  
  
-- If the ReportServerTempDBData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBData',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBData.bak'  
  
-- Create a logical backup device, ReportServerTempDBLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBLog.bak'  
  
-- Back up the full ReportServerTempDB database.  
BACKUP DATABASE ReportServerTempDB  
   TO ReportServerTempDBData  
   WITH COPY_ONLY  
  
-- Back up the ReportServerTempDB log.  
BACKUP LOG ReportServerTempDB  
   TO ReportServerTempDBLog  
   WITH COPY_ONLY  
```  
  
### <a name="using-restore-and-move-to-relocate-the-report-server-databases"></a>使用 RESTORE 和 MOVE 重新定位报表服务器数据库  
 还原数据库时，请务必包括 MOVE 参数，以便指定路径。 使用 NORECOVERY 参数执行初始还原；此操作可使数据库保持 RESTORING 状态，给您留出时间来检查日志备份，以确定要还原的备份。 最后一步是重复包含 RECOVERY 参数的 RESTORE 操作。  
  
 MOVE 参数使用数据文件的逻辑名称。 若要找到逻辑名称，请执行下列语句： `RESTORE FILELISTONLY FROM DISK='C:\ReportServerData.bak';`  
  
 以下示例包括 FILE 参数，因此您可以指定要还原的日志文件的文件位置。 若要找到文件位置，请执行下列语句： `RESTORE HEADERONLY FROM DISK='C:\ReportServerData.bak';`  
  
 还原数据库和日志文件时，应单独运行每个 RESTORE 操作。  
  
```  
-- Restore the report server database and move to new instance folder   
RESTORE DATABASE ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore the report server log file to new instance folder   
RESTORE LOG ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore and move the report server temporary database  
RESTORE DATABASE ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Restore the temporary database log file to new instance folder   
RESTORE LOG ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServer  
   WITH RECOVERY  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServerTempDB  
   WITH RECOVERY  
GO  
```  
  
### <a name="how-to-configure-the-report-server-database-connection"></a>如何配置报表服务器数据库连接  
  
1.  启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器并连接到报表服务器。  
  
2.  在“数据库”页上，单击 **“更改数据库”**。 单击“下一步”。  
  
3.  单击 **“选择现有报表服务器数据库”**。 单击“下一步”。  
  
4.  选择现在承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并单击 **“测试连接”**。 单击“下一步”。  
  
5.  在“数据库名称”中，选择要使用的报表服务器数据库。 单击“下一步”。  
  
6.  在“凭据”中，指定报表服务器用来连接到报表服务器数据库的凭据。 单击“下一步”。  
  
7.  单击 **“下一步”** ，然后单击 **“完成”**。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装要求 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例包含 `RSExecRole` 角色。 通过 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具设置报表服务器数据库连接时，将创建角色、注册登录信息并分配角色。 如果使用备用方法（具体来说，如果使用 rsconfig.exe 命令提示实用工具）来配置连接，报表服务器不会处于工作状态。 您可能需要编写 WMI 代码以使报表服务器可用。 有关详细信息，请参阅 [访问 Reporting Services WMI 提供程序](../tools/access-the-reporting-services-wmi-provider.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建 RSExecRole](../security/create-the-rsexecrole.md)   
 [启动和停止报表服务器服务](start-and-stop-the-report-server-service.md)   
 [&#40;SSRS Configuration Manager 配置报表服务器数据库连接&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [&#40;SSRS Configuration Manager 配置无人参与的执行帐户&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [rsconfig 实用工具 &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [&#40;SSRS Configuration Manager 中配置和管理加密密钥&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [报表服务器数据库（SSRS 本机模式）](report-server-database-ssrs-native-mode.md)  
  
  
