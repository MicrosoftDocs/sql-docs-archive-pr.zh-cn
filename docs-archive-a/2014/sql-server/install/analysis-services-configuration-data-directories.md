---
title: Analysis Services 配置-数据目录 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ef732855-b7af-4f40-a619-5573c1c354bb
author: heidisteen
ms.author: heidist
ms.openlocfilehash: e0711c6998e8f931e7d561bb388a0d7809733a44
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586233"
---
# <a name="analysis-services-configuration---data-directories"></a>Analysis Services 配置 - 数据目录
  下表中的默认目录是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中可由用户配置的目录。 对这些文件的访问权限授予了本地管理员和在 \<instance> 安装过程中创建并设置的 SQLServerMSASUser $ 安全组的成员。  
  
## <a name="ui-element-list"></a>UI 元素列表  
  
|说明|默认目录|建议|  
|-----------------|-----------------------|---------------------|  
|数据根目录|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID>\OLAP\Data \| 确保 \Program files\Microsoft SQL Server \ 文件夹受到有限权限的保护。 在许多配置中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 性能取决于数据目录所在的存储区的性能。 请将此目录放置在附加到系统上的最高性能存储区中。 对于故障转移群集安装，应确保数据目录位于共享磁盘上。|  
|日志文件目录|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID>\OLAP\Log \| 这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 日志文件的目录，其中包括 FlightRecorder 日志。 如果要延长网络流量记录器持续时间，请确保该日志目录有足够的空间。|  
|Temp 目录|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID>\OLAP\Temp \| 将 Temp 目录放置在高性能存储子系统上。|  
|备份目录|C:\Program Files\Microsoft SQL Server\MSAS12. \<InstanceID>\OLAP\Backup \| 这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 默认备份文件的目录。 对于 PowerPivot for SharePoint 安装，这还是 PowerPivot 系统服务缓存 PowerPivot 数据文件的位置。<br /><br /> 确保设置合适的权限以防止数据丢失，并确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务的用户组具有写入备份目录的足够权限。 不支持对备份目录使用映射的驱动器。|  
  
## <a name="notes"></a>注释  
  
-   在 SharePoint 场上部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例将应用程序文件、数据文件和属性存储于内容数据库和服务应用程序数据库中。  
  
-   向现有安装添加功能时，不能更改以前安装的功能的位置，也不能为新功能指定该位置。  
  
-   如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例中的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件也应安装到单独的目录。  
  
-   在下列情况下，不能安装程序文件和数据文件：  
  
    -   在可移动磁盘驱动器上  
  
    -   在使用压缩的文件系统上  
  
    -   在系统文件所在的目录上  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 的默认实例和命名实例的文件位置](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
  
