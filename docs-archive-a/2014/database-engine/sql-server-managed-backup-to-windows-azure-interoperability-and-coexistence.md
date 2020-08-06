---
title: SQL Server 托管备份到 Azure：互操作性和共存 |Microsoft Docs
description: 本文介绍 SQL Server 2014 中的多项功能 Microsoft Azure 互操作性和共存 SQL Server 托管备份。
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2e2839fc4755fe47504e42e5058a5da117888900
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690020"
---
# <a name="sql-server-managed-backup-to-azure-interoperability-and-coexistence"></a>SQL Server 托管备份到 Azure：互操作性和共存
  本主题介绍[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]与 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中若干功能的互操作性和共存情况。 这些功能包括以下各项：AlwaysOn 可用性组、数据库镜像、备份维护计划、日志传送、即席备份、分离数据库和删除数据库。  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn 可用性组  
 配置为支持 Azure 的解决方案的 AlwaysOn 可用性组 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 不支持仅本地或混合 AlwaysOn 可用性组配置。 有关详细信息和其他注意事项，请参阅为[可用性组设置 SQL Server 托管备份到 Azure](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>数据库镜像  
 仅主体数据库上支持[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 如果将主体数据库和镜像数据库都配置为使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，则跳过镜像数据库，不进行备份。 但是，在故障转移的情况下，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]将在镜像完成角色切换并联机后开始备份过程。 在这种情况下，备份将存储在新的容器中。 如果未将镜像配置为使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，则在进行故障转移的情况下，不进行任何备份。 建议同时在主体和镜像上配置[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，以便在进行故障转移的情况下可继续备份。  
  
> [!TIP]  
>  如果要在具有[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]默认设置的实例上创建镜像数据库，则最好禁用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]实例默认值，以使这些设置不应用于镜像数据库，然后在配置主体和镜像后重新启用实例默认值。  
  
### <a name="maintenance-plan"></a>维护计划  
 在不支持启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]时，可使用维护计划来创建备份。 此时，维护计划将导致日志链中断，而 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 可能无法支持在还原过程中保证数据库得以恢复。 在实例级别启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]后，也适用这一规则。  
  
> [!TIP]  
>  为同一数据库或实例配置 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 后，支持具有仅复制备份的维护计划。  
  
### <a name="log-shipping"></a>日志传送  
 无法为同一数据库同时配置日志传送和 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 这样做会影响使用任一功能时数据库可复原性。  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>使用 Transact-SQL 和 SQL Server Management Studio 的即席备份  
 即席备份或一次性备份是在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]外部使用 Transact-SQL 或 SQL Server Management Studio 创建的。根据它所使用的备份类型和存储介质，它可能会影响[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]进程。 将备份记录到与使用的 Azure 存储帐户不同的 Azure 存储帐户 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，或者将其与 Azure Blob 存储服务的任何其他目标相比，将导致日志链中断。 建议使用[smart_admin。 sp_backup_on_demand &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)存储过程在已启用的数据库上启动备份 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 。 可使用此存储过程启动完整数据库备份或日志备份。  
  
### <a name="drop-database-and-detach-database"></a>删除数据库和分离数据库  
 如果分离或删除了启用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的数据库，虽然无法进行其他备份，但先前的备份仍保留在存储中，直到保持期结束，之后将清除这些备份。  
  
### <a name="changes-to-recovery-model"></a>对恢复模式的更改  
  
-   如果将数据库的恢复模式从 "**简单**" 更改为 "**完整**" 或 "**大容量日志**"，则可以选择 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 为数据库配置。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]会将数据库视为新的数据库。  
  
-   如果将数据库的恢复模式从**完整**或**大容量日志**更改为**简单**，则已 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 启用，将不再计划备份操作。 保持期设置仍将有效，并且备份文件仍将保留在存储帐户中，直到保持期结束。 如果要保留备份，则我们建议将文件下载到其他存储帐户或本地位置。 如果恢复模式恢复为**完全**或**大容量日志记录**，则会保留配置设置，并可重复使用这些设置。  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>使用其他备份工具或自定义脚本进行日志备份  
 配置为对同一数据库执行日志备份的任何两个备份都将导致备份日志链中断。 尽管 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 将尝试通过在检测到备份链中断时安排完整备份而补救备份链中断的情况，但这意味着持续不断地定期中断，并由两个竞争的工具执行日志备份。 这还有可能影响数据库的可恢复性，因为任何工具都不会有一整套备份。 尽管这一点适用于执行日志备份的任何两个功能或工具，但如下所述，强调特定的示例仍很有用。 这也是配置维护计划或日志传送问题的基础，如本主题的前面几节所述。  
  
 **Data Protection Manager (DPM) 备份：** Microsoft Data Protection Manager 允许执行完整备份和增量备份。 增量备份是在创建 T 日志备份之后执行日志截断的日志备份。 因此，不支持为同一数据库同时配置 DPM 和 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
 **第三方工具或脚本：** 执行日志备份的任何第三方工具或脚本导致日志截断与不兼容 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，并且不受支持。  
  
 如果已 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 为数据库实例启用了，并且想要获取即席备份，则可以[smart_admin 使用 Sp_backup_on_demand &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)存储过程，如前面部分所述。 如果还需要在 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 之外定期安排备份，则可使用“仅复制备份”。  有关详细信息，请参阅[仅复制备份 (SQL Server)](../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  
  
  
