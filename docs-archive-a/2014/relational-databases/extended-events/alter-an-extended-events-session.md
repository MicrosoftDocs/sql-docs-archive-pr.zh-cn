---
title: 更改扩展事件会话 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 114ec05b-7eca-4c87-b276-25e37b84be39
author: rothja
ms.author: jroth
ms.openlocfilehash: 14be41e48262bc7ebc8aeeaf55185f5e35d0c72e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576767"
---
# <a name="alter-an-extended-events-session"></a>更改扩展事件会话
  在创建扩展事件会话后，可以使用 **“SQL Server 扩展事件向导”** 根据需要更改它。  
  
## <a name="before-you-begin"></a>开始之前  
 不能更改活动和不活动会话的目标，不能更改活动会话的高级属性配置。  
  
 可以对活动和不活动事件会话进行以下更改：  
  
-   在会话中添加或删除事件，更改事件配置（如事件字段、筛选器和操作）。  
  
-   添加或删除事件会话的目标。  
  
-   启用 **“在服务器启动时启动事件会话”** 选项。  
  
 可以对不活动的事件会话进行以下其他更改：  
  
-   启用 **“跟踪事件之间的关系”** 选项。  
  
-   更改高级属性配置。  
  
> [!NOTE]  
>  “SQL Server 扩展事件向导”**** 不支持事件会话修改。  
  
## <a name="how-to-alter-an-extended-events-session-using-the-sql-server-extended-events-wizard"></a>如何使用 SQL Server 扩展事件向导更改扩展事件会话  
  
-   在对象资源管理器中，依次展开 **“管理”**、 **“扩展事件”** 和 **“会话”**。  
  
-   右键单击要更改的会话，然后单击“属性”****。  
  
-   在 **“属性”** 对话框中进行相应的更改，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER EVENT SESSION &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)   
 [使用查询编辑器创建扩展事件会话](../../database-engine/create-an-extended-events-session-using-query-editor.md)  
  
  
