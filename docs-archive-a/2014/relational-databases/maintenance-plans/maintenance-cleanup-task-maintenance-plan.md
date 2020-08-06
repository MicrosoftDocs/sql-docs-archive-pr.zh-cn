---
title: “清除维护”任务（维护计划）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.cleanup.f1
helpviewer_keywords:
- Maintenance Cleanup Task dialog box
ms.assetid: 022b679c-6799-4c13-9185-814224a20412
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9023881ff5cf5ba5ddd8c61aa179c5881162bf44
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587375"
---
# <a name="maintenance-cleanup-task-maintenance-plan"></a>“清除维护”任务（维护计划）
  使用 **“‘清除维护’任务”** 可以删除与维护计划相关的旧文件，包括由维护计划文件和数据库备份文件创建的文本报告。  
  
> [!NOTE]  
>  “清除维护”任务不会自动删除指定目录的子文件夹中的文件。 此功能减少了使用清除维护任务删除文件的恶意攻击的可能性。 如果要删除一级子文件夹中的文件，必须选择“包括一级子文件夹”。  
  
## <a name="options"></a>选项  
 **Connection**  
 显示当前的连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **备份文件**  
 删除备份文件。  
  
 **维护计划文本报告**  
 删除以前运行的维护计划的文本报告。  
  
 **删除特定文件**  
 删除在“文件名”框中提供的特定文件。  
  
 **文件名**  
 要删除的文件的路径和名称。  
  
 **搜索文件夹并根据扩展名删除文件**  
 删除指定文件夹中带有指定扩展名的所有文件。 使用此选项可一次删除多个文件，例如 Tuesday 文件夹中带有 .bak 扩展名的所有备份文件。  
  
 **文件夹**  
 要删除的文件所在的文件夹的路径和名称。  
  
 **文件扩展名**  
 提供要删除的文件的文件扩展名。  
  
 **包括一级子文件夹**  
 从“文件夹”下的一级子文件夹中删除具有为“文件扩展名”指定的扩展名的文件。  
  
 **在任务运行时根据文件保留时间删除文件**  
 通过在“删除文件，如果其保留时间超过”框中提供数字和时间单位，指定将要删除的文件所要保留的最短时间。  
  
 **删除文件，如果其保留时间超过**  
 通过提供数字和时间单位（天、周、月或年），指定将要删除的文件所要保留的最短时间。 保留时间长于指定时间长度的文件将被删除。  
  
 **查看 T-SQL**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **...**  
 选择以查看可用服务器的列表。  
  
 **输入登录服务器所需的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows 集成安全性**  
 使用 Microsoft Windows 身份验证连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。  
  
 **使用特定用户名和密码**  
 使用 SQL Server 身份验证连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例。 此选项不可用。  
  
 **用户名**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **密码**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [维护计划](maintenance-plans.md)  
  
  
