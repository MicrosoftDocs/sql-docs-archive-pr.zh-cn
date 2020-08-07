---
title: 报表管理器 URL (SSRS 本机模式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ec43c91bb2d24bb96cc6541d93311ce6dd234ed4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588257"
---
# <a name="report-manager-url-ssrs-native-mode"></a>报表管理器 URL（SSRS 本机模式）
  使用报表管理器 URL 页可配置或修改用于访问报表管理器的 URL。 默认情况下，报表管理器 URL 继承报表服务器 Web 服务 URL 的前缀、IP 地址和端口。 这是因为报表管理器提供了对于运行在相同报表服务器服务中的 Web 服务的前端访问。 如果您正在隔离服务应用程序并使用报表管理器访问其他计算机上的报表服务器 Web 服务，则必须编辑 RSReportServer.config 文件以将报表管理器指向不同的实例。 有关配置与远程 Report Server 报表管理器连接的详细信息，请参阅[Reporting Services 配置管理器 &#40;纯模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]本机模式。  
  
 如果您打算将报表服务器配置为在 SharePoint 集成模式下运行，请不要创建报表管理器 URL。 在 SharePoint 集成模式下运行的报表服务器不支持报表管理器。 如果报表管理器已存在一个 URL，则将报表服务器配置为在 SharePoint 集成模式下运行后，该 URL 将不可用。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，并在导航窗格中单击 **“报表管理器 URL”** 。 有关如何启动 Configuration Manager 的详细信息，请参阅[Reporting Services 配置管理器 &#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
> [!NOTE]  
>  如果报表管理器未启用，则将无法设置此页上的选项。 有关启用报表管理器的详细信息，请参阅[Reporting Services 配置管理器 &#40;本机模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>选项  
 **虚拟目录**  
 指定报表管理器的虚拟目录名称。 在同一台计算机上，每个报表管理器实例只能有一个虚拟目录名称。  
  
 **URLs**  
 显示为当前报表管理器实例定义的 URL。  
  
 **高级**  
 为当前报表管理器实例添加附加 URL。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSRS Configuration Manager 配置 URL&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [&#40;SSRS Configuration Manager 的配置文件中的 Url&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [配置报表服务器 URL（SSRS 配置管理器）](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
