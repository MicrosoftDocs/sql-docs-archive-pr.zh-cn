---
title: 订阅过期和停用 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d81e8b5c02fcfe5399be9e63c8160036a999547
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693234"
---
# <a name="subscription-expiration-and-deactivation"></a>订阅过期和停用
  如果在指定的“保持期”  内未同步订阅，订阅可能会停用或过期。 发生什么操作取决于复制的类型和所超过的保持期。  
  
 若要设置保持期，请参阅[设置订阅的过期期限](publish/set-the-expiration-period-for-subscriptions.md)、[设置事务发布的分发保持期 &#40;SQL Server Management Studio&#41;](set-distribution-retention-period-for-transactional-publications.md) 以及[配置发布和分发](configure-publishing-and-distribution.md)。  
  
## <a name="transactional-replication"></a>事务复制  
 事务复制使用最大的分发保持期 (**@max_distretention** [Sp_adddistributiondb &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)) 的参数和发布保持期 (sp_addpublication **@retention** [transact-sql &#40;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)&#41;的参数) ：  
  
-   如果订阅未能在最大分发保持期（默认为 72 小时）内同步，而且分发数据库中还存在尚未传递到订阅服务器的更改，则订阅将会被分发服务器上运行的 **“清除分发”** 作业标记为停用。 必须重新初始化订阅。  
  
-   如果订阅未能在发布保持期（默认为 336 小时）内同步，订阅便会过期，而被发布服务器上运行的 **“过期的订阅清除”** 作业删除。 必须重新创建和同步订阅。  
  
     如果推送订阅过期，则会彻底删除该订阅，但是请求订阅则不同。 您必须清除订阅服务器上的请求订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](delete-a-pull-subscription.md)。  
  
## <a name="merge-replication"></a>合并复制  
 合并复制使用发布保持期 (**@retention** **@retention_period_unit** [&#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)) 的 sp_addmergepublication 和参数。 订阅过期后必须将其重新初始化，因为订阅的元数据已被删除。 未重新初始化的订阅将由运行在发布服务器上的 **“过期的订阅清除”** 作业删除。 默认情况下，此作业每天运行；它删除在两倍的发布保持期内尚未同步的所有推送订阅。 例如：  
  
-   如果某发布的保持期为 14 天，则订阅如果在 14 天内尚未同步就会过期。  
  
     如果发布服务器运行的是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本，并且订阅的代理来自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本，则仅当对该订阅分区中的数据进行更改时，该订阅才会过期。 例如，假定订阅服务器仅接收德国客户的客户数据。 如果将保持期设置为 14 天，则只有在最近 14 天内更改了德国客户的数据时，该订阅才会在第 14 天过期。  
  
-   在上次同步后的第 14 天到第 27 天，可以重新初始化该订阅。  
  
-   在上次同步后的第 28 天，该订阅由 **“过期的订阅清除”** 作业删除。 如果推送订阅过期，则会彻底删除该订阅，但是请求订阅则不同。 您必须清除订阅服务器上的请求订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](delete-a-pull-subscription.md)。  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>设置合并发布的发布保持期时的注意事项  
 在设置合并发布的保持期时，请谨记下列注意事项：  
  
-   合并发布的保持期具有 24 小时的宽限期，以适应处于不同时区中的订阅服务器。 例如，如果将保持期设置为 1 天，则实际的保持期为 48 小时。  
  
-   合并复制元数据的清除取决于发布保持期：  
  
    -   在到达保持期之前，复制无法清除发布数据库和订阅数据库中的元数据。 在为保持期指定较大值时务必谨慎，因为这可能对复制性能产生负面影响。 如果能很有把握地预测出所有订阅服务器都将在该时间段内定期同步，则建议使用较低的设置。  
  
    -   可以指定订阅永不过期 (值为 0 **@retention**) ，但强烈建议您不要使用此值，因为不能清除元数据。  
  
-   任何重新发布服务器的保持期都必须设置为等于或小于在原始发布服务器上设置的保持期。 对于所有发布服务器和它们的备用同步伙伴，应该使用相同的发布保持期。 使用不同的值可能会导致无法收敛。 如果需要更改发布保持期的值，请重新初始化订阅服务器，以免数据无法收敛。  
  
-   如果在清除之后增大发布保持期，而且订阅尝试与发布服务器（已删除元数据）合并，则订阅将由于增大了保持期值而不会过期。 但是，发布服务器没有足够的元数据来下载对订阅服务器所做的更改，这会导致无法收敛。  
  
## <a name="see-also"></a>另请参阅  
 [重新初始化订阅](reinitialize-subscriptions.md)   
 [复制代理管理](agents/replication-agent-administration.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
