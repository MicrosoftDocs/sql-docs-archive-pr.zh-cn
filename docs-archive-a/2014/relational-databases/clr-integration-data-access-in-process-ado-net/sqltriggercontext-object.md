---
title: SqlTriggerContext 对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
ms.openlocfilehash: f7eae3d290a70bedee0ed9badf9e6d0503caa2bc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693993"
---
# <a name="sqltriggercontext-object"></a><span data-ttu-id="8ede0-102">SqlTriggerContext 对象</span><span class="sxs-lookup"><span data-stu-id="8ede0-102">SqlTriggerContext Object</span></span>
  <span data-ttu-id="8ede0-103">`SqlTriggerContext` 类提供有关触发器的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="8ede0-103">The `SqlTriggerContext` class provides context information about the trigger.</span></span> <span data-ttu-id="8ede0-104">该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是数据定义语言 (DDL) 触发器，则还包括描述触发操作的 XML `EventData` 结构。</span><span class="sxs-lookup"><span data-stu-id="8ede0-104">This contextual information includes the type of action that caused the trigger to fire, which columns were modified in an UPDATE operation, and, in the case of a data definition language (DDL) trigger, an XML `EventData` structure that describes the triggering operation.</span></span> <span data-ttu-id="8ede0-105">有关如何使用类的详细信息和示例 `SqlTriggerContext` ，请参阅[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。</span><span class="sxs-lookup"><span data-stu-id="8ede0-105">For more information and examples of how to use the `SqlTriggerContext` class, see [CLR Triggers](../../database-engine/dev-guide/clr-triggers.md).</span></span>  
  
 <span data-ttu-id="8ede0-106">有关详细信息，请参阅 `Microsoft.SqlServer.Server.SqlTriggerContext` .NET FRAMEWORK SDK 文档中的类参考文档。</span><span class="sxs-lookup"><span data-stu-id="8ede0-106">For more information, see the `Microsoft.SqlServer.Server.SqlTriggerContext` class reference documentation in the .NET Framework SDK documentation.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8ede0-107">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8ede0-107">See Also</span></span>  
 <span data-ttu-id="8ede0-108">[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md) </span><span class="sxs-lookup"><span data-stu-id="8ede0-108">[CLR Triggers](../../database-engine/dev-guide/clr-triggers.md) </span></span>  
 [<span data-ttu-id="8ede0-109">EVENTDATA (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="8ede0-109">EVENTDATA &#40;Transact-SQL&#41;</span></span>](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
