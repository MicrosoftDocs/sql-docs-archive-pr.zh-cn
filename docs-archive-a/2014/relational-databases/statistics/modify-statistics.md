---
title: 修改统计信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6dd44da6d1a80050f37f08e49773f95af0e5a339
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590112"
---
# <a name="modify-statistics"></a>修改统计信息
  您可以通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 修改 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的现有统计信息。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要修改统计信息，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求：  
  
-   用户对表或视图具有 ALTER 权限。  
  
-   用户是表或索引视图所有者，或者是以下角色之一的成员： **sysadmin** 固定服务器角色、 **db_owner** 固定数据库角色或 **db_ddladmin** 固定数据库角色。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-statistics"></a>修改统计信息  
  
1.  在 **“对象资源管理器”** 中，单击加号以便展开要修改统计信息的数据库。  
  
2.  单击加号以便展开 **“表”** 文件夹。  
  
3.  单击加号以便展开要修改统计信息的表。  
  
4.  单击加号以便展开 **“统计信息”** 文件夹。  
  
5.  右键单击要修改的统计信息对象，然后选择“属性”。  
  
6.  在“统计信息属性 - statistics_name”对话框中的“常规”页面上，单击“添加”、“删除”、“上移”、“下移”或上述任何组合，以更改统计信息的属性     。 请记住，某一列在“统计信息列”网格内的位置可能会显著影响统计信息的有用性。  
  
7.  单击“确定”。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **修改统计信息**  
  
 无法使用 Transact-SQL 语句执行此任务。 若要使用 Transact-SQL 修改统计信息，必须首先删除现有的统计信息，然后使用新属性重新创建统计信息。  
  
 详细信息，请参阅 [DROP STATISTICS (Transact SQL)](/sql/t-sql/statements/drop-statistics-transact-sql) 和 [CREATE STATISTICS (Transact SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
  
