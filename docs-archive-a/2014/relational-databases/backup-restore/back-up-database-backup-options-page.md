---
title: 备份数据库（“备份选项”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ffd527ba4334244c7fd4c5d4a73099093cb8520b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591432"
---
# <a name="back-up-database-backup-options-page"></a>备份数据库（“备份选项”页）
  使用  **“备份数据库”** 对话框的 **“备份选项”** 页可以查看或修改数据库备份选项。  
  
 **使用 SQL Server Management Studio 创建备份**  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  可以定义用于创建数据库备份的数据库维护计划。 有关详细信息，请参阅[维护计划](../maintenance-plans/maintenance-plans.md)和[使用维护计划向导](../maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定备份任务时，可以通过单击“脚本”  按钮，再为脚本选择一个目标，生成对应的 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) 脚本。  
  
## <a name="options"></a>选项  
  
### <a name="backup-set"></a>备份集  
 **“备份集”** 面板中的选项允许您指定有关备份操作所创建的备份集的可选信息。  
  
 **名称**  
 指定备份集名称。 系统将根据数据库名称和备份类型自动建议一个默认名称。  
  
 有关备份集的信息，请参阅[媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)。  
  
 **说明**  
 输入备份集的说明。  
  
 **备份集过期时间**  
 选择以下过期选项之一： 如果选择 **“URL”** 作为备份目标，则禁用此选项。  
  
|||  
|-|-|  
|**之后**|指定在多少天后此备份集才会过期，从而可被覆盖。 此值范围为 0 到 99999 天；0 天表示备份集将永不过期。<br /><br /> 备份过期时间的默认值是在“默认备份介质保持期(天)”  选项中设置的值。 若要访问此选项，请在对象资源管理器中右键单击服务器名称，再选择  “属性”；然后，单击  “服务器属性”对话框的  “数据库设置”页。|  
|**On**|指定备份集过期从而可被覆盖的具体日期。|  
  
### <a name="compression"></a>压缩  
 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] （或更高版本）支持 [备份压缩](backup-compression-sql-server.md)。  
  
 **设置备份压缩**  
 在 [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] （或更高版本）中，选择以下备份压缩值之一：  
  
|||  
|-|-|  
|**使用默认服务器设置**|单击此选项可使用服务器级别默认值。<br /><br /> 此默认值可通过 **backup compression default** 服务器配置选项进行设置。 有关如何查看此选项当前设置的信息，请参阅 [查看或配置 backup compression default 服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。|  
|**压缩备份**|单击此选项可压缩备份，而不考虑服务器级别默认值。<br /><br /> **\*\* 重要提示 \*\*** 默认情况下，压缩会大大提高 CPU 使用率，但压缩进程占用的额外 CPU 可能会对并发操作造成不利影响。 因此，你可能需要在会话中创建低优先级的压缩备份，其 CPU 使用率受 [资源调控器](../resource-governor/resource-governor.md)限制。 有关详细信息，请参阅本主题后面的 [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制。|  
|**不压缩备份**|单击此选项可创建未压缩的备份，而不考虑服务器级别默认值。|  
  
### <a name="encryption"></a>加密  
 若要创建加密的备份，请选中 **“加密备份”** 复选框。 选择要用于加密步骤的加密算法，然后从现有证书或非对称密钥的列表中提供一个证书或非对称密钥。 可用于加密的算法是：  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   三重 DES  
  
> [!TIP]  
>  如果您选择了追加到现有备份集，则禁用加密选项。  
>   
>  建议做法是备份证书或密钥，而存储它们的位置要与所加密的备份不同。  
>   
>  仅支持位于可扩展密钥管理 (EKM) 中的密钥。  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)   
 [备份文件和文件组 (SQL Server)](back-up-files-and-filegroups-sql-server.md)   
 [在数据库损坏时备份事务日志 (SQL Server)](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
