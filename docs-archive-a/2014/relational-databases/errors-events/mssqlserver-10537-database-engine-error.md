---
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1baccad5236bd8c1a71024b7dd542cc9d11cbd7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690638"
---
# <a name="mssqlserver_10537"></a>MSSQLSERVER_10537
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10537|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_DUP_ENABLED|  
|消息正文|无法启用计划指南 '%.*ls'，因为已启用的计划指南 '%.\*ls' 包含该语句的相同作用域和初始偏移量值。 请先禁用现有计划指南，再启用指定的计划指南。|  
  
## <a name="explanation"></a>说明  
 现有计划指南与指定计划指南中的语句包含相同的作用域和初始偏移量值。  
  
## <a name="user-action"></a>用户操作  
 请先禁用现有计划指南，再启用指定的计划指南。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
