---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eeec3a3adf318cadc96501938f8a5565f1c07670
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577736"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10502|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_DUP_FOUND|  
|消息正文|无法创建计划指南 '%.*ls'，因为 @stmt 和 @module_or_batch 或 @plan_handle 和 @statement_start_offset 指定的语句与数据库中的现有计划指南 '%.\*ls' 相匹配。 请先删除现有计划指南，再创建新的计划指南。|  
  
## <a name="explanation"></a>说明  
 指定语句的计划指南已经存在。  
  
## <a name="user-action"></a>用户操作  
 请先删除现有计划指南，再创建新的计划指南。  
  
## <a name="see-also"></a>另请参阅  
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
