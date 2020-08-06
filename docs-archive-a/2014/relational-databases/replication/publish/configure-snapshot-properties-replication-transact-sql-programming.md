---
title: 配置快照属性（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c7dd645fed073f73132c6993f12925a885a8e0e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691660"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>配置快照属性（复制 Transact-SQL 编程）
  可以使用复制存储过程以编程方式定义和修改快照属性，使用的存储过程取决于发布的类型。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>在创建快照发布或事务发布时配置快照属性  
  
1.  在发布服务器上，执行 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 为指定发布名称，为指定一个 **@publication** 值， **snapshot**并为**指定** **@repl_freq** 以下一个或多个快照相关参数：  
  
    -   **@alt_snapshot_folder**-如果此发布的快照可从该位置访问，而不是在快照默认文件夹中访问，请指定路径。  
  
    -   **@compress_snapshot**-如果备用快照文件夹中的快照文件是 CAB 文件格式的压缩文件，则将值指定**为 true** [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
    -   **@pre_snapshot_script**-指定在初始快照应用之前的初始化过程中将在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **@post_snapshot_script**-指定在初始快照应用之后的初始化过程中将在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **@snapshot_in_defaultfolder**-如果快照仅在非默认位置可用，则将值指定为**false** 。  
  
     有关创建发布的详细信息，请参阅 [Create a Publication](create-a-publication.md)。  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>创建合并发布时配置快照属性  
  
1.  在发布服务器上，执行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 为指定发布名称，为指定一个 **@publication** 值， **snapshot**并为**指定** **@repl_freq** 以下一个或多个快照相关参数：  
  
    -   **@alt_snapshot_folder**-如果此发布的快照可从该位置访问，而不是在快照默认文件夹中访问，请指定路径。  
  
    -   **@compress_snapshot**-如果备用快照文件夹中的快照文件是 CAB 文件格式的压缩文件，则将值指定**为 true** 。  
  
    -   **@pre_snapshot_script**-指定在初始快照应用之前的初始化过程中将在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **@post_snapshot_script**-指定在初始快照应用之后的初始化过程中将在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **@snapshot_in_defaultfolder**-如果快照仅在非默认位置可用，则将值指定为**false** 。  
  
2.  有关创建发布的详细信息，请参阅 [Create a Publication](create-a-publication.md)。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>修改现有快照发布或事务发布的快照属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 将的值指定**1**为 1 **@force_invalidate_snapshot** ，并为指定以下值之一 **@property** ：  
  
    -   **alt_snapshot_folder** -还为的备用快照文件夹指定新路径 **@value** 。  
  
    -   **compress_snapshot** -还将值指定为**true**或**false** ， **@value** 以指示备用快照文件夹中的快照文件是否为 CAB 文件格式的压缩文件。  
  
    -   **pre_snapshot_script** -还 **@value** 可指定在初始化过程中，在应用初始快照之前，在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **post_snapshot_script** -还可 **@value** 指定在初始化初始快照后，在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **snapshot_in_defaultfolder** - 也将值指定为 **true** 或 **false** ，以指示快照是否仅在非默认位置可用。  
  
2.  （可选）在发布服务器上，对发布数据库执行 [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)。 指定 **@publication** 和要更改的一个或多个计划或安全凭据参数。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
3.  在命令提示符处运行 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 或启动快照代理作业以生成新的快照。 有关详细信息，请参阅 [创建并应用初始快照](../create-and-apply-the-initial-snapshot.md)。  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>修改现有合并发布的快照属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 将的值指定**1**为 1 **@force_invalidate_snapshot** ，并为指定以下值之一 **@property** ：  
  
    -   **alt_snapshot_folder** -还为的备用快照文件夹指定新路径 **@value** 。  
  
    -   **compress_snapshot** -还将值指定为**true**或**false** ， **@value** 以指示备用快照文件夹中的快照文件是否为 CAB 文件格式的压缩文件。  
  
    -   **pre_snapshot_script** -还 **@value** 可指定在初始化过程中，在应用初始快照之前，在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **post_snapshot_script** -还可 **@value** 指定在初始化初始快照后，在订阅服务器上执行的 **.sql**文件的文件名和完整路径。  
  
    -   **snapshot_in_defaultfolder** - 也将值指定为 **true** 或 **false** ，以指示快照是否仅在非默认位置可用。  
  
2.  在命令提示符处运行 [Replication Snapshot Agent](../agents/replication-snapshot-agent.md) 或启动快照代理作业以生成新的快照。 有关详细信息，请参阅 [创建并应用初始快照](../create-and-apply-the-initial-snapshot.md)。  
  
## <a name="example"></a>示例  
 此示例创建一个使用备用快照文件夹和压缩快照的发布。  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubaltsnapshot.sql#sp_mergealtsnapshot)]  
  
## <a name="see-also"></a>另请参阅  
 [备用快照文件夹位置](../alternate-snapshot-folder-locations.md)   
 [压缩的快照](../compressed-snapshots.md)   
 [在应用快照之前和之后执行脚本](../snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [通过 FTP 传输快照](../transfer-snapshots-through-ftp.md)   
 [更改发布和项目属性](change-publication-and-article-properties.md)  
  
  
