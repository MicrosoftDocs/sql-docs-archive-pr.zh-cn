---
title: Reporting Services 的备份和还原操作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e895733457fe0c8892294540bbe8345cb121f2a7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589448"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Reporting Services 的备份和还原操作
  本主题概述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中使用的所有数据文件，并介绍应在何时以及如何备份这些文件。 为报表服务器数据库文件制定备份和还原计划是恢复策略中最重要的一部分。 但是，更全面的恢复策略应包括备份加密密钥、自定义程序集或扩展插件、配置文件，以及报表和模型的源文件。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
 备份和还原操作通常用于移动所有或部分 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装：  
  
-   如果只移动报表服务器数据库，则可以使用备份和还原或附加和分离功能在其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中重新定位数据库。 有关详细信息，请参阅 [将报表服务器数据库移至其他计算机（SSRS 本机模式）](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)。  
  
-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装移到新计算机的过程称为迁移。 在迁移安装时，需要运行安装程序以安装新的报表服务器实例，然后将实例数据复制到新计算机上。 有关迁移 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装的详细信息，请参阅以下主题：  
  
    -   [升级和迁移 Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
    -   [迁移 Reporting Services 安装（SharePoint 模式）](migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [迁移 Reporting Services 安装（本机模式）](migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>备份和还原报表服务器数据库  
 由于报表服务器是无状态服务器，因此所有应用程序数据都存储于在 **实例上运行的** reportserver **和** reportservertempdb [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 数据库中。 可以使用支持的备份 **数据库的方法之一备份** reportserver **和** reportservertempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 特定于报表服务器数据库的建议包括以下几项：  
  
-   应使用完整恢复模式备份 **reportserver** 数据库。  
  
-   应使用简单恢复模式备份 **reportservertempdb** 数据库。  
  
-   可以对每个数据库使用不同的备份计划。 备份 **reportservertempdb** 只是为了在发生硬件故障时避免重新创建该数据库。 在发生硬件故障时，不必恢复 **reportservertempdb**中的数据，但需要使用表结构。 如果 **reportservertempdb**丢失，重新获得它的唯一方法是重新创建报表服务器数据库。 如果重新创建 **reportservertempdb**，应使其名称与主报表服务器数据库的名称相同，这一点非常重要。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库的备份和恢复的详细信息，请参阅 [SQL Server 数据库的备份和还原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
> [!IMPORTANT]  
>  如果您的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器处于 SharePoint 模式下，则会有其他一些数据库需要加以注意，包括 SharePoint 配置数据库和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 警报数据库。 在 SharePoint 模式下，对于每个 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序将创建三个数据库。 **reportserver**、 **reportservertempdb**和 **dataalerting** 数据库。 有关详细信息，请参阅 [备份和还原 Reporting Services SharePoint 服务应用程序](../backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
## <a name="backing-up-the-encryption-keys"></a>备份加密密钥  
 首次配置 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装时，应备份加密密钥。 此外，任何时候更改服务帐户标识或重命名计算机时，都应备份密钥。 有关详细信息，请参阅 [Back Up and Restore Reporting Services Encryption Keys](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)。 对于 SharePoint 模式报表服务器，请参阅[管理 Reporting Services SharePoint 服务应用程序](../manage-a-reporting-services-sharepoint-service-application.md)的 "密钥管理" 部分。  
  
## <a name="backing-up-the-configuration-files"></a>备份配置文件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用配置文件来存储应用程序设置。 首次配置服务器时和部署任何自定义扩展插件之后，都应备份文件。 要备份的文件包括：  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   报表服务器和报表管理器 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 应用程序的 Web.config  
  
-   针对 的 Machine.config [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>备份数据文件  
 备份在报表设计器和模型设计器中创建和维护的文件。 这些文件包括报表定义 (.rdl) 文件、报表模型 (.smdl) 文件、共享数据源 (.rds) 文件、数据视图 (.dv) 文件、数据源 (.ds) 文件、报表服务器项目 (.rptproj) 文件以及报表解决方案 (.sln) 文件。  
  
 请记住备份为管理或部署任务创建的所有脚本文件 (.rss)。  
  
 确认具有所使用的所有自定义扩展插件和自定义程序集的备份副本。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器数据库 &#40;SSRS 本机模式&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Reporting Services 配置文件](../report-server/reporting-services-configuration-files.md)   
 [rskeymgmt 实用工具 &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)   
 [通过备份和还原来复制数据库](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [&#40;SSRS 本机模式下管理报表服务器数据库&#41;](../report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [配置和管理加密密钥（SSRS 配置管理器）](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
