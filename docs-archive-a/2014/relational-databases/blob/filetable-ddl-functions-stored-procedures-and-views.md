---
title: FileTable DDL、函数、存储过程和视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], database objects
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3fca483581a47720cf0d923506f4439e3e614520
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692964"
---
# <a name="filetable-ddl-functions-stored-procedures-and-views"></a>FileTable DDL、函数、存储过程和视图
  列出用于在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中支持 FileTable 功能的新增或更改的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库对象。  
  
 下表中的“状态”列指示此项是 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的新增功能，还是在早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已存在但在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中已更改用于支持语义搜索。  
  
 有关支持 FILESTREAM 的语句和数据库对象的列表，请参阅 [FILESTREAM DDL, Functions, Stored Procedures, and Views](../views/views.md)。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL 数据定义语言 (DDL) 语句  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)<br /><br /> [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)|已更改|[启用 FileTable 的先决条件](enable-the-prerequisites-for-filetable.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[ALTER TABLE (Transact-SQL)](/sql/t-sql/statements/alter-table-transact-sql)|已更改|[创建、更改和删除 FileTable](create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)|已更改|[启用 FileTable 的先决条件](enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE (Transact-SQL)](/sql/t-sql/statements/create-table-transact-sql)|已更改|[创建、更改和删除 FileTable](create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)<br /><br /> [RESTORE 参数 (Transact-SQL)](/sql/t-sql/statements/restore-statements-arguments-transact-sql)|已更改||  
  
##  <a name="functions"></a><a name="func"></a> 函数  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[FileTableRootPath (Transact-SQL)](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|**已添加**|[在 FileTable 中使用目录和路径](work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath (Transact-SQL)](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|**已添加**|[在 FileTable 中使用目录和路径](work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator (Transact-SQL)](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|**已添加**|[在 FileTable 中使用目录和路径](work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="stored-procedures"></a><a name="sproc"></a> 存储过程  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles (Transact-SQL)](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles)|**已添加**|[管理 FileTable](manage-filetables.md)|  
  
##  <a name="catalog-views"></a><a name="cv"></a> 目录视图  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sys.database_filestream_options (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql)|**已添加**|[启用 FileTable 的先决条件](enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)|**已添加**|[创建、更改和删除 FileTable](create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](manage-filetables.md)|  
|[sys.filetables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)|**已添加**|[管理 FileTable](manage-filetables.md)|  
|[sys.tables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|已更改|[管理 FileTable](manage-filetables.md)|  
  
##  <a name="dynamic-management-views"></a><a name="dmv"></a> 动态管理视图  
  
|Object|状态|更多信息|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)|**已添加**|[管理 FileTable](manage-filetables.md)|  
  
## <a name="see-also"></a>另请参阅  
 [管理 FileTable](manage-filetables.md)  
  
  
