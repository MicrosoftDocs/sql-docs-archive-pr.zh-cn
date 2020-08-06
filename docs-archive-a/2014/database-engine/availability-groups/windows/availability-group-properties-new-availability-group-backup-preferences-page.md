---
title: 可用性组属性：新建可用性组 (备份首选项页面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7914d4b1d7af06bcaf4f3fd05a260138e3edf5fc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577858"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>可用性组属性：新建可用性组（“备份首选项”页）
  使用此对话框可以查看和更改所选可用性组的备份首选项。  
  
 **查看可用性组属性**  
  
-   [查看可用性组属性 (SQL Server)](view-availability-group-properties-sql-server.md)  
  
-   [使用 AlwaysOn 面板 (SQL Server Management Studio)](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>应在何处进行备份？  
 **优先辅助**  
 指定备份应在辅助副本上发生，但在主副本是唯一联机的副本时除外。 在该情况下，备份应在主副本上发生。 这是默认选项。  
  
 **仅辅助**  
 指定备份应该永远不会在主副本上执行。 如果主副本是唯一的联机副本，则备份应不会发生。  
  
 **主要节点**  
 指定备份应该始终在主副本上发生。 如果您需要在对辅助副本运行备份时不支持的备份功能，例如创建差异备份，此选项将很有用。  
  
 **任何副本**  
 指定您希望在选择要执行备份的副本时备份作业将忽略可用性副本的角色。 请注意，备份作业可能评估其他因素，例如每个可用性副本的备份优先级及其操作状态和已连接状态。  
  
> [!IMPORTANT]  
>  没有实施备份首选项设置。 对此首选项的解释依赖于您为给定可用性组中的数据库撰写作业脚本的逻辑（如果有）。 有关详细信息，请参阅[活动辅助副本：辅助副本上的备份 (AlwaysOn 可用性组) ](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。  
  
## <a name="replica-backup-priorities"></a>副本备份优先级  
 此网格将显示每个承载可用性组的副本的服务器实例的当前备份优先级。 使用此网格可以更改一个或多个可用性副本的备份优先级。  
  
 **服务器实例**  
 承载可用性副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
 **备份优先级(最低 = 1，最高 = 100)**  
 指定相对于同一可用性组中的其他副本，在此副本上执行备份的优先级。 该值是范围 0..100 中的整数。 1 表示最低优先级，100 表示最高优先级。 如果“备份优先级”****= 1，则仅在当前没有更高优先级的可用性副本可用时，才选择此可用性副本来执行备份。  
  
 **排除副本**  
 如果从不希望选择此可用性副本来执行备份，请选择此选项。 例如，这对于您永远不希望备份故障转移到的远程可用性副本十分有用。  
  
## <a name="see-also"></a>另请参阅  
 [活动辅助副本：辅助副本上的备份 (AlwaysOn 可用性组) ](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP (Transact-SQL)](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
