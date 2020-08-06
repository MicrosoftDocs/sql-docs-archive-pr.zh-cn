---
title: 查看或更改数据库的兼容级别 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- compatibility levels [SQL Server], viewing
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], changing
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35cf7af50eba333440c42a1bac428df1fff156b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693378"
---
# <a name="view-or-change-the-compatibility-level-of-a-database"></a>查看或更改数据库的兼容级别
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看或更改数据库的兼容级别。 在更改数据库的兼容级别之前，应先了解此更改对应用程序的影响。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **查看或更改数据库的兼容级别，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对数据库拥有 ALTER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-compatibility-level-of-a-database"></a>查看或更改数据库的兼容级别  
  
1.  连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的相应实例之后，在对象资源管理器中，单击服务器名称。  
  
2.  展开 **“数据库”** ，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击数据库，再单击“属性”。  
  
     **“数据库属性”** 对话框将打开。  
  
4.  在 **“选择页”** 窗格中，单击 **“选项”** 。  
  
     当前兼容级别显示在 **“兼容级别”** 列表框中。  
  
5.  若要更改兼容级别，请从列表中选择其他选项。 可用选项包括 **SQL Server 2008 (100)**、 **SQL Server 2012 (110)** 或 **SQL Server 2014 (120)**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-compatibility-level-of-a-database"></a>查看数据库的兼容级别  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例将返回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的兼容级别。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-compatibility-level-of-a-database"></a>更改数据库的兼容级别  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例更改的兼容级别 [!INCLUDE[ssSampleDBobject](../../includes/sssql14-md.md)] 。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
  
