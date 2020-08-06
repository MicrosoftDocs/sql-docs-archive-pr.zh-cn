---
title: 仅复制备份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fc74d7b1bba2a0163ac9edefb5d465c54ef6296c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591410"
---
# <a name="copy-only-backups-sql-server"></a>仅复制备份 (SQL Server)
  *仅复制备份*是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]独立于常规备份序列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的备份。 通常，进行备份会更改数据库并影响其后备份的还原方式。 但是，有时在不影响数据库总体备份和还原过程的情况下，为特殊目的而进行备份还是有用的。 仅复制备份就是用于此目的。  
  
 仅复制备份的类型如下所示：  
  
-   仅复制完整备份（所有恢复模式）  
  
     仅复制备份不能用作差异基准或差异备份，并且不影响差异基准。  
  
     还原仅复制完整备份与还原任何其他完整备份相同。  
  
-   仅复制日志备份（仅限于完整恢复模式和大容量日志恢复模式）  
  
     仅复制日志备份保留当前日志存档点，因此，不影响常规日志备份的序列。 通常不必进行仅复制日志备份。 相反，您可以创建新的常规日志备份（使用 WITH NORECOVERY），然后将该备份与还原序列所需的任何以前的日志备份一起使用。 但是，仅复制日志备份有时可用于执行联机还原。 关于这方面的示例，请参阅[示例：读/写文件的联机还原（完整恢复模式）](example-online-restore-of-a-read-write-file-full-recovery-model.md)。  
  
     事务日志从不在仅复制备份后出现截断。  
  
 仅复制备份记录在 **backupset** 表的 [is_copy_only](/sql/relational-databases/system-tables/backupset-transact-sql) 列中。  
  
## <a name="to-create-a-copy-only-backup"></a>创建仅复制备份  
 您可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]或 PowerShell 创建仅复制备份。  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
1.  在 **“备份数据库”** 对话框的 **“常规”** 页上，选择 **“仅复制备份”** 选项。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 基本 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语法如下所示：  
  
-   对于仅复制完整备份：  
  
     备份数据库*database_name*到 \<backup_device*> * .。。COPY_ONLY .。。  
  
    > [!NOTE]  
    >  使用 DIFFERENTIAL 选项指定时，COPY_ONLY 不起作用。  
  
-   对于仅复制日志备份：  
  
     备份日志*database_name*到 *\<*backup_device*>* .。。COPY_ONLY .。。  
  
###  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  
  
将 `Backup-SqlDatabase` cmdlet 与 `-CopyOnly` 参数一起使用。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  

### <a name="to-create-a-full-or-log-backup"></a>创建完整备份或日志备份
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
### <a name="to-view-copy-only-backups"></a>查看仅复制备份
  
-   [backupset (Transact-SQL)](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
### <a name="to-set-up-and-use-the-sql-server-powershell-provider"></a>设置和使用 SQL Server PowerShell 提供程序
  
-   [SQL Server PowerShell 提供程序](../../powershell/sql-server-powershell-provider.md)  

## <a name="see-also"></a>另请参阅  
 [备份概述 (SQL Server)](backup-overview-sql-server.md)   
 [恢复模式 (SQL Server)](recovery-models-sql-server.md)   
 [通过备份和还原来复制数据库](../databases/copy-databases-with-backup-and-restore.md)   
 [还原和恢复概述 (SQL Server)](restore-and-recovery-overview-sql-server.md)  
