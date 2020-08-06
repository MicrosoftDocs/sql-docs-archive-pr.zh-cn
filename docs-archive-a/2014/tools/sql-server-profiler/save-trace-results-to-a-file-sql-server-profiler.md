---
title: 将跟踪结果保存到文件 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: ac528747-0c19-4f3d-96f5-44c762a4abed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9644751cda3689cf7b7cb00ec25310bc700ca1c5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692019"
---
# <a name="save-trace-results-to-a-file-sql-server-profiler"></a>将跟踪结果保存到文件 (SQL Server Profiler)
  本主题说明如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]将跟踪结果保存到文件。  
  
### <a name="to-save-trace-results-to-a-file"></a>将跟踪结果保存到文件  
  
1.  在 **“文件”** 菜单上，单击 **“新建跟踪”** ，再连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
     将出现“跟踪属性”对话框。 **“跟踪属性”** 对话框。  
  
    > [!NOTE]  
    >  如果选择“建立连接后立即开始跟踪”，则不会显示“跟踪属性”对话框，而是开始跟踪。 若要关闭此设置，请在“工具”菜单上，单击“选项”，然后清除“建立连接后立即开始跟踪”复选框。  
  
2.  在 **“跟踪名称”** 框中，键入跟踪的名称。  
  
3.  选中 **“保存到文件”** 复选框。  
  
     将显示“另存为”对话框。  
  
4.  在“另存为”对话框中指定路径和文件名。 单击“保存”。  
  
    > [!NOTE]  
    >  请确保 SQL Server 服务有足够的权限写入到指定目录的文件中。  
  
5.  在“跟踪属性”对话框的“设置最大文件大小 (MB)”文本框中，输入最大文件大小。 默认值为 5 MB。  
  
6.  还可以指定下列选项：  
  
    -   选中 **“启用文件滚动更新”** 复选框，在达到最大文件大小后，使 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 立即创建新文件来存储跟踪数据。 默认情况下选择此选项。  
  
    -   选中 **“服务器处理跟踪数据”** 复选框以确保服务器记录每个跟踪事件。  
  
        > [!NOTE]  
        >  清除“服务器处理跟踪数据”后，如果记录事件会显著降低性能，则服务器不会记录事件。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
