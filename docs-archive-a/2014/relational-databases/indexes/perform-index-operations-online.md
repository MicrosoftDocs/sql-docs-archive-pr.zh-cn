---
title: 联机执行索引操作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4d09bd99a0eaec5fdb433bd8c33351d7622957a2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590788"
---
# <a name="perform-index-operations-online"></a>联机执行索引操作
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中联机创建、重新生成或删除索引。 ONLINE 选项允许并发用户在执行这些索引操作期间访问基础表或聚集索引数据和任何关联非聚集索引。 例如，一个用户正在重新生成聚集索引时，该用户和其他用户可以继续更新和查询基础数据。 当脱机执行数据定义语言 (DDL) 操作（例如，生成或重新生成聚集索引）时，这些操作对基础数据和关联索引持有排他锁。 这样可以防止在索引操作未完成时对基础数据进行修改和查询。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各版本中均不提供联机索引操作。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要联机重新生成索引，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   建议对于全天候运行的业务环境执行联机索引操作，在这些环境中，在执行索引操作期间必须有并发用户活动。  
  
-   以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中可以使用 ONLINE 选项。  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql)  
  
    -   [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql)  
  
    -   [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) （使用 CLUSTERED 索引选项添加或删除 UNIQUE 约束或 PRIMARY KEY 约束）  
  
-   有关联机创建、重新生成或删除索引的更多限制和局限性，请参阅 [联机索引操作指南](guidelines-for-online-index-operations.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求对表或视图具有 ALTER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>联机重新生成索引  
  
1.  在“对象资源管理器”中，单击加号以便展开包含您要联机重新生成索引的表的数据库。  
  
2.  展开 **“表”** 文件夹。  
  
3.  单击加号以展开您要联机重新生成索引的表。  
  
4.  展开 **“索引”** 文件夹。  
  
5.  右键单击要联机重新生成的索引，然后选择“属性”。  
  
6.  在 **“选择页”** 下，选择 **“选项”** 。  
  
7.  选择 **“允许联机 DML 处理”** ，然后从列表中选择 **True** 。  
  
8.  单击“确定”。  
  
9. 右键单击要联机重新生成的索引，然后选择“重新生成”。  
  
10. 在 **“重新生成索引”** 对话框中，确认正确的索引位于 **“要重新生成的索引”** 网格中，然后单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-rebuild-or-drop-an-index-online"></a>联机创建、重新生成或删除索引  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例将联机重新生成现有的索引  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     以下示例使用 `NewGroup` 子句联机删除一个聚集索引并将生成表（堆）移动到文件组 `MOVE TO` 。 在移动之前和之后，将查询 `sys.indexes`、 `sys.tables`和 `sys.filegroups` 目录视图，以验证索引和表在文件组中的位置。  
  
     [!code-sql[IndexDDL#DropIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/dropindex.sql#dropindex4)]  
  
 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](/sql/t-sql/statements/alter-index-transact-sql)。  
  
  
