---
title: 管理对等拓扑（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, peer-to-peer replication
ms.assetid: 4d0fa941-f9ea-4a14-aed9-34df593fc6f2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3a73af1c1f3a7196d87f77681ee9d62a3ef248a4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580160"
---
# <a name="administer-a-peer-to-peer-topology-replication-transact-sql-programming"></a>管理对等拓扑（复制 Transact-SQL 编程）
  管理对等拓扑类似于管理典型的事务复制拓扑，但有许多需要特别注意的地方。 管理对等拓扑的主要区别在于，有些更改需要让系统“停止” **。 为了停止系统，需要停止对所有节点上已发布表的操作，并确保每个节点都已收到来自所有其他节点的所有更改。 有关详细信息，请参阅[停止复制拓扑（复制 Transact-SQL 编程）](quiesce-a-replication-topology-replication-transact-sql-programming.md)。  
  
> [!NOTE]  
>  在对等拓扑中，分发服务器使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本不能低于请求订阅服务器的版本。  
  
### <a name="to-add-an-article-to-an-existing-configuration"></a>向现有配置添加项目  
  
1.  停止系统。  
  
2.  停止拓扑中每个节点上的分发代理。 有关详细信息，请参阅[复制代理可执行文件概念](../concepts/replication-agent-executables-concepts.md)或[启动和停止复制代理 (SQL Server Management Studio)](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
3.  执行 CREATE TABLE 语句，在拓扑中每个节点上添加新表。  
  
4.  通过使用 [bcp 实用工具](../../../tools/bcp-utility.md)在所有节点上以手动方式为新表大容量复制数据。  
  
5.  执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ，在拓扑中的每个节点上创建新项目。 有关详细信息，请参阅 [定义项目](../publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 之后，复制会将此项目自动添加到拓扑中的订阅。  
  
6.  重新启动拓扑中每个节点上的分发代理。  
  
### <a name="to-make-schema-changes-to-a-publication-database"></a>对发布数据库进行架构更改  
  
1.  停止系统。  
  
2.  执行数据定义语言 (DDL) 语句来修改已发布表的架构。 有关支持的架构更改的详细信息，请参阅[对发布数据库进行架构更改](../publish/make-schema-changes-on-publication-databases.md)。  
  
3.  恢复已发布表中的操作之前，请再次停止系统。 这将确保在复制任何新的数据更改前所有节点已收到架构更改。  
  
## <a name="example"></a>示例  
 以下示例演示如何将新的表项目添加到具有两个节点的现有对等复制拓扑中。  
  
 [!code-sql[HowTo#sp_addp2particle_createtables](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createtables)]  
  
 [!code-sql[HowTo#sp_addp2particle_cmdline](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_cmdline)]  
  
 [!code-sql[HowTo#sp_addp2particle_createarticle](../../../snippets/tsql/SQL15/replication/howto/tsql/addp2particle.sql#sp_addp2particle_createarticle)]  
  
## <a name="see-also"></a>另请参阅  
 [复制管理常见问题解答](frequently-asked-questions-for-replication-administrators.md)   
 [SQL Server 数据库的备份和还原](../../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [@loopback_detection](../transactional/peer-to-peer-transactional-replication.md)  
  
  
