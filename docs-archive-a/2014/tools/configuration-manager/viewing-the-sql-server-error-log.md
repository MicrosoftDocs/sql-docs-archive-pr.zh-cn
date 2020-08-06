---
title: 查看 SQL Server 错误日志 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cycling SQL Server error log
- viewing SQL Server error log
- errors [SQL Server], logs
- SQL Server error log
- displaying SQL Server error log
- logs [SQL Server], SQL Server error logs
ms.assetid: 6908c21a-65e3-458f-a272-fee256d86448
author: stevestein
ms.author: sstein
ms.openlocfilehash: 822ae4fba589f005aaee41857a9db3388a309254
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576466"
---
# <a name="viewing-the-sql-server-error-log"></a>查看 SQL Server 错误日志
  查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志可以确保进程（例如，备份和还原操作、批处理命令或其他脚本和进程）成功完成。 此功能可用于帮助检测任何当前或潜在的问题领域，包括自动恢复消息（尤其是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例已停止并重新启动时）、内核消息或其他服务器级错误消息。  
  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或任何文本编辑器可以查看 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 错误日志。 有关如何查看错误日志的详细信息，请参阅 [Open Log File Viewer](../../relational-databases/logs/log-file-viewer.md)。 默认情况下，错误日志位于 `Program Files\Microsoft SQL Server\MSSQL.`*n*`\MSSQL\LOG\ERRORLOG` 和 `ERRORLOG.`*n* 文件中。  
  
 每当启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，将创建新的错误日志，虽然 [sp_cycle_errorlog](/sql/relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql) 系统存储过程可用于循环使用错误日志文件，而不必重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 通常， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保留前六个日志的备份，并指定最近日志备份的扩展名为 .1、下一个最近日志备份的扩展名为 .2，依次类推。 当前的错误日志没有扩展名。  
  
 请注意，您还可以查看脱机或无法启动的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。 有关详细信息，请参阅 [查看脱机日志文件](../../relational-databases/logs/view-offline-log-files.md)。  
  
  
