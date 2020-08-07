---
title: 创建数据库（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 617b3fe10a17ae2d8659b51e85cdb3fed4470506
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588635"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>创建数据库（SQL Server 导入和导出向导）
  使用 "**创建数据库**" 页可以为目标文件定义一个新数据库。  
  
 此页提供了一部分可用于创建新数据库的选项。 若要查看所有选项，请使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
 若要了解有关此向导的详细信息，请参阅[SQL Server 导入和导出向导](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要了解启动向导的选项以及成功运行向导所需的权限，请参阅[运行 SQL Server 导入和导出向导](start-the-sql-server-import-and-export-wizard.md)。  
  
 SQL Server 导入和导出向导的作用是将数据从源复制到目标。 该向导还可以为您创建目标数据库和目标表。 但是，如果必须复制多个数据库或表，或者必须复制其他类型的数据库对象，则应改用复制数据库向导。 有关详细信息，请参阅 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>选项  
 **名称**  
 为目标 SQL Server 数据库提供唯一的名称。 请确保对此数据库命名时遵循 SQL Server 约定。  
  
 **数据文件名**  
 查看数据文件的名称。 它是由以前提供的数据库名称派生而来的。  
  
 **日志文件名**  
 查看日志文件的名称。 它是由以前提供的数据库名称派生而来的。  
  
 **初始大小（数据文件）**  
 指定数据文件的初始大小 (MB)。  
  
 **不允许增长（数据文件）**  
 指示数据文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比（数据文件）**  
 指定数据文件可以增长的百分比。  
  
 **增长规模（数据文件）**  
 指定数据文件可以增长的大小 (MB)。  
  
 **初始大小（日志文件）**  
 指定日志文件的初始大小 (MB)。  
  
 **不允许增长（日志文件）**  
 指示日志文件是否可以增长以超出指定的初始大小。  
  
 **增长百分比（日志文件）**  
 指定日志文件可以增长的百分比。  
  
 **增长规模（日志文件）**  
 指定日志文件可以增长的大小 (MB)。  
  
  
