---
title: 查看排序规则信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 995e559cfd7ca871f5abd90751f2f79167bdf76f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591388"
---
# <a name="view-collation-information"></a>查看排序规则信息
    
##  <a name="you-can-view-the-collation-of-a-server-database-or-column-in-ssmanstudiofull-using-object-explorer-menu-options-or-by-using-tsql"></a><a name="Top"></a> 您可以通过使用“对象资源管理器”菜单选项或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查看 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的服务器、数据库或列的排序规则。  
  
##  <a name="how-to-view-a-collation-setting"></a><a name="Procedures"></a> 如何查看排序规则设置  
 您可以使用以下项之一：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **使用对象资源管理器查看服务器（SQL Server 实例）的排序规则设置**  
  
1.  在“对象资源管理器”中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  右键单击该实例，然后选择“属性”  。  
  
 **使用对象资源管理器查看数据库的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  展开“数据库”  ，右键单击数据库，然后选择“属性”  。  
  
 **使用对象资源管理器查看列的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例，然后展开该实例。  
  
2.  依次展开 **“数据库”** 、数据库和 **“表”** 。  
  
3.  展开包含该列的表，然后展开 **“列”** 。  
  
4.  右键单击该列并选择“属性”  。 如果排序规则属性为空，则该列不是字符数据类型。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看服务器的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”** 。  
  
2.  在查询窗口中，输入以下使用 SERVERPROPERTY 系统函数的语句。  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  或者，您可以使用 sp_helpsort 系统存储过程。  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **查看 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”** 。  
  
2.  在查询窗口中，输入以下使用 SERVERPROPERTY 系统函数的语句。  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **查看数据库的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”** 。  
  
2.  在查询窗口中，输入以下使用 sys.databases 系统目录视图的语句。  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  或者，您可以使用 DATABASEPROPERTYEX 的系统函数。  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **查看列的排序规则设置**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例，并在工具栏中单击 **“新建查询”** 。  
  
2.  在查询窗口中，输入以下使用 sys.columns 系统目录视图的语句。  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sys.fn_helpcollations (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [sys.columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [排序规则优先级 (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [sp_helpsort (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpsort-transact-sql)  
  
  
