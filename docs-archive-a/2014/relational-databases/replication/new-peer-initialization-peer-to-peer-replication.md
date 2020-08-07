---
title: 新对等方的初始化（对等复制）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 26658fdfbcf0d3d3a88bedbace4102cda6cee9c2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588983"
---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>新对等方的初始化（对等复制）
  可以使用 **“新对等方初始化”** 页指定如何初始化对等数据库。 必须先初始化 (对等方，然后才能完成此向导。 ) 对等方将手动初始化，或使用事务复制提供的**initialize with backup**功能来初始化。  (对等事务复制不支持使用快照初始化对等方。 ) 如果必须使用不同的方法初始化不同的对等方，则必须通过多次运行向导来添加对等方。  
  
## <a name="options"></a>选项  
 **指定如何初始化新的对等数据库**  
 所有已发布对象的架构和数据必须存在于每个对等方。 选择以下选项之一：  
  
-   如果已经手动为已发布的对象创建了架构，或者已经还原了备份，并且在此备份后第一个发布数据库的数据未更改，则可以选择第一个选项。 如果手动创建了架构，则必须确保每个对等方存在所有所需的数据。 此选项对应于订阅属性 **sync_type** 的 **replication support only**值。  
  
-   如果您已经还原了备份，并且在此备份后第一个发布数据库的数据发生了更改，则可以选择第二个选项。 复制必须立即传递备份中不包括的第一个发布数据库的更改。 此选项对应于订阅属性 **sync_type** 的 **initialize with backup**值。  
  
     为对等复制启用发布时，将设置 **allow_initialize_from_backup** 发布属性。 复制立即开始跟踪在第一个发布数据库中所做的更改。 因此，如果选择了 **initialize with backup** 选项，则可以将这些更改传递给一个或多个对等方上的已还原数据库。 单击 **“浏览”** 按钮以找到所使用的备份，然后复制将从该备份中读取日志序列号 (LSN)。 具有较高 LSN 的第一个发布数据库中的所有更改都将传递到每个对等方。  
  
     如果是创建或添加到包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的拓扑中，则此选项可能不可用。 下表显示了当将节点添加到现有拓扑中时此选项是否可用。  
  
    |新建节点|第一个节点|其他节点|选项|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|已禁用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|无|已禁用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|已禁用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|无|Enabled|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|无|Enabled|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|已启用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|无|Enabled|  
  
## <a name="see-also"></a>另请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
