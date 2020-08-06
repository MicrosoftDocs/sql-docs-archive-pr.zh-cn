---
title: 基于事件结束时间筛选事件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event end times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 74628f9e-2d39-496a-a443-0a3887db223d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d25d8e1adbd95f48d88fd1516c48dcc0f8374a7c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693583"
---
# <a name="filter-events-based-on-the-event-end-time-sql-server-profiler"></a>基于事件结束时间筛选事件 (SQL Server Profiler)
  本主题介绍了如何通过使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]来根据事件结束时间筛选跟踪事件。  
  
### <a name="to-filter-events-based-on-the-event-end-time"></a>根据事件结束时间筛选事件  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”** ，再连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”  ，则不会显示“跟踪属性”  对话框，而是开始跟踪。 若要关闭此设置，请在“工具”  菜单上，单击“选项”  ，然后清除“建立连接后立即开始跟踪”  复选框。  
  
2.  在 **“跟踪属性”** 对话框中，确保选中 **“常规”** 选项卡，然后在 **TraceName** 文本框中输入名称。  
  
3.  从“使用模板”  列表中选择一个跟踪模板。  
  
4.  根据需要，指定保存跟踪结果的目标文件或表。  
  
5.  在“事件选择”  选项卡上，单击“EndTime”  数据列启动“编辑筛选器”  对话框。 也可以右键单击列标题，然后选择“编辑列筛选器”  。  
  
6.  展开 "**大于**" 或 "**小于**"，然后在 `datetime` 比较运算符下显示的字段中输入一个值。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 事件探查器](sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
