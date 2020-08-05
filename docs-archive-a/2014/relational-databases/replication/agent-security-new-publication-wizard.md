---
title: 代理安全性（新建发布向导）| Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.agentsecurity.articles.f1
ms.assetid: 05ae44df-8e9f-46ea-95f6-972ad109c6c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a0da30cb49a73024ca83d8587a4f6477d21c49c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580156"
---
# <a name="agent-security-new-publication-wizard"></a>代理安全性（新建发布向导）
  可以使用 **“代理安全性”** 页指定运行以下代理的帐户，以及连接到复制拓扑中的计算机：  
  
-   所有发布的快照代理。  
  
-   所有事务发布的日志读取器代理。  
  
-   允许可更新订阅的事务发布的队列读取器代理。 如果你在“发布类型”页上指定了“具有可更新订阅的事务发布”，那么不管使用何种类型的可更新订阅，都将为此代理创建 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理作业 。 有关可更新订阅的详细信息，请参阅 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
 有关代理要求的权限及复制安全的最佳实践的信息，请参阅 [Replication Agent Security Model](security/replication-agent-security-model.md) 和 [Replication Security Best Practices](security/replication-security-best-practices.md)。  
  
## <a name="options"></a>选项  
 **快照代理**  
 所有发布都将显示此选项。 单击 **“安全设置”** ，可以指定 **“快照代理安全性”** 对话框中的安全设置。  
  
 单击 **“快照代理安全性”** 对话框中的 **“帮助”** ，可以获得快照代理使用的帐户所需权限的详细信息。  
  
 **日志读取器代理**  
 所有事务发布都将显示此选项。 单击 **“安全设置”** ，可以指定 **“日志读取器代理安全性”** 对话框中的安全设置。  
  
 单击 **“日志读取器代理安全性”** 对话框中的 **“帮助”** ，可以获得日志读取器代理使用的帐户所需权限的详细信息。  
  
> [!NOTE]  
>  对于使用事务复制发布的每个数据库，都有一个日志读取器代理。 如果数据库中已经存在事务发布，则安全设置是只读的。 您可以更改 **“发布属性”** 对话框中的设置，但是此更改会影响数据库中的所有事务发布。  
  
 **队列读取器代理**  
 允许可更新订阅的事务发布都将显示此选项。 单击 **“安全设置”** ，可以指定 **“队列读取器代理安全性”** 对话框中的安全设置。 此向导完成时将创建队列读取器代理作业；而不会取决于您创建的任意排队更新订阅。 如果您不打算创建任何排队更新订阅，那么可以禁用该作业。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的“作业”文件夹中右键单击该作业（命名格式为 [\<Publisher>].\<integer>），然后单击“禁用” 。  
  
 单击 **“队列读取器代理安全性”** 对话框中的 **“帮助”** ，可以获得队列读取器代理使用的帐户所需权限的详细信息。  
  
> [!NOTE]  
>  每个分发数据库（及其所有发布服务器）都具有一个队列读取器代理。 如果使用给定分发数据库的任意发布服务器中已存在允许排队更新订阅的事务发布，则安全设置是只读的。 可以在 **“分发服务器属性”** 对话框中更改运行队列读取器代理并建立连接的帐户，但是此更改会影响使用分发数据库的所有发布服务器中的发布。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Publication](publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   
 [查看和修改发布属性](publish/view-and-modify-publication-properties.md)   
 [管理复制中的登录名和密码](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [发布数据和数据库对象](publish/publish-data-and-database-objects.md)   
 [复制代理概述](agents/replication-agents-overview.md)  
  
  
