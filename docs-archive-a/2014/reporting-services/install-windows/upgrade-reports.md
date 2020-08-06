---
title: 升级报表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a2b6d2bb8fec78bd17235512c965d1d5ffd93113
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577387"
---
# <a name="upgrade-reports"></a>Upgrade Reports
  报表定义 (.rdl) 文件通过以下方式自动升级：  
  
-   当您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的报表设计器中打开某一报表时，报表定义将升级到当前支持的 RDL 架构。 当您在项目属性中指定某一 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 报表服务器时，报表定义将保存在与目标服务器兼容的架构中。  
  
-   将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装升级到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 安装时，已发布到报表服务器的现有报表和快照将在第一次进行处理时编译并自动升级为新的架构。 如果报表不能自动升级，则将使用向后兼容模式处理报表。 报表定义保留在原始架构中。  
  
 在您将报表定义文件直接上载到报表服务器或 SharePoint 站点时，报表不升级。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中升级报表定义是升级 .rdl 文件的唯一方法。  
  
 在本地或在报表服务器上升级报表后，您可能注意到出现附加的错误、警告和消息。 这是对内部报表对象模型和处理组件进行更改的结果，当在报表中检测到根本问题时，将导致出现这些消息。 有关详细信息，请参阅 [Reporting Services Backward Compatibility](../reporting-services-backward-compatibility.md)。  
  
 有关的新功能的详细信息 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ，请参阅[&#41;的新功能 &#40;Reporting Services ](../what-s-new-reporting-services.md)。  
  
 本主题内容：  
  
-   [升级支持的版本](#bkmk_versionsupported)  
  
-   [报表定义 ( .rdl) 文件和报表设计器](#bkmk_rdlfiles)  
  
-   [已发布的报表和报表快照](#bkmk_publishedreports_and_snapshots)  
  
-   [向后兼容模式](#bkmk_backcompat)  
  
-   [使用子报表升级报表](#bkmk_subreports)  
  
-   [使用自定义报表项升级报表](#bkmk_CRIs)  
  
-   [“转换 CRI”对话框](#bkmk_convertCRIdialog)  
  
##  <a name="versions-supported-by-upgrade"></a><a name="bkmk_versionsupported"></a>升级支持的版本  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 早期的任一版本中创建的报表都可以升级。 包括下列版本：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 Service Pack 1  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 Service Pack 2  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
##  <a name="report-definition-rdl-files-and-report-designer"></a><a name="bkmk_rdlfiles"></a> 报表定义 (.rdl) 文件和报表设计器  
 报表定义文件包括对 RDL 命名空间的引用，该命名空间指定了用于验证 .rdl 文件的报表定义架构的版本。  
  
 当您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的报表设计器中打开某个 .rdl 文件时，如果报表是针对先前命名空间创建的，报表设计器会自动创建一个备份文件，并将该报表升级到当前命名空间。 这是升级报表定义文件的唯一方法。  
  
 您设置的部署属性可以影响保存报表定义文件的架构。 有关详细信息，请参阅 [SQL Server Data Tools 中的部署和版本支持 (SSRS)](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)中。  
  
 可以将在早期版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中创建的 .rdl 文件上载到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器，该报表将在第一次使用时自动升级。 报表服务器将以原始格式存储报表定义文件。 报表将在第一次被查看时自动升级，但是存储的报表定义文件仍保持不变。  
  
> [!NOTE]  
>  不能将具有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表定义命名空间的报表发布或上载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 报表服务器。  
  
 若要为报表、报表服务器或报表设计器标识当前 RDL 架构，请参阅[查找报表定义架构版本 (SSRS)](../reports/find-the-report-definition-schema-version-ssrs.md)。  
  
##  <a name="published-reports-and-report-snapshots"></a><a name="bkmk_publishedreports_and_snapshots"></a> 已发布的报表和报表快照  
 第一次使用时，报表服务器会尝试将现有的已发布报表和报表快照升级为新的报表定义架构，不需要您执行特定操作。 当用户查看报表或报表快照时，或者当报表服务器处理订阅时，将尝试进行升级。 报表定义不会被替换，而是继续存储在它在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表服务器上的原始架构中。 如果报表不能升级，则报表将在向后兼容模式下运行。  
  
##  <a name="backward-compatibility-mode"></a><a name="bkmk_backcompat"></a> 向后兼容模式  
 成功升级的报表由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器进行处理。 不能升级的报表由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器在向后兼容模式下进行处理。 一个报表不能同时由这两个报表处理器来处理。 第一次使用时，报表将成功升级或标记为向后兼容。  
  
 只有 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器才支持新功能。 如果报表不能升级，您仍然可以查看呈现的报表，但不能使用新功能。 若要利用新功能，必须成功地升级报表。  
  
##  <a name="upgrading-a-report-with-subreports"></a><a name="bkmk_subreports"></a> 使用子报表升级报表  
 当报表中包含子报表时，升级过程中会出现四种可能的状态之一：  
  
-   主报表和所有子报表都能成功地升级。 它们由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器来处理。  
  
-   主报表和所有子报表都不能升级。 它们由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器来处理。  
  
-   主报表可以升级，但一个或多个子报表不能升级。 主报表由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器处理，但呈现的报表在不能升级的子报表将出现的位置显示消息“错误: 无法处理子报表”。  
  
-   主报表不能升级，但一个或多个子报表可以升级。 主报表由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器处理，但呈现的报表在子报表将出现的位置显示消息“错误: 无法处理子报表”。  
  
 如果看到错误“错误: 无法处理子报表”，则必须更改主报表或子报表的定义，以便可以由报表处理器的同一版本处理报表。  
  
 钻取报表没有此限制，因为它们被作为独立的报表处理。  
  
##  <a name="upgrading-a-report-with-custom-report-items"></a><a name="bkmk_CRIs"></a> 使用自定义报表项升级报表  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表可能包含由第三方软件供应商提供并由系统管理员安装在报表创作计算机和报表服务器上的自定义报表项 (CRI)。 可以按以下方式升级包含 CRI 的报表：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表服务器升级到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表服务器。 在首次使用时自动升级报表服务器上的已发布报表。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表上载到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表服务器。 报表将在首次使用时自动升级。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的报表设计器中打开 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]报表。 将创建原始报表的一个备份副本。 发生以下两种情况之一：  
  
    1.  报表中的所有 CRI 没有不受支持的功能。 CRI 将转换为新报表定义架构中的报表项，以便升级整个报表。 如果保存该文件，则它将保存在当前 RDL 命名空间中。  
  
    2.  报表中的一个或多个 CRI 具有不受支持的功能。 出现一个对话框，提示用户是转换这些 CRI 还是将它们保留不变。  
  
     有关详细信息，请参阅本主题后面的 [在报表设计器中打开报表](#OpeningaReport) 。  
  
 有关为报表服务器、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或报表标识当前 RDL 命名空间的信息，请参阅[查找报表定义架构版本 (SSRS)](../reports/find-the-report-definition-schema-version-ssrs.md)。  
  
### <a name="upgrading-reports-on-a-report-server"></a>升级报表服务器上的报表  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表第一次在已升级到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表服务器的报表服务器上运行时，该报表将自动升级到报表服务器支持的当前报表定义命名空间。 该报表可能在升级之前已存在于报表服务器上，或该报表可能已通过报表管理器上载，或从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的报表设计器发布到报表服务器。  
  
 下表列出由报表服务器为报表中特定类型的 CRI 执行的升级操作。  
  
|CRI 类型|报表服务器升级操作|  
|--------------|----------------------------------|  
|第三方 CRI|不执行升级。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器来处理。|  
|具有不受支持的功能的 Dundas 2005 图表 CRI|升级到最新的 RDL 架构。 所有的 Dundas 2005 图表 CRI 都将转换为与 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]兼容的图表数据区域。<br /><br /> 由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器来处理。|  
|不具有不受支持的功能的 Dundas 2005 仪表 CRI|升级到最新的 RDL 架构。 所有的 Dundas 2005 仪表 CRI 都将转换为与 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 兼容的仪表数据区域。<br /><br /> 由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表处理器来处理。|  
|具有不受支持的功能的 Dundas 2005 图表 CRI|不执行升级。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器来处理。|  
|具有不受支持的功能的 Dundas 2005 仪表 CRI|不执行升级。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表处理器来处理。|  
  
###  <a name="opening-a-report-with-cris-in-report-designer"></a><a name="OpeningaReport"></a> 在报表设计器中使用 CRI 打开报表  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表设计器中打开包含 cri 的2005报表时 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ，报表将升级到新的报表定义架构。 根据报表中包含的 CRI，将执行下列操作之一：  
  
-   检测到第三方 CRI。 如果安装在报表创作计算机上的 CRI 的版本与新的 RDL 架构不兼容，则设计图面将显示带有红色 X 的文本框。您必须与系统管理员联系，以便从与新的 RDL 架构兼容的第三方供应商那里安装新版本的 CRI。  
  
-   检测到 Dundas 2005 图表或仪表 CRI，所有实例都包含受支持的功能。 所有 Dundas 2005 图表和仪表 CRI 都将转换为您在工具箱中看到的 Reporting Services 图表和仪表报表项。 这些项称为本机图表和仪表报表项。  
  
-   检测到 Dundas 2005 图表或仪表 CRI，所有实例都包含不受支持的功能。 不受支持的功能将在本节后面的内容中介绍。 您可以选择是否将所有 CRI 转换为本机报表项。  
  
    -   如果转换它们，报表将升级到新的 RDL 架构，Dundas 2005 图表和仪表 CRI 将转换为相应的本机图表和仪表报表项，但将删除不受支持的功能。 在呈现报表中，您看到的情况可能与 CRI 的显示方式有所不同。  
  
    -   如果选择不转换它们，则报表将升级到新的 RDL 架构，但是 CRI 将被视为第三方 CRI。 您必须配合系统管理员和第三方供应商来安装与新报表架构兼容的全新 CRI。 如果新的 CRI 不可用，则报表将在报表设计器中显示一个带有红色 X 的文本框。  
  
 在报表创作环境中升级报表后将其保存，这是将现有报表升级到新的报表定义架构的唯一方式。  
  
### <a name="unsupported-dundas-2005-chart-custom-report-item-functionality"></a>不受支持的 Dundas 2005 图表自定义报表项功能  
 Dundas 2005 图表 CRI 不受支持的功能包括：  
  
-   批注。  
  
-   自定义图例项。  
  
-   自定义属性具有下列名称：  
  
    -   CUSTOM_CODE_CS  
  
    -   CUSTOM_CODE_VB  
  
    -   CUSTOM_CODE_COMPILED_ASSEMBLY  
  
         例如，如果 .rdl 文件包含以下部分，则需要在升级之前将其删除：  
  
        ```  
        <CustomProperty>  
         <Name>CUSTOM_CODE_CS</Name>  
         <Value>dXNpWERwegfdfgiobxxl3bmc... </Value>  
        </CustomProperty>  
        ```  
  
### <a name="unsupported-dundas-2005-gauge-custom-report-item-functionality"></a>不受支持的 Dundas 2005 仪表自定义报表项功能  
 Dundas 2005 仪表 CRI 不受支持的功能包括：  
  
-   数字指示器。  
  
-   状态指示器。  
  
-   自定义图像。  
  
###  <a name="convert-cri-dialog-box"></a><a name="bkmk_convertCRIdialog"></a>"转换 CRI" 对话框  
 该报表包含其中有不受支持的功能的自定义报表项 (CRI)。 CRI 是对报表定义语言 (RDL) 的扩展，它支持用于显示报表中的数据的自定义对象。 CRI 包含由第三方软件供应商提供的设计时和运行时组件。  
  
> [!NOTE]  
>  对于是否选择在报表服务器上支持自定义报表项，需要由系统管理员决定。 若要查看报表中的 CRI，必须将 CRI 组件安装在报表创作客户端上以预览报表，并将其安装在报表服务器上以查看已发布或上载的报表。 有关详细信息，请参阅来自第三方软件供应商的[自定义报表项](../custom-report-items/custom-report-items.md)和文档。  
  
 某些 CRI 可以转换为采用新的报表定义格式的报表项。 有关可以转换的 CRI 的列表，请参阅 [Upgrading Reports](upgrade-reports.md)。 使用下表可以决定是否转换该报表中的 CRI：  
  
-   **是** 选择 **“是”** 将转换报表中所有可以转换的 CRI。 无法升级 CRI 中不受支持的功能，也不能从报表定义文件中删除它们。 有关不支持的功能的列表，请参阅 [Upgrading Reports](upgrade-reports.md)。 查看报表时，可能看到 CRI 在报表中的显示方式存在差异。  
  
-   **否** ：如果不希望转换报表中的 CRI，请选择 **“否”** 。 当前版本中的报表处理器无法显示这些 CRI。 如果您的系统管理员计划安装从第三方软件供应商那里得到的且与新报表定义格式兼容的新版本 CRI，则应当选择 **“否”**。 在使用新版本以前，CRI 将作为带有红色 X 的空文本框显示在报表中。  
  
 在任一情况下，报表将升级到新的报表定义格式，并将原始报表的备份副本另存为 *\<Report Name>* `-` 备份 .rdl。 如果在报表创作工具中保存报表，则会以新的报表定义格式保存升级的报表。 如果发布报表，则报表首先保存在您的计算机上，然后发布到报表服务器。 您需要将报表的升级版本发布到报表服务器。  
  
 如果不保存报表，则原始报表将保持不变。 但是，不能在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 版本中或者在使用较新报表定义格式的报表创作环境中编辑该报表。 对于报表的原始版本，通过使用报表管理器将它上载到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 报表服务器，可以继续运行它。 有关详细信息，请参阅[上传文件或报表（报表管理器）](../reports/upload-a-file-or-report-report-manager.md)。  
  
 对于上载而不是发布到报表服务器的报表，报表处理器将在第一次使用该报表时确定是否可以将它升级。 对于无法升级的报表，将以向后兼容模式对其进行处理，并像在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的早期版本中那样继续显示它们。  
  
## <a name="see-also"></a>另请参阅  
 [升级和迁移 Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [SQL Server 2014 中 SQL Server Reporting Services 的重大更改](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014 中 SQL Server Reporting Services 的行为更改](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server 2014 中的 SQL Server Reporting Services 已停止使用的功能](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [自定义报表项](../custom-report-items/custom-report-items.md)   
 [升级报表服务器数据库](upgrade-a-report-server-database.md)  
  
  
