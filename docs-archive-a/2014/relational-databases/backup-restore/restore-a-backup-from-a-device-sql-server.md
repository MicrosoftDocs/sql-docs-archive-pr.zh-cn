---
title: 从设备还原备份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], device restores
- backup devices [SQL Server], restoring from
- database restores [SQL Server], device restores
- devices [SQL Server]
ms.assetid: 6e139de7-7de2-4d18-9df0-beac31ba7ff1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 50d7f7b8e255aea470a1065df669c0cc3169a8dd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688953"
---
# <a name="restore-a-backup-from-a-device-sql-server"></a>从设备还原备份 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中从设备还原备份。  
  
> [!NOTE]  
>  有关 SQL Server 备份到 Azure Blob 存储服务的信息，请参阅[SQL Server 通过 Azure Blob 存储服务进行备份和还原](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要从设备还原备份，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 如果不存在要还原的数据库，则用户必须有 CREATE DATABASE 权限才能执行 RESTORE。 如果数据库存在，则 RESTORE 权限默认授予 **sysadmin** 和 **dbcreator** 固定服务器角色成员以及数据库的所有者 (**dbo**)（对于 FROM DATABASE_SNAPSHOT 选项，数据库始终存在）。  
  
 RESTORE 权限被授予那些成员身份信息始终可由服务器使用的角色。 因为只有在固定数据库可以访问且没有损坏时（在执行 RESTORE 时并不会总是这样）才能检查固定数据库角色成员身份，所以 **db_owner** 固定数据库角色成员没有 RESTORE 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-restore-a-backup-from-a-device"></a>从设备还原备份  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例之后，在“对象资源管理器”中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”** ，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击数据库，指向“任务”  ，再单击“还原”  。  
  
4.  单击所需的还原操作类型（“数据库”  、“文件和文件组”  或“事务日志”  ）。 这将打开相应的还原对话框。  
  
5.  在 **“常规”** 页的 **“还原的源”** 部分，单击 **“源设备”** 。  
  
6.  单击 **“源设备”** 文本框中的浏览按钮，这将打开 **“指定备份”** 对话框。  
  
7.  在 **“备份介质”** 文本框中，选择 **“备份设备”** ，然后单击 **“添加”** 按钮以打开 **“选择备份设备”** 对话框。  
  
8.  在 **“备份设备”** 文本框中，选择要用于还原操作的设备。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-restore-a-backup-from-a-device"></a>从设备还原备份  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  在 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 语句中，指定用于备份操作的逻辑备份设备或物理备份设备。 此示例从具有物理名称 `Z:\SQLServerBackups\AdventureWorks2012.bak`的磁盘文件还原。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' ;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [RESTORE FILELISTONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE HEADERONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)   
 [RESTORE LABELONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [RESTORE VERIFYONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [在简单恢复模式下还原数据库备份 (Transact-SQL)](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)   
 [还原数据库备份 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [还原差异数据库备份 (SQL Server)](restore-a-differential-database-backup-sql-server.md)   
 [将数据库还原到新位置 (SQL Server)](restore-a-database-to-a-new-location-sql-server.md)   
 [备份文件和文件组 (SQL Server)](back-up-files-and-filegroups-sql-server.md)   
 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)   
 [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
  
