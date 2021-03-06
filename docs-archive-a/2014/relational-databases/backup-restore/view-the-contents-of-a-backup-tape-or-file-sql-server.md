---
title: 查看备份磁带或文件的内容 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], tapes
- displaying backup content
- viewing backup content
- tape backup devices, viewing contents
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 044519b64d41fbbdfc9302ce24369ab282727f67
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690663"
---
# <a name="view-the-contents-of-a-backup-tape-or-file-sql-server"></a>查看备份磁带或文件的内容 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看备份磁带或文件的内容。  
  
> [!NOTE]  
>  在 SQL Server 的未来版本中将不再支持磁带备份设备。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要查看备份磁带或文件的内容，可使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
 有关安全性的信息，请参阅 [RESTORE HEADERONLY (Transact SQL)](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更高版本中，获取有关备份集或备份设备的信息要求具有 CREATE DATABASE 权限。 有关详细信息，请参阅 [GRANT 数据库权限 (Transact-SQL)](/sql/t-sql/statements/grant-database-permissions-transact-sql)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>查看备份磁带或文件的内容  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例之后，在“对象资源管理器”中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”** ，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击要备的数据库，指向  “任务”，再单击  “备份”。 将出现 **“备份数据库”** 对话框。  
  
4.  在 **“常规”** 页的 **“目标”** 部分中，单击 **“磁盘”** 或 **“磁带”** 。 在 **“备份到”** 列表框中，查找所需的磁盘文件或磁带。  
  
     如果磁盘文件或磁带未显示在列表框中，请单击  “添加”。 选择一个文件名或磁带机。 若要将其添加到  “备份到”列表框，请单击  “确定”。  
  
5.  在  “备份到”列表框中，选择要查看的磁盘或磁带机的路径，再单击  “内容”。 将打开 **“设备内容”** 对话框。  
  
6.  右侧窗格显示有关所选磁带或文件上的介质集和备份集的信息。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>查看备份磁带或文件的内容  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  使用 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 语句。 此示例将返回有关名为 `AdventureWorks2012-FullBackup.bak`的文件的信息。  
  
```sql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [backupfilegroup (Transact-SQL)](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile (Transact-SQL)](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset (Transact-SQL)](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset (Transact-SQL)](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily (Transact-SQL)](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [备份设备 (SQL Server)](backup-devices-sql-server.md)   
 [为磁盘文件定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [为磁带驱动器定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
