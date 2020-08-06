---
title: Reporting Services 工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 43e181e52cd40c961423b4e5f8b60d5528145005
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691571"
---
# <a name="reporting-services-tools"></a>Reporting Services 工具
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含支持在托管环境中开发和使用具有丰富功能的报表的一组图形和脚本编写工具。 该工具集包括开发工具、配置和管理工具以及报表查看工具。 本主题简要介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的各工具以及如何访问该工具。  
  
 如需立即找到工具，请参阅[教程：如何查找并启动 Reporting Services 工具 (SSRS)](tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md)。  
  
## <a name="tools-for-report-authoring"></a>报表创作工具  
 下表列出了可用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中创作报表的工具。  
  
|工具|说明|如何访问|  
|----------|-----------------|-------------------|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|交互式数据浏览和直观显示体验，为使您可基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型创建报表和与报表交互而专门设计。<br /><br /> 注意：需要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在 SharePoint 模式下运行。|具有 Silverlight 的浏览器。|  
|报表设计器|使用此工具可以设计报表和部署到本机模式或 SharePoint 模式报表服务器。<br /><br /> 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> 用于组织在报表中使用的数据的“报表数据”窗格<br /><br /> 用于交互式报表设计的设计和预览的选项卡式视图<br /><br /> 可帮助指定要从数据源中检索的数据以及与 [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md)中的数据源类型相关联的查询设计器<br /><br /> 具有 IntelliSense 的表达式编辑器，生成可自定义报表内容和外观的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 表达式<br /><br /> 支持自定义报表项和自定义查询设计器<br /><br /> <br /><br /> 有关详细信息，请参阅 [SQL Server Data Tools 中的 Reporting Services (SSDT)](reporting-services-in-sql-server-data-tools-ssdt.md)。|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|报表生成器|使用此工具可以设计报表和部署到本机模式或 SharePoint 模式报表服务器。<br /><br /> 类似 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 的创作环境<br /><br /> 能够将报表项另存为报表部件<br /><br /> 用于创建地图的向导<br /><br /> 聚合的聚合<br /><br /> 增强的对表达式的支持<br /><br /> 帮助指定要从所选内置数据源类型检索的数据的查询设计器<br /><br /> <br /><br /> 有关详细信息，请参阅[报表生成器 &#40;SSRS&#41;](report-builder-authoring-environment-ssrs.md)。|下载 MSI 或者从报表管理器/SharePoint 打开|  
  
## <a name="tools-for-report-server-administration"></a>用于报表服务器管理的工具  
 一组图形和脚本工具可用于管理中的 Report Server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您使用的工具取决于您的报表服务器的部署模式。  
  
### <a name="native-mode"></a>本机模式  
 下表列出了可用于管理在本机模式下部署的报表服务器的工具。  
  
|工具|说明|如何访问|  
|----------|-----------------|-------------------|  
|Reporting Services 配置管理器|使用此工具可以配置 Reporting Services 安装。 请注意，Reporting Services 配置管理器不会帮助你管理 Report Server 内容、启用其他功能或授予对服务器的访问权限。 可用任务包括：<br /><br /> 配置本地和远程报表服务器实例<br /><br /> 配置报表服务器服务帐户。<br /><br /> 创建和配置一个或多个 Web 服务 URL。<br /><br /> 配置报表管理器 URL<br /><br /> 创建和配置报表服务器数据库。<br /><br /> 配置扩展部署。<br /><br /> 备份、还原或替换用于加密存储的连接字符串以及凭据的对称密钥。<br /><br /> 配置无人参与的执行帐户。<br /><br /> 配置 SMTP 服务器以进行电子邮件传递。<br /><br /> <br /><br /> 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)。|“开始”菜单|  
|SQL Server Management Studio|使用此工具可以在单一环境中管理一个或多个报表服务器实例，包括：<br /><br /> 管理本地和远程报表服务器实例<br /><br /> 设置报表服务器属性<br /><br /> 修改角色定义<br /><br /> 关闭不使用的报表服务器功能<br /><br /> 管理作业<br /><br /> 管理共享计划|“开始”菜单|  
|SQL Server 配置管理器|使用此工具可以：<br /><br /> 启动和停止 Reporting Services Windows 服务<br /><br /> 配置客户反馈报告、转储目录位置和错误报告<br /><br /> <br /><br /> 警告不要使用此工具来配置服务帐户。 ** \* \* \* \* ** 请改用 Reporting Services 配置工具。<br /><br /> 有关详细信息，请参阅 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)。|“开始”菜单|  
|Rsconfig 实用工具|使用此工具可配置和管理报表服务器与报表服务器数据库的连接。 您还可以使用该工具来指定用于无人参与报表处理的用户帐户。<br /><br /> 有关详细信息，请参阅[报表服务器命令提示实用工具 (SSRS)](report-server-command-prompt-utilities-ssrs.md)。|命令提示符|  
|Rskeymgmt 实用工具|使用此工具可以：<br /><br /> 提取、还原、创建和删除用于加密报表服务器数据的对称密钥<br /><br /> 在扩展部署中联接报表服务器实例<br /><br /> <br /><br /> 有关详细信息，请参阅[报表服务器命令提示实用工具 (SSRS)](report-server-command-prompt-utilities-ssrs.md)。|命令提示符|  
|Windows Management Instrumentation (WMI) 类|通过使用这些类，无需使用图形用户界面即可自动化 Reporting Services 配置管理器中的配置任务。<br /><br /> 有关详细信息，请参阅 [Accessing the WMI Provider Programmatically](../accessing-the-wmi-provider-programmatically.md)。|Visual Basic 脚本|  
  
