---
title: 设置跟踪表的最大表大小 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- size [SQL Server], trace tables
- maximum table size for traces
ms.assetid: d0ae83e5-1c88-4a2e-be05-2c341280b978
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f48efbe02e300e06faf857ed0fb36ae340ad979
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682489"
---
# <a name="set-a-maximum-table-size-for-a-trace-table-sql-server-profiler"></a>设置跟踪表的最大表大小 (SQL Server Profiler)
  本主题说明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]设置跟踪表的最大表大小。  
  
### <a name="to-set-a-maximum-table-size-for-a-trace-table"></a>设置跟踪表的最大表大小  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”** ，再连接到 SQL Server 实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”  ，则不会显示“跟踪属性”  对话框，而是开始跟踪。 若要关闭此设置，请在“工具”  菜单上，单击“选项”  ，然后清除“建立连接后立即开始跟踪”  复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称。  
  
3.  在“模板名称”  列表中，选择跟踪模板。  
  
4.  选中“保存到表”  复选框。  
  
5.  连接到要存储跟踪的服务器。  
  
     将显示 **“目标表”** 对话框。  
  
6.  从 **“数据库”** 列表中，为跟踪选择数据库。  
  
7.  在 **“表”** 框中，键入或选择表名。  
  
8.  选中 **“设置最大行数”** 复选框，然后指定跟踪表的最大行数。  
  
    > [!NOTE]  
    >  表中的行数超过指定的最大值时，将不再记录跟踪事件。 但是，仍继续跟踪。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
