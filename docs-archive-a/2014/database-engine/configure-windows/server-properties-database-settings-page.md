---
title: 服务器属性（“数据库设置”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3beb2b6aa9a34982cccdfb252941c1c779a16121
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692513"
---
# <a name="server-properties-database-settings-page"></a>服务器属性（“数据库设置”页）
  使用此页可以查看或修改数据库设置。  
  
## <a name="options"></a>选项  
 **默认索引填充因子**  
 指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用现有数据创建新索引时对每一页的填充程度。 由于在页填充时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必须花时间来拆分页，因此填充因子会影响性能。  
  
 默认值为 100。有效值介于 0 和 100 之间。 填充因子值为 0 或 100 时，表示基于完全数据页创建聚集索引，并基于完全叶子页创建非聚集索引，但在索引树的较高级别中预留空间。 填充因子值 0 和 100 在所有方面都是相同的。  
  
 较小的填充因子值将导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基于不饱满的页创建索引。 每一个索引占用更多的存储空间，但同时也允许以后无需拆分页面即可插入索引。  
  
 **无限期等待**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在等待新备份磁带时永不超时。  
  
 **尝试一次**  
 指定如果需要备份磁带但它却不可用，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将超时。  
  
 **尝试的分钟数**  
 指定如果备份磁带在指定的时间内不可用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将超时。  
  
 **默认备份介质保持期(天)**  
 提供一个系统范围默认值，指示在用于数据库备份或事务日志备份后每一个备份介质的保留时间。 此选项可以防止在指定的日期前覆盖备份。  
  
 **压缩备份**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]（或更高版本）中，指示“backup compression default”选项的当前设置。 此选项决定了用于压缩备份的服务器级默认设置，具体如下：  
  
-   如果未选中 **“压缩备份”** 框，在默认情况下将不压缩新备份。  
  
-   如果 **“压缩备份”** 框已选中，则默认情况下将压缩新备份。  
  
    > [!IMPORTANT]  
    >  默认情况下，压缩显著增加 CPU 使用率，并且压缩进程占用的额外 CPU 可能会对并发操作造成不利影响。 因此，你可能需要在会话中创建低优先级的压缩备份，其 CPU 使用率受 [资源调控器](../../relational-databases/resource-governor/resource-governor.md)限制。 有关详细信息，请参阅本主题后面的 [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制。  
  
 如果你是 **sysadmin** 或 **serveradmin** 固定服务器角色的成员，则可以通过单击“压缩备份”  框来更改设置。  
  
 有关详细信息，请参阅[查看或配置“backup compression default”服务器配置选项](view-or-configure-the-backup-compression-default-server-configuration-option.md)和[备份压缩 (SQL Server)](../../relational-databases/backup-restore/backup-compression-sql-server.md)。  
  
 **恢复间隔(分钟)**  
 设置每个数据库恢复时所需的最大分钟数。 默认值为 0，指示由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动配置。 实际上，这表示每个数据库的恢复时间不超过 1 分钟，对于活动的数据库大约每 1 分钟有一个检查点。 有关详细信息，请参阅 [Configure the recovery interval Server Configuration Option](configure-the-recovery-interval-server-configuration-option.md)。  
  
 **Data**  
 指定数据文件的默认位置。 单击“浏览”按钮导航到新的默认位置。 直到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，更改才会生效。  
  
 **日志**  
 指定日志文件的默认位置。 单击“浏览”按钮导航到新的默认位置。 直到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，更改才会生效。  
  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果尚未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 查看此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  
