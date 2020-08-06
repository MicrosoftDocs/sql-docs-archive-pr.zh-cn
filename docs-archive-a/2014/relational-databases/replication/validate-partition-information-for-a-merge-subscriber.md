---
title: 验证合并订阅服务器的分区信息 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3032ff13af69a0690e1f81f08f7b3fb17aae0ee1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577499"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>验证合并订阅服务器的分区信息
  在为合并发布定义参数化行筛选器时，将使用引用订阅服务器信息（如订阅服务器的登录名）的函数。 默认情况下，每次同步前和快照应用于订阅服务器时，复制都将根据此函数验证订阅服务器信息。 验证过程确保每个订阅服务器的数据都进行了正确的分区。 验证行为由 **validate_subscriber_info** 发布属性控制，此属性可以使用 [sp_changemergepublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) 或在“发布属性”对话框的“订阅选项”页上进行更改********。 有关更改发布属性的详细信息，请参阅 [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md)。  
  
## <a name="how-partition-validation-works"></a>分区验证的工作机制  
 对发布进行筛选时（例如，使用函数 **SUSER_SNAME()**），合并代理根据对 **SUSER_SNAME()** 表达式有效的数据，将初始快照应用到每个订阅服务器。  
  
 如果验证已启用，则当订阅服务器重新连接到发布服务器进行下次同步处理时，合并代理将验证订阅服务器上的信息，并确保每个订阅服务器的分区与初始快照中所接收的相同。 针对每个后续合并或快照应用程序，合并代理将验证每个订阅服务器的分区。  
  
 如果合并代理检测到在筛选表达式中使用的函数返回了一个不同于其在初始快照中返回的值，则合并或快照应用程序将失败，而且此订阅服务器的订阅可能需要重新初始化。 可能需要重新初始化以避免出现问题（如果更改了订阅服务器的合并设置，则可能引发这些问题），不过，将订阅服务器上的信息更改回初始快照时使用的值（如登录名）可能也足以避免出现问题。  
  
 合并代理验证分区时，除了对筛选表达式使用的所有函数返回的值验证分区之外，代理还会检查快照的生成是否先于令其无效的更改，如元数据清除操作或架构更改。 如果分区快照太旧，合并代理将返回一个错误，并且必须根据当前常规快照为此订阅服务器重新生成分区快照。  
  
## <a name="see-also"></a>另请参阅  
 [复制管理常见问题解答](administration/frequently-asked-questions-for-replication-administrators.md)   
 [复制管理的最佳做法](administration/best-practices-for-replication-administration.md)   
 [重新初始化订阅](reinitialize-subscriptions.md)   
 [验证已复制的数据](validate-data-at-the-subscriber.md)  
  
  
