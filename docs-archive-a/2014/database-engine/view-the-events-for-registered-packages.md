---
title: 查看已注册包的事件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- viewing events
- extended events [SQL Server], viewing events
ms.assetid: 9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5e3665a695bd3f40407a8680872c9b0dc79fbc53
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591509"
---
# <a name="view-the-events-for-registered-packages"></a>查看已注册包的事件
  创建 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 扩展事件会话之前，找到注册包中可用的事件非常有用。 有关详细信息，请参阅 [SQL Server Extended Events Packages](../relational-databases/extended-events/sql-server-extended-events-packages.md)。  
  
 若要完成此任务，需使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查询编辑器执行以下过程。  
  
 此过程中的语句完成后，查询编辑器的 **“结果”** 选项卡将显示以下列：  
  
-   名称。 包名称。  
  
-   事件。 事件名称。  
  
-   关键字 从内部数值映射表派生的关键字。  
  
-   渠道。 事件的用户。  
  
-   说明。 事件说明。  
  
## <a name="to-view-the-events-for-registered-packages-using-query-editor"></a>使用查询编辑器查看已注册包的事件  
  
-   在查询编辑器中发出以下语句：  
  
    ```  
    USE msdb  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
    (  
    SELECT event_package=o.package_guid, o.description,   
    event=c.object_name, channel=v.map_value  
    FROM sys.dm_xe_objects o  
    LEFT JOIN sys.dm_xe_object_columns c ON o.name=c.object_name  
    INNER JOIN sys.dm_xe_map_values v ON c.type_name=v.name   
    AND c.column_value=cast(v.map_key AS nvarchar)  
    WHERE object_type='event' AND (c.name='CHANNEL' or c.name IS NULL)  
  
    ) c LEFT JOIN   
    (  
    SELECT event_package=c.object_package_guid, event=c.object_name,   
    keyword=v.map_value  
    FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
    ON c.type_name=v.name AND c.column_value=v.map_key   
    AND c.type_package_guid=v.object_package_guid  
    INNER JOIN sys.dm_xe_objects o ON o.name=c.object_name   
    AND o.package_guid=c.object_package_guid  
    WHERE object_type='event' AND c.name='KEYWORD'   
    ) k  
    ON  
    k.event_package=c.event_package AND (k.event=c.event or k.event IS NULL)  
    INNER JOIN sys.dm_xe_packages p ON p.guid=c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 扩展事件包](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [sys.dm_xe_objects (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
