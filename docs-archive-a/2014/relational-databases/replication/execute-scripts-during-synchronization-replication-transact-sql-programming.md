---
title: 在同步期间执行脚本（复制 Transact-SQL 编程）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4bc217ad160a0238cc4247600d65eb32f156071f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578094"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a><span data-ttu-id="dd846-102">在同步期间执行脚本（复制 Transact-SQL 编程）</span><span class="sxs-lookup"><span data-stu-id="dd846-102">Execute Scripts During Synchronization (Replication Transact-SQL Programming)</span></span>
  <span data-ttu-id="dd846-103">复制支持事务发布和合并发布的订阅服务器的按需脚本执行。</span><span class="sxs-lookup"><span data-stu-id="dd846-103">Replication supports on demand script execution for Subscribers to transactional and merge publications.</span></span> <span data-ttu-id="dd846-104">此功能可将脚本复制到复制工作目录，然后使用 **sqlcmd** 将脚本应用到订阅服务器。</span><span class="sxs-lookup"><span data-stu-id="dd846-104">This functionality copies the script to the replication working directory and then uses **sqlcmd** to apply the script at the Subscriber.</span></span> <span data-ttu-id="dd846-105">默认情况下，如果在对事务发布的订阅应用脚本时发生故障，分发代理将停止。</span><span class="sxs-lookup"><span data-stu-id="dd846-105">By default, if there is a failure when applying the script for a subscription to a transactional publication, the Distribution Agent will stop.</span></span> <span data-ttu-id="dd846-106">您可以使用复制存储过程以编程的方式指定要执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。</span><span class="sxs-lookup"><span data-stu-id="dd846-106">You can specify a [!INCLUDE[tsql](../../includes/tsql-md.md)] script to execute programmatically using replication stored procedures.</span></span>  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a><span data-ttu-id="dd846-107">为快照发布、事务发布或合并发布的所有订阅服务器指定要运行的脚本</span><span class="sxs-lookup"><span data-stu-id="dd846-107">To specify a script to run for all Subscribers to a snapshot, transactional or merge publication</span></span>  
  
1.  <span data-ttu-id="dd846-108">编写并测试将按需执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本。</span><span class="sxs-lookup"><span data-stu-id="dd846-108">Compose and test the [!INCLUDE[tsql](../../includes/tsql-md.md)] script that will be executed on demand.</span></span>  
  
2.  <span data-ttu-id="dd846-109">将此脚本文件保存到此发布的快照代理能访问的位置。</span><span class="sxs-lookup"><span data-stu-id="dd846-109">Save the script file to a location where it can be accessed by the Snapshot Agent for the publication.</span></span>  
  
3.  <span data-ttu-id="dd846-110">在发布服务器上，对发布数据库执行 [sp_addscriptexec (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="dd846-110">At the Publisher on the publication database, execute [sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql).</span></span> <span data-ttu-id="dd846-111">指定\*\* \@ 发布**、在步骤2中为** \@ SCRIPTFILE**创建的具有完整 UNC 路径的脚本文件的名称，并为** \@ skiperror\*\*指定以下值之一：</span><span class="sxs-lookup"><span data-stu-id="dd846-111">Specify **\@publication**, the name of the script file with full UNC path created in step 2 for **\@scriptfile**, and one of the following values for **\@skiperror**:</span></span>  
  
    -   <span data-ttu-id="dd846-112">**0** - 如果遇到错误，代理将停止执行脚本。</span><span class="sxs-lookup"><span data-stu-id="dd846-112">**0** - the agent will stop executing the script if an error is encountered.</span></span>  
  
    -   <span data-ttu-id="dd846-113">**1** - 遇到错误时，代理将记录错误并继续执行脚本。</span><span class="sxs-lookup"><span data-stu-id="dd846-113">**1** - the agent will log errors and continue executing the script when errors are encountered.</span></span>  
  
4.  <span data-ttu-id="dd846-114">在代理下次运行以同步订阅时，指定的脚本将在每个订阅服务器上执行。</span><span class="sxs-lookup"><span data-stu-id="dd846-114">The specified script will be executed at each Subscriber when the agent next runs to synchronize the subscription.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dd846-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="dd846-115">See Also</span></span>  
 [<span data-ttu-id="dd846-116">同步数据</span><span class="sxs-lookup"><span data-stu-id="dd846-116">Synchronize Data</span></span>](synchronize-data.md)  
  
  
