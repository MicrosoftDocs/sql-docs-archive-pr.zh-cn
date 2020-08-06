---
title: 删除日志传送 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 14fdc36c66073e89dcc2014aed4319a2ce78a98f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586946"
---
# <a name="remove-log-shipping-sql-server"></a>删除日志传送 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除日志传送。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [安全性](#Security)  
  
-   **若要删除日志传送，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 日志传送存储过程要求 **sysadmin** 固定服务器角色中的成员身份。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-log-shipping"></a>删除日志传送  
  
1.  连接到当前是日志传送主服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并展开该实例。  
  
2.  展开“数据库”，右键单击日志传送主数据库，再单击“属性”。  
  
3.  在 **“选择页”** 下，单击 **“事务日志传送”** 。  
  
4.  清除 **“将此数据库启用为日志传送配置中的主数据库”** 复选框。  
  
5.  单击 **“确定”** ，从此主数据库中删除日志传送。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-log-shipping"></a>删除日志传送  
  
1.  在日志传送主服务器上，执行 [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) 从主服务器上删除有关辅助数据库的信息。  
  
2.  在日志传送辅助服务器上，执行 [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) 以删除辅助数据库。  
  
    > [!NOTE]  
    >  如果不存在具有相同辅助 ID 的其他辅助数据库，则从 **sp_delete_log_shipping_secondary_database** 调用 **sp_delete_log_shipping_secondary_primary** ，以删除该辅助 ID 的项并删除复制和还原作业。  
  
3.  在日志传送主服务器上，执行 **sp_delete_log_shipping_primary_database** 以删除有关主服务器的日志传送配置的信息。 此操作还将删除备份作业。  
  
4.  在日志传送主服务器上，禁用备份作业。 有关详细信息，请参阅 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)。  
  
5.  在日志传送辅助服务器上，禁用复制和还原作业。  
  
6.  或者，如果您不再使用日志传送辅助数据库，则可以从辅助服务器中删除它。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [将日志传送升级到 SQL Server 2014 &#40;Transact-sql&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [配置日志传送 (SQL Server)](configure-log-shipping-sql-server.md)  
  
-   [向日志传送配置添加辅助数据库 (SQL Server)](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [从日志传送配置中删除辅助数据库 (SQL Server)](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [监视日志传送 (Transact-SQL)](monitor-log-shipping-transact-sql.md)  
  
-   [故障转移到日志传送辅助服务器 (SQL Server)](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](about-log-shipping-sql-server.md)   
 [日志传送表和存储过程](log-shipping-tables-and-stored-procedures.md)  
  
  
