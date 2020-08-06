---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e20018c0fe1cd0748f4930e0022622adcbfad10
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586685"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|833|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|BUF_LONG_IO|  
|消息正文|SQL Server 在数据库中的文件 [% ls] 上遇到超过% d 秒的 i/o 请求) 出现% d 次 (。 `[%ls] (%d)`  OS 文件句柄是 0x%p。  最新的长时间 I/O 操作的偏移量是: %#016I64x。|  
  
## <a name="explanation"></a>说明  
 该消息指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已从磁盘发出读取或写入请求，并且表明该请求返回所用的时间已超过 15 秒。 该错误由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 报告，表明 IO 子系统有问题。  
  
### <a name="possible-causes"></a>可能的原因  
 这种问题可能是由于系统性能问题、硬件错误、固件错误、设备驱动程序问题或 IO 进程中的筛选器驱动程序干预引起的。  
  
## <a name="user-action"></a>用户操作  
 通过检查系统事件日志获得硬件相关错误消息来纠正引错误。 并且，如果有特定于硬件的日志，也要进行检查。  
  
 使用性能监视器检查以下计数器：  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
 例如，运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的 **Average Disk Sec/Transfer** 时间通常少于 15 毫秒。 如果 **Average Disk Sec/Transfer** 值增加，这表明 I/O 子系统未能完全满足 I/O 需求。  
  
> [!NOTE]  
>  防病毒程序可能会减慢磁盘访问速度。 若要提高访问速度，请将错误消息中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据文件从实时病毒扫描中排除。  
  
 有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))以及 [https://support.microsoft.com/kb/897284](https://support.microsoft.com/kb/897284) 上的知识库文章。  
  
  