### <a name="sharepoint-integrated-mode"></a>SharePoint 集成模式  
 在 SharePoint 模式下，Reporting Services 是 SharePoint 体系结构中的服务应用程序，并且直接通过 SharePoint 进行管理  
  
|工具|说明|如何访问|  
|----------|-----------------|-------------------|  
|SharePoint 管理中心|使用 SharePoint 管理中心可为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]创建、查询和管理共享服务应用程序。<br /><br /> 有关详细信息，请参阅[配置和管理报表服务器（Reporting Services SharePoint 模式）](../configure-administer-report-server-reporting-services-sharepoint-mode.md)。|浏览到 SharePoint 站点 URL 以便进行中心管理|  
|PowerShell Cmdlet|使用 PowerShell cmdlet 可为 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]创建、查询和管理共享服务应用程序。<br /><br /> 有关详细信息，请参阅 [用于 Reporting Services SharePoint 模式的 PowerShell cmdlet](../powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。|SharePoint 2010 Management Shell|  
  
## <a name="tools-for-report-content-management"></a>用于报表内容管理的工具  
 提供了一组图形和脚本编写工具来管理中的内容 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 您使用的工具取决于您的报表服务器的部署模式。  
  
|工具|说明|如何访问|  
|----------|-----------------|-------------------|  
|报表服务器 Web 服务 URL|使用此工具可在一般的项导航页中浏览报表目录中的内容。<br /><br /> 有关详细信息，请参阅 [Report Server Web Service](../report-server-web-service/report-server-web-service.md)。|浏览者|  
|报表管理器|**（仅限本机模式）** 使用此工具可通过 HTTP 连接来管理远程位置的单个报表服务器实例。 您可以执行下列操作：<br /><br /> 查看、搜索、打印和订阅报表。<br /><br /> 创建、保护和维护文件夹层次结构，以便组织服务器上的项。<br /><br /> 配置基于角色的安全性，确定对项和操作的访问权限。<br /><br /> 配置报表执行属性、报表历史记录和报表参数。<br /><br /> 创建连接到 Microsoft SQL Server Analysis Services 数据源或 SQL Server 关系数据源或从其检索数据的报表模型。<br /><br /> 设置模型项安全性，以便可以访问模型中的特定实体，或将实体映射到事先创建的预定义点击链接型报表。<br /><br /> 创建共享计划和共享数据源，以提高计划和数据源连接的可管理性。<br /><br /> 创建可以将报表展开为大型收件人列表的数据驱动订阅。<br /><br /> 创建链接报表，以便按不同方式重用现有报表和重新确定其用途。<br /><br /> 启动报表生成器来创建可以在报表服务器上保存和运行的报表。<br /><br /> <br /><br /> 有关详细信息，请参阅[报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。||  
|RS 实用工具|此工具是可用于执行脚本操作的脚本主机。 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 使用此工具可以运行   脚本，这些脚本可在报表服务器数据库之间复制数据、发布报表、在报表服务器数据库中创建项等。<br /><br /> 有关详细信息，请参阅[报表服务器命令提示实用工具 (SSRS)](report-server-command-prompt-utilities-ssrs.md)。|命令提示符|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 报表服务器](../reporting-services-report-server.md)   
 [SSRS &#40;Reporting Services 概念&#41;](../reporting-services-concepts-ssrs.md)   
 [Reporting Services (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
