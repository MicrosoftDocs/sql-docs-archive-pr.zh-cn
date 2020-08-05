---
title: 创建数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], creating
- database creation [SQL Server], SQL Server Management Studio
- creating databases
ms.assetid: 4c4beea2-6cbc-4352-9db6-49ea8130bb64
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe42e394482e3abf4d87c00c6e79ee84db6ba278
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581311"
---
# <a name="create-a-database"></a>创建数据库
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建数据库。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **创建数据库，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   在一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例中最多可以指定 32,767 个数据库。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   CREATE DATABASE 语句必须以自动提交模式（默认事务管理模式）运行，不允许在显式或隐式事务中使用。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
  
-   创建、修改或删除用户数据库后，应备份 [master](master-database.md) 数据库。  
  
-   在创建数据库时，请根据数据库中预期的最大数据量，创建尽可能大的数据文件。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对 master 数据库的 CREATE DATABASE 权限，或需要 CREATE ANY DATABASE/ALTER ANY DATABASE 权限。  
  
 为了控制对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机上的磁盘使用，通常只有少数登录帐户才有创建数据库的权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-database"></a>创建数据库  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的实例，然后展开该实例。  
  
2.  右键单击“数据库”，然后单击“新建数据库”。  
  
3.  在 **“新建数据库”** 中，输入数据库名称。  
  
4.  若要通过接受所有默认值创建数据库，请单击 **“确定”** ；否则，请继续后面的可选步骤。  
  
5.  若要更改所有者名称，请单击 (…) 选择其他所有者。  
  
    > [!NOTE]  
    >  “使用全文检索”选项始终处于选中和灰显状态，这是因为从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，所有用户数据库都启用了全文检索。  
  
6.  若要更改主数据文件和事务日志文件的默认值，请在 **“数据库文件”** 网格中单击相应的单元并输入新值。 有关详细信息，请参阅 [向数据库中添加数据文件或日志文件](add-data-or-log-files-to-a-database.md)。  
  
7.  若要更改数据库的排序规则，请选择 **“选项”** 页，然后从列表中选择一个排序规则。  
  
8.  若要更改恢复模式，请选择 **“选项”** 页，然后从列表中选择一个恢复模式。  
  
9. 若要更改数据库选项，请选择 **“选项”** 页，然后修改数据库选项。 有关各选项的详细说明，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
10. 若要添加新文件组，请单击 **“文件组”** 页。 单击 **“添加”** ，然后输入文件组的值。  
  
11. 若要将扩展属性添加到数据库中，请选择 **“扩展属性”** 页。  
  
    1.  在 **“名称”** 列中，输入扩展属性的名称。  
  
    2.  在 **“值”** 列中，输入扩展属性文本。 例如，输入描述数据库的一个或多个语句。  
  
12. 若要创建数据库，请单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-database"></a>创建数据库  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例将创建数据库 `Sales`。 因为没有使用关键字 PRIMARY，第一个文件 (`Sales`_`dat`) 将成为主文件。 因为在 `Sales`\_`dat` 文件的 SIZE 参数中没有指定 MB 或 KB，将使用 MB 并按 MB 分配。 创建、修改或删除用户数据库后，应备份 `Sales`\_`log` 文件以 MB 为单位进行分配，因为 `MB` 参数中显式声明了 `SIZE` 后缀。  
  
```sql  
USE master ;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
 有关更多示例，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [Database Files and Filegroups](database-files-and-filegroups.md)   
 [数据库分离和附加 (SQL Server)](database-detach-and-attach-sql-server.md)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [向数据库中添加数据文件或日志文件](add-data-or-log-files-to-a-database.md)  
  
  
