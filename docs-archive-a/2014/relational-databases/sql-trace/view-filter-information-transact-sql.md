---
title: 查看筛选器信息 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8d94a7b4a73c264c1fb3a950aa1c9615a73db956
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694407"
---
# <a name="view-filter-information-transact-sql"></a><span data-ttu-id="0dee1-102">查看筛选器信息 (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="0dee1-102">View Filter Information (Transact-SQL)</span></span>
  <span data-ttu-id="0dee1-103">本主题介绍了如何使用内置函数查看跟踪筛选器信息。</span><span class="sxs-lookup"><span data-stu-id="0dee1-103">This topic describes how to use built-in functions to view trace filter information.</span></span>  
  
### <a name="to-view-filter-information"></a><span data-ttu-id="0dee1-104">查看筛选器信息</span><span class="sxs-lookup"><span data-stu-id="0dee1-104">To view filter information</span></span>  
  
1.  <span data-ttu-id="0dee1-105">通过指定所需筛选器信息的跟踪 ID，执行 **fn_trace_getfilterinfo** 。</span><span class="sxs-lookup"><span data-stu-id="0dee1-105">Execute **fn_trace_getfilterinfo** by specifying the ID of the trace about which filter information is needed.</span></span> <span data-ttu-id="0dee1-106">此函数将返回一个表，表中列出了筛选器、应用筛选器的列和应用筛选器的值。</span><span class="sxs-lookup"><span data-stu-id="0dee1-106">This function returns a table that lists the filters, the columns on which the filters are applied, and the values on which the filter is applied.</span></span>  
  
     <span data-ttu-id="0dee1-107">请按以下方式调用此函数：</span><span class="sxs-lookup"><span data-stu-id="0dee1-107">Invoke the function this way:</span></span>  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="0dee1-108">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0dee1-108">See Also</span></span>  
 <span data-ttu-id="0dee1-109">[sys.fn_trace_getfilterinfo (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="0dee1-109">[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql) </span></span>  
 <span data-ttu-id="0dee1-110">[系统存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) </span><span class="sxs-lookup"><span data-stu-id="0dee1-110">[System Stored Procedures &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql) </span></span>  
 [<span data-ttu-id="0dee1-111">SQL Server Profiler 存储过程 (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="0dee1-111">SQL Server Profiler Stored Procedures &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
