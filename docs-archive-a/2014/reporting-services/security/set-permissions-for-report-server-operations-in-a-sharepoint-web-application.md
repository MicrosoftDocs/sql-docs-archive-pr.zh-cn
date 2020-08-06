---
title: 在 SharePoint Web 应用程序中设置报表服务器操作的权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 68f503fef0e1350a502dd71c616fd309f0f30913
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692667"
---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>在 SharePoint Web 应用程序中设置报表服务器操作的权限
  对于在 SharePoint 集成模式下运行的报表服务器而言，在 SharePoint 站点定义的安全设置将决定您查看和管理报表、报表模型以及共享数据源的方式。 如果使用的是默认 SharePoint 组、权限级别和权限分配，则可以使用当前安全设置来处理报表和其他文档。  
  
 如果默认安全设置未提供所需访问级别，则可以使用以下各部分提供的信息来了解特定操作需要哪些权限：  
  
-   [查看和管理报表的权限](#permissionReports)  
  
-   [创建报表和使用报表生成器的权限](#permissionReportBuilder)  
  
-   [创建和管理共享计划的权限](#permissionSharedSchedules)  
  
-   [创建和管理订阅的权限](#permissionSubscriptions)  
  
-   [创建和管理共享数据源和报表模型的权限](#permissionDataSources)  
  
 在 SharePoint 站点上完成每个操作几乎都需要使用某几个关键权限。 这些权限未列在下面的任务和权限表中，但是您必须在创建自定义权限级别时包括这些必需的权限：  
  
-   浏览用户信息  
  
-   使用远程接口  
  
-   打开  
  
-   查看应用程序页  
  
 如果使用的是预定义权限级别，则无需执行任何操作，因为上述权限已经包含在“完全控制”、“设计”、“参与讨论”、“读取”和“有限访问”中。 但是，如果使用自定义权限级别或对分配给特定用户或组的权限进行编辑，则必须手动添加此权限。  
  
 利用“浏览用户信息”权限，报表服务器可以返回有关项目创建者和最后修改项目的用户的信息。 如果无此权限，报表服务器将返回以下错误。 对于浏览操作，错误为：“报表服务器遇到 SharePoint 错误。 ---> System.UnauthorizedAccessException：拒绝访问。” 对于发布操作，错误是： "为用户 '<用户 ' 授予的权限不足，无法 \<domain> \\ \> 执行此操作。"  
  
##  <a name="permissions-for-viewing-and-managing-reports"></a><a name="permissionReports"></a> 查看和管理报表的权限  
 报表定义权限是通过包含报表的库的列表权限来定义的，但如果要限制访问，则可以对单个报表设置权限。 下表提供了任务列表以及支持每个任务的权限列表。  
  
|任务|权限|  
|----------|----------------|  
|查看报表。|对包含文件的库或对单个报表拥有“查看项”  权限。|  
|查看将报表模型用作数据源的链接型报表。|对包含报表和报表模型的库或对单个报表和模型拥有“查看项”  权限。 如果您对模型没有查看权限，则仍可以打开该报表，但无法对数据执行即席浏览。<br /><br /> 如果报表模型使用模型项安全性，则用户还必须拥有该报表模型的“枚举权限”。 |  
|查看报表历史记录中的快照。|对包含文件的库或对单个报表拥有“编辑项”  权限。 对于特定报表，可以查看所有报表历史记录或不查看任何报表历史记录。 无法对报表历史记录中的单个快照设置权限。|  
|将报表上载或发布到库。|对将要包含报表的库拥有“添加项”  权限。|  
|设置报表的属性，包括数据源连接信息、处理选项和参数属性。|对包含报表的库或对单个报表拥有“编辑项”  权限。 还必须对共享数据源 (.rsds) 拥有查看权限以选择该共享数据源用于报表。|  
|计划报表处理。|若要选择共享计划，则必须对包含报表的库所在的站点拥有“打开”  权限。 若要计划数据处理或缓存过期时间，则必须对包含报表的库或对单个报表拥有“编辑项”  权限。|  
|删除报表。|对包含报表的库或对单个报表拥有“删除项”  权限。|  
|用更新的版本替换报表定义（在不影响属性、权限、历史记录或订阅的情况下）。|对包含报表的库或对单个报表拥有“编辑项”  权限。|  
|在报表历史记录中创建快照。|对要创建报表历史记录的报表所在的库拥有“添加项”  权限。|  
|在报表历史记录中创建快照。|对要创建报表历史记录的报表所在的库拥有“添加项”  权限。|  
|在报表历史记录中删除快照，并删除随着时间变化已签出和修改的报表定义的特定版本。|对要删除报表历史记录的报表所在的库拥有“删除版本”  权限。|  
|在报表历史记录中查看快照，并查看随着时间变化已签出和修改的报表定义的特定版本。|对包含报表的库拥有“查看版本”  权限。|  
  
##  <a name="permissions-for-creating-reports-and-using-report-builder"></a><a name="permissionReportBuilder"></a> 创建报表和使用报表生成器的权限  
 报表生成器是一种可用来创建特别报告的报表创作工具。 报表生成器将报表模型作为数据源使用，以支持即席数据浏览。 可以在报表生成器中加载模型，以便创建和运行报表，单击查看模型中的数据，也可以将报表保存到库中。 然后，拥有足够权限的用户可以打开同一报表，也可以执行即席数据浏览。  
  
> [!NOTE]  
>  对报表生成器的访问也可由权限之外的其他因素决定。 站点管理员可以通过设置服务器属性禁用特别报告，也可以通过不添加报表生成器报表内容类型添加到库来限制报表生成器的可用性，这样可防止用户在库的 **“新建”** 菜单中创建新报表。 此外，报表服务器管理员可以为报表服务器设置属性，以使报表生成器不可用。 如果服务器满足上述任一条件，则即使拥有所需的权限也不能使用报表生成器。  
  
 下表列出了用于创建报表和使用报表生成器的各项任务以及支持每项任务的权限：  
  
|任务|权限|  
|----------|----------------|  
|启动报表生成器。|没有显式用来控制对报表生成器的使用的权限。 如果配置了报表服务器集成并拥有将项添加到库的权限，则可以使用报表生成器。 若要从库的 **“新建”** 菜单中启动报表生成器，则必须注册报表生成器内容类型。 有关详细信息，请参阅[将报表服务器内容类型添加到库 &#40;Reporting Services 在 SharePoint 集成模式下&#41;" ](../add-reporting-services-content-types-to-a-sharepoint-library.md)。|  
|上载模型或共享数据源。|对将要包含文件的库拥有“添加项”  权限。|  
|查看模型或依赖的共享数据源。|对包含文件的库拥有“查看项”  权限。<br /><br /> 如果模型包含模型项安全设置，则用户还必须拥有该模型的“枚举权限”。 |  
|从共享数据源中生成模型。|对包含共享数据源 (.rsds) 文件（从中生成模型）的库拥有“添加项”  权限。|  
|在模型内设置对特定模型项的权限。|对包含库和报表模型 (.smdl) 文件的站点拥有“管理权限”  权限。|  
|在报表生成器中加载模型。|对报表模型 (.smdl) 文件拥有“编辑项”  权限。|  
|在报表生成器中创建报表定义并将报表保存到库中。|拥有将文件保存到库的“添加项”  权限。|  
|在报表生成器中编辑报表。|对报表定义文件拥有“编辑项”  权限。|  
  
 用来创建和使用订阅、报表历史记录以及对报表生成器报表设置报表或数据处理选项的权限与对标准报表定义文件执行同种操作所使用的权限相同。  
  
##  <a name="permissions-for-creating-and-managing-shared-schedules"></a><a name="permissionSharedSchedules"></a> 创建和管理共享计划的权限  
 共享计划并不是存储在库中的文档。 为此，创建和管理这些计划要求拥有网站权限。 无法限制对特定共享计划的访问。 创建的任何共享计划都可供整个网站上拥有打开权限的任一用户使用。  
  
 下表列出了用于创建、管理和使用共享计划的各项任务及权限：  
  
|任务|权限|  
|----------|----------------|  
|创建、编辑或删除共享计划。|对站点拥有“管理网站”  权限。|  
|为订阅处理或数据检索选择共享计划。|对包含库的站点拥有“打开”  权限。|  
  
##  <a name="permissions-for-creating-and-managing-subscriptions"></a><a name="permissionSubscriptions"></a> 创建和管理订阅的权限  
 SharePoint 强制在订阅和查看权限之间实现依赖关系。 对于没有查看权限的报表，无法订阅。 如果授予订阅报表的权限，则将自动授予查看权限。  
  
 下表列出了用于创建、管理和使用订阅的各项任务及权限：  
  
|任务|权限|  
|----------|----------------|  
|创建、编辑或删除用户拥有的对特定报表的订阅。|包含报表的库上或报表本身上的“编辑项”  。 “查看项”权限是一种依赖权限，会自动包含在权限级别中。 可以创建订阅的用户也可以创建自定义计划来运行该订阅。|  
|选择共享计划与订阅配合使用。|对包含库的站点拥有“打开”  权限。|  
|创建、编辑或删除整个站点上的任何订阅。|对站点拥有“管理通知”  权限。|  
  
##  <a name="permissions-for-creating-and-managing-shared-data-sources-and-report-models"></a><a name="permissionDataSources"></a> 创建和管理共享数据源和报表模型的权限  
 共享数据源 (.rsds) 文件包含可供多个报表和模型使用的数据源连接信息。 对于标准报表，使用 .rsds 文件来指定数据源连接信息是可选的。 对于模型驱动报表，使用 .rsds 文件是必需的。 报表模型始终使用 .rsds 文件连接到外部数据源。  
  
 可以设置共享数据源的属性，这些属性可决定各个用户是否可以查看或管理共享数据源。 查看或管理共享数据源的权限与报表查看权限不同；您可以在对 .rsds 文件本身没有查看权限的情况下查看使用 .rsds 文件的报表。  
  
|任务|权限|  
|-----------|----------------|  
|创建共享数据源。|对包含共享数据源的库拥有“添加项”  权限。 可以从库中的“新建”菜单创建新共享数据源。 为此，必须在库中注册报表数据源内容类型。 有关详细信息，请参阅[将报表服务器内容类型添加到库 &#40;Reporting Services 在 SharePoint 集成模式下&#41;" ](../add-reporting-services-content-types-to-a-sharepoint-library.md)。|  
|编辑共享数据源。|对包含共享数据源的库或对共享数据源本身拥有“编辑项”  权限。|  
|删除共享数据源。|对包含共享数据源的库或对共享数据源本身拥有“删除项”  权限。|  
|将共享数据源 (.rsds) 用于报表。|对报表或包含报表的库拥有“编辑项”  权限。 在报表上设置数据源属性包括选择共享数据源。|  
|从共享数据源中生成报表模型。|对将要包含报表模型的库拥有“添加项”  权限。|  
|删除报表模型。|对包含报表模型的库或对报表模型本身拥有“删除项”  权限。|  
|在模型内设置对特定模型项的权限。|对包含库和报表模型 (.smdl) 文件的站点拥有“管理权限”  权限。|  
  
> [!NOTE]  
>  没有编辑报表模型的权限。 尽管可以生成或删除报表模型，但不能在 SharePoint 站点内编辑这些报表模型。 编辑报表模型要求使用模型设计器，这是一种不受 SharePoint 中所设置的权限影响的客户端创作工具。  
  
## <a name="see-also"></a>另请参阅  
 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [将 Windows SharePoint Services 中的内置安全性用于报表服务器项](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  
