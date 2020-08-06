---
title: 查看 SQL Server 实例的数据库列表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- current databases
- databases currently on server [SQL Server]
- database list [SQL Server]
- viewing database list
- displaying database list
- databases [SQL Server], viewing
- servers [SQL Server], databases listed on
- listing databases
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 47283fa9065a0b9d6238dab804094d9a65d17897
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693374"
---
# <a name="view-a-list-of-databases-on-an-instance-of-sql-server"></a>查看 SQL Server 实例的数据库列表
  本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查看 [!INCLUDE[tsql](../../includes/tsql-md.md)]实例上的数据库列表。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **查看 SQL Server 实例的数据库列表，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 如果 **sys.databases** 的调用方并非数据库的所有者，并且数据库不是 **master** 或 **tempdb**，则查看对应行所需的最小权限为 ALTER ANY DATABASE 或 VIEW ANY DATABASE 服务器级权限，或者为 **master** 数据库中的 CREATE DATABASE 权限。 始终可以在 **sys.databases**中查看调用方连接的数据库。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>查看 SQL Server 实例的数据库列表  
  
1.  在 **对象资源管理器**中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的实例，然后展开该实例。  
  
2.  若要查看实例上的所有数据库的列表，请展开 **“数据库”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-list-of-databases-on-an-instance-of-sql-server"></a>查看 SQL Server 实例的数据库列表  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上的数据库列表。 该列表包含数据库名称、数据库 ID 和创建数据库的日期。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库和文件目录视图 (Transact-SQL)](/sql/relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
