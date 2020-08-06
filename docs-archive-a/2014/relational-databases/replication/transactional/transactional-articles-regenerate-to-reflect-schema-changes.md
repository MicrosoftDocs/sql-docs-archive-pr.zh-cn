---
title: 重新生成自定义事务过程以反映架构更改 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b41b5309816e037ce3619e880b796e0653c7506
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692342"
---
# <a name="regenerate-custom-transactional-procedures-to-reflect-schema-changes"></a>重新生成自定义事务过程以反映架构更改
  默认情况下，事务复制通过发布中的每个表项目的内部过程生成的存储过程，在订阅服务器上进行所有数据更改。 三个过程（分别对应插入、更新和删除）将复制到订阅服务器并在插入、更新或删除复制到订阅服务器后执行。 对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布服务器上的表进行架构更改后，复制会通过调用同一组内部脚本过程自动重新生成这些过程，以便新过程与新架构相匹配（Oracle 发布服务器不支持复制架构更改）。  
  
 也可以指定自定义过程来替换一个或多个默认过程。 如果架构更改将影响过程，则应该更改自定义过程。 例如，如果一个过程引用了架构更改中删除的列，则对此列的引用应从过程中删除。 复制有两种方式将新的自定义过程传播到订阅服务器：  
  
-   第一种选择是使用自定义脚本过程替换复制使用的默认过程：  
  
    1.  在执行[&#40;transact-sql&#41;sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)时，请确保 **@schema_option** 0x02 位为**true**。  
  
    2.  执行[sp_register_custom_scripting &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql) ，并为参数指定值 "insert"、"update" 或 "delete"，并为参数指定 **@type** 自定义脚本过程的名称 **@value** 。  
  
     下次进行架构更改时，复制会调用此存储过程为新用户定义的自定义存储过程编写定义脚本，然后将此过程传播到每个订阅服务器。  
  
-   第二种选择是使用包含新自定义过程定义的脚本：  
  
    1.  当执行[sp_addarticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)时，将 **@schema_option** 0x02 位设置为**false** ，以便复制不会自动在订阅服务器上生成自定义过程。  
  
    2.  每次更改架构前，请执行 [sp_register_custom_scripting &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql) 来创建新脚本文件并注册具有复制的脚本。 将参数的值指定为 "custom_script" **@type** ，并为参数指定发布服务器上脚本的路径 **@value** 。  
  
     下次进行相关的架构更改时，此脚本会在每个订阅服务器上、在 DDL 命令所在的事务内执行。 更改架构后，此脚本将撤消注册。 在后续架构更改后必须重新注册此脚本，使其执行。  
  
## <a name="see-also"></a>另请参阅  
 [指定如何传播事务项目的更改](transactional-articles-specify-how-changes-are-propagated.md)   
 [对发布数据库进行架构更改](../publish/make-schema-changes-on-publication-databases.md)  
  
  
