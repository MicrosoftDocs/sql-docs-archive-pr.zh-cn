---
title: 停止跟踪 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], stopping
- stopping traces
ms.assetid: 47c4f33d-63e0-4444-bec8-4c1c91f8e25c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 501ea4a4838f8e2ea42fc475c486466d48020a4c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690944"
---
# <a name="stop-a-trace-sql-server-profiler"></a>停止跟踪 (SQL Server Profiler)
  本主题介绍如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]停止正在运行的跟踪。  
  
 停止跟踪将停止捕获数据。 停止跟踪后，除非已将数据捕获到了跟踪文件或跟踪表中，否则重新启动该跟踪将丢失以前捕获的数据。 您还可以在停止跟踪后将收集的数据保存到表或文件。 当停止跟踪时，以前选择的所有跟踪属性将保留， 您也可以更改名称、事件、列和筛选器。  
  
### <a name="to-stop-a-trace"></a>停止跟踪  
  
1.  选择正在运行的跟踪。  
  
2.  在 **“文件”** 菜单上，单击 **“停止跟踪”** 。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
