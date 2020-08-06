---
title: 启用 FileTable 的先决条件 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5d5d2c5dab7909ec5403911d482823f488cdd809
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576839"
---
# <a name="enable-the-prerequisites-for-filetable"></a>启用 FileTable 的先决条件
  介绍如何启用创建和使用 FileTable 的先决条件。  
  
##  <a name="enabling-the-prerequisites-for-filetable"></a><a name="EnablePrereq"></a> 启用 FileTable 的先决条件  
 若要启用创建和使用 FileTable 的先决条件，请启用下列项目：  
  
-   **在实例级别：**  
  
    -   [在实例级别启用 FILESTREAM](#BasicsFilestream)  
  
-   **在数据库级别：**  
  
    -   [在数据库级别提供 FILESTREAM 文件组](#filegroup)  
  
    -   [在数据库级别启用非事务性访问](#BasicsNTAccess)  
  
    -   [在数据库级别指定 FileTable 的目录](#BasicsDirectory)  
  
##  <a name="enabling-filestream-at-the-instance-level"></a><a name="BasicsFilestream"></a> 在实例级别启用 FILESTREAM  
 FileTable 扩展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 FILESTREAM 功能。 因此，在创建和使用 FileTable 前，必须在 Windows 级别和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上启用 FILESTREAM 用于文件 I/O 访问。  
  
###  <a name="how-to-enable-filestream-at-the-instance-level"></a><a name="HowToFilestream"></a> 如何：在实例级别启用 FILESTREAM  
 有关如何启用 FILESTREAM 的信息，请参阅 [启用和配置 FILESTREAM](enable-and-configure-filestream.md)。  
  
 当您调用 `sp_configure` 在实例级别启用 FILESTREAM 时，必须将 filestream_access_level 选项设置为 2。 有关详细信息，请参阅 [文件流访问级别服务器配置选项](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)。  
  
###  <a name="how-to-allow-filestream-through-the-firewall"></a><a name="firewall"></a> 如何：允许 FILESTREAM 通过防火墙  
 有关如何允许 FILESTREAM 通过防火墙的信息，请参阅 [Configure a Firewall for FILESTREAM Access](configure-a-firewall-for-filestream-access.md)。  
  
##  <a name="providing-a-filestream-filegroup-at-the-database-level"></a><a name="filegroup"></a> 在数据库级别提供 FILESTREAM 文件组  
 数据库必须首先具有 FILESTREAM 文件组，然后您才能在该数据库中创建 FileTable。 有关此先决条件的详细信息，请参阅 [创建启用了 FILESTREAM 的数据库](create-a-filestream-enabled-database.md)。  
  
##  <a name="enabling-non-transactional-access-at-the-database-level"></a><a name="BasicsNTAccess"></a> 在数据库级别启用非事务性访问  
 FileTable 使 Windows 应用程序可以获取 FILESTREAM 数据的 Windows 文件句柄而不需要事务。 为了允许对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的文件进行此非事务性访问，您必须为要包含 FileTable 的每个数据库在数据库级别上指定所需的非事务性访问级别。  
  
###  <a name="how-to-check-whether-non-transactional-access-is-enabled-on-databases"></a><a name="HowToCheckAccess"></a> 如何：检查是否在数据库上启用了非事务性访问  
 查询目录视图 [sys.database_filestream_options (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql) 并检查 **non_transacted_access** 和 **non_transacted_access_desc** 列。  
  
```sql  
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="how-to-enable-non-transactional-access-at-the-database-level"></a><a name="HowToNTAccess"></a> 如何：在数据库级别启用非事务性访问  
 非事务性访问的可用级别为 FULL、READ_ONLY 和 OFF。  
  
 **使用 Transact-SQL 指定非事务性访问的级别**  
 -   **创建新数据库**时，调用带 **NON_TRANSACTED_ACCESS** FILESTREAM 选项的 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql) 语句。  
  
    ```sql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
-   **更改现有数据库**时，调用带 **NON_TRANSACTED_ACCESS** FILESTREAM 选项的 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql) 语句。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
 **使用 SQL Server Management Studio 指定非事务性访问的级别**  
 可以在“数据库属性”  对话框的“选项”  页的“FILESTREAM 非事务性访问”  字段中指定非事务性访问的级别。 有关此对话框的详细信息，请参阅[数据库属性（选项页）](../databases/database-properties-options-page.md)。  
  
##  <a name="specifying-a-directory-for-filetables-at-the-database-level"></a><a name="BasicsDirectory"></a> 在数据库级别指定 FileTable 的目录  
 在数据库级别启用对文件的非事务性访问时，可以选择使用 **DIRECTORY_NAME** 选项同时提供一个目录名称。 如果启用非事务性访问时没有提供目录名称，则在以后必须提供它，这样才能在数据库中创建 FileTable。  
  
 在 FileTable 文件夹层次结构中，此数据库级目录将成为在实例级别为 FILESTREAM 指定的共享名称的子级以及在数据库中创建的 FileTable 的父级。 有关详细信息，请参阅 [Work with Directories and Paths in FileTables](work-with-directories-and-paths-in-filetables.md)。  
  
###  <a name="how-to-specify-a-directory-for-filetables-at-the-database-level"></a><a name="HowToDirectory"></a> 如何：在数据库级别指定 FileTable 的目录  
 您指定的名称必须在跨数据库级目录的实例中是唯一的。  
  
 **使用 Transact-SQL 指定 FileTable 的目录**  
 -   **创建新数据库**时，调用带 **DIRECTORY_NAME** FILESTREAM 选项的 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql) 语句。  
  
    ```sql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **更改现有数据库**时，调用带 **DIRECTORY_NAME** FILESTREAM 选项的 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql) 语句。 使用这些选项更改目录名称时，数据库必须以独占方式锁定，没有打开的文件句柄。  
  
    ```sql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **附加数据库**时，调用带 **FOR ATTACH** 选项和 **DIRECTORY_NAME** FILESTREAM 选项的 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql) 语句。  
  
    ```sql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   **还原数据库**时，调用带 **DIRECTORY_NAME** FILESTREAM 选项的 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql) 语句。  
  
    ```sql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **使用 SQL Server Management Studio 指定 FileTable 的目录**  
 可以在“数据库属性”  对话框的“选项”  页的“FILESTREAM 目录名称”  字段中指定目录名称。 有关此对话框的详细信息，请参阅[数据库属性（选项页）](../databases/database-properties-options-page.md)。  
  
###  <a name="how-to-view-existing-directory-names-for-the-instance"></a><a name="viewnames"></a> 如何：查看实例的现有目录名  
 若要查看该实例的现有目录名称的列表，可查询目录视图 [sys.database_filestream_options (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql) 并查看 **filestream_database_directory_name** 列。  
  
```sql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="requirements-and-restrictions-for-the-database-level-directory"></a><a name="ReqDirectory"></a> 数据库级别目录的要求和限制  
  
-   在调用 **CREATE DATABASE** 或 **ALTER DATABASE** 时，设置 **DIRECTORY_NAME**是可选的。 如果未指定 **DIRECTORY_NAME**的值，则目录名称仍是 Null。 但不能在数据库中创建 FileTable，直到在数据库级别指定了 **DIRECTORY_NAME** 的值。  
  
-   您提供的目录名称必须符合文件系统对有效目录名称的要求。  
  
-   当数据库包含 FileTable 时，不能将 **DIRECTORY_NAME** 设置回为 Null 值。  
  
-   附加或还原数据库时，如果新数据库的 **DIRECTORY_NAME** 值在目标实例中已存在，则该操作失败。 调用 **CREATE DATABASE FOR ATTACH** 或 **RESTORE DATABASE** 时，指定 **DIRECTORY_NAME**的唯一值。  
  
-   当将现有数据库升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时， **DIRECTORY_NAME** 的值为 Null。  
  
-   在数据库级别启用或禁用非事务性访问时，该操作不检查是否已指定目录名称或该名称是否唯一。  
  
-   删除已为 FileTable 启用的数据库时，将删除数据库级目录和其下的所有 FileTable 的所有目录结构。  
  
  
