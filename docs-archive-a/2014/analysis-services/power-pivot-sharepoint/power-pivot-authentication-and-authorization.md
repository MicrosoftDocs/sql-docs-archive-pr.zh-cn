---
title: PowerPivot 身份验证和授权 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 48230cc0-4037-4f99-8360-dadf4bc169bd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1cf777960b24d9c65c7e7f7d9651eeb48e0fe42b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687272"
---
# <a name="powerpivot-authentication-and-authorization"></a>PowerPivot 身份验证和授权
  在 SharePoint 2010 场中运行的 PowerPivot for SharePoint 部署使用 SharePoint 服务器提供的身份验证子系统和授权模型。 SharePoint 安全基础结构扩展至 PowerPivot 内容和操作，因为所有与 PowerPivot 相关的内容都存储在 SharePoint 内容数据库中，并且通过场中的 PowerPivot 共享服务执行所有与 PowerPivot 相关的操作。 使用基于对应 Windows 用户标识的 SharePoint 用户标识对请求包含 PowerPivot 数据的工作簿的用户进行身份验证。 工作簿上的查看权限决定了是同意还是拒绝请求。  
  
 因为自助服务数据分析需要与 Excel Services 进行集成，所以，为了确保 PowerPivot 服务器的安全，您还需要了解 Excel Services 安全性。 当用户查询与 PowerPivot 数据具有数据连接的数据透视表时，Excel Services 将数据连接请求转发给场中的 PowerPivot 服务器以加载数据。 服务器之间的这种交互要求您了解如何配置两个服务器的安全设置。  
  
 单击下面的链接可阅读本主题中的特定部分：  
  
 [Windows 身份验证（使用经典模式登录）要求](power-pivot-authentication-and-authorization.md#bkmk_auth)  
  
 [要求用户授权的 PowerPivot 操作](#UserConnections)  
  
 [用于 PowerPivot 数据访问的 SharePoint 权限](#Permissions)  
  
 [PowerPivot 工作簿的 Excel Services 安全注意事项](#excel)  
  
##  <a name="windows-authentication-using-classic-mode-sign-in-requirement"></a><a name="bkmk_auth"></a>使用经典模式登录要求的 Windows 身份验证  
 PowerPivot for SharePoint 支持 SharePoint 中可用的一组简化的身份验证选项。 在这些可用的身份验证选项中，PowerPivot for SharePoint 部署只支持 Windows 身份验证。 此外，通过登录访问的 Web 应用程序必须配置为经典模式。  
  
 Windows 身份验证是必需的，因为 PowerPivot for SharePoint 部署中的 Analysis Services 数据引擎只支持 Windows 身份验证。 Excel Services 使用 Windows 用户标识通过 MSOLAP OLE DB 访问接口建立到 Analysis Services 的连接，该标识已通过 NTLM 或 Kerberos 协议进行了身份验证。  
  
 第二个要求（针对 Web 应用程序的经典模式身份验证）用于确保 PowerPivot Web 服务的可操作性。 Web 服务是在 Web 前端上运行并提供到场中 PowerPivot for SharePoint 服务器的 HTTP 重定向的组件。 尽管 Web 服务声明可以识别服务到服务的通信，但是它不声明可以识别路由到场中 PowerPivot 共享服务的数据连接请求。 仅对使用 Windows 标识来自 IIS 的经过身份验证的连接支持加载 PowerPivot 数据的请求。 Web 应用程序的经典模式登录确保成功从 PowerPivot Web 服务连接到场中的 PowerPivot 共享服务。  
  
 尽管经典模式登录不是较常见的数据访问方案（其中，PowerPivot 数据提取自呈现它的同一 Excel 工作簿）所必需的，但不要尝试将 PowerPivot for SharePoint 与配置为使用其他身份验证访问接口的 SharePoint Web 应用程序一起使用。 只要用户尝试连接到作为外部数据源的 PowerPivot 工作簿，上述操作就会导致连接失败。  
  
 如果未使用经典模式登录，则 PowerPivot Web 服务处理的以下类型的请求将失败：  
  
-   对来自场外的 PowerPivot 数据的任何请求（例如，在报表设计器或报表生成器中创建一个报表，其中数据源为指向 PowerPivot 工作簿的 SharePoint URL）  
  
-   来自客户端应用程序或报表的场内请求，该应用程序或报表使用 PowerPivot 工作簿作为外部数据源（例如，在 Excel 桌面应用程序中创建一个工作簿，将您的数据源作为包含 PowerPivot 数据的第二个发布的 Excel 工作簿）  
  
### <a name="how-to-check-the-authentication-provider-for-your-application"></a>如何检查应用程序的身份验证访问接口  
 在创建新的 Web 应用程序时，请确保在“新建 Web 应用程序”页中选择 **“经典模式的身份验证”** 选项。  
  
 对于现有的 Web 应用程序，使用以下说明来验证 Web 应用程序配置为使用 Windows 身份验证。  
  
1.  在管理中心的 "应用程序管理" 中，单击 "**管理 web 应用程序**"。  
  
2.  选择 Web 应用程序。  
  
3.  单击 **“身份验证访问接口”**。  
  
4.  验证您对于每个区域具有一个访问接口，默认区域设置为 Windows。  
  
##  <a name="powerpivot-operations-requiring-user-authorization"></a><a name="UserConnections"></a>需要用户授权的 PowerPivot 操作  
 对 PowerPivot 查询和数据处理的所有级别的访问都仅使用 SharePoint 授权。  
  
 不支持基于 Analysis Services 角色的授权模型。 在单元、行或表级别对于 PowerPivot 数据没有基于角色的授权。 您不能保护工作簿的不同部分，以授予或拒绝特定用户对其中敏感数据的访问权限。 嵌入的 PowerPivot 数据全部可供对 SharePoint 库中的 Excel 工作簿具有查看权限的用户使用。  
  
 PowerPivot for SharePoint 在以下情况下将模拟 SharePoint 用户：  
  
-   针对与 PowerPivot 数据库具有数据连接的数据透视表或数据透视图执行的查询，其中，某个 PowerPivot 服务应用程序代表用户与处理数据的特定 PowerPivot 共享服务实例之间建立连接。  
  
-   在数据无法以其他方式可用的情况下从缓存或库加载 PowerPivot 数据。 如果对尚未加载到系统中的 PowerPivot 数据发出数据连接请求，[!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]实例将使用 SharePoint 用户的标识来从内容库中检索数据源并将其加载到内存中。  
  
-   数据刷新操作，用于将数据源的已更新副本保存到内容库中的工作簿。 在此情况下，将使用从安全存储区服务中的目标应用程序检索的用户名和密码执行实际登录操作。 凭据可以是 PowerPivot 无人参与的数据刷新帐户，也可以是在创建数据刷新计划时随其存储的凭据。 有关详细信息，请参阅为[Powerpivot 数据刷新配置存储的凭据 &#40;PowerPivot for SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)并[配置 Powerpivot 无人参与的数据刷新帐户 &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)。  
  
##  <a name="sharepoint-permissions-for-powerpivot-data-access"></a><a name="Permissions"></a>用于 PowerPivot 数据访问的 SharePoint 权限  
 只有通过 SharePoint 集成，才能支持发布、管理和保护 PowerPivot 工作簿。 SharePoint 服务器提供身份验证和授权子系统，以确保合法访问数据。 没有支持的方案可用于安全地在 SharePoint 场之外部署 PowerPivot 工作簿。  
  
 用户通过“查看”权限或更高权限对 PowerPivot 数据的访问在服务器上是只读的。 “参与讨论”权限允许添加和编辑文件。 更改 PowerPivot 数据要求您将工作簿下载到安装了 PowerPivot for Excel 的 Excel 桌面应用程序。 对文件的“参与讨论”权限将确定用户是否可在本地下载文件然后将更改保存回 SharePoint。  
  
 在这种情况下，“参与讨论”和“仅查看”权限级别确定用户对于 PowerPivot 数据的有效访问权限集。 其他权限级别的最大限度与“参与讨论”和“仅查看”的权限相同（例如，因为“读取”包含“仅查看”权限，所以，已分配了“读取”权限的用户将与“仅查看”具有相同的访问权限级别）。  
  
 下表汇总了确定对 PowerPivot 数据和服务器操作的访问权限的权限级别：  
  
|权限级别|允许这些任务|  
|----------------------|------------------------|  
|场或服务管理员|安装、启用和配置服务和应用程序。<br /><br /> 使用 PowerPivot 管理面板和查看管理报表。|  
|完全控制|在网站集级别激活 PowerPivot 功能集成。<br /><br /> 创建 PowerPivot 库。<br /><br /> 创建数据馈送库。|  
|参与|添加、编辑、删除和下载 PowerPivot 工作簿。<br /><br /> 配置数据刷新。<br /><br /> 基于 SharePoint 站点上的 PowerPivot 工作簿创建新的工作簿或报表。<br /><br /> 在数据馈送库中创建数据服务文档|  
|读取|将 PowerPivot 工作簿作为外部数据源访问，其中，工作簿 URL 在连接对话框中显式输入 (例如，在 Excel 的数据连接向导) 中。|  
|仅查看|查看 PowerPivot 工作簿。<br /><br /> 查看数据刷新历史记录。<br /><br /> 将本地工作簿连接到 SharePoint 站点上的 PowerPivot 工作簿，以其他方法重新设定其数据的作用。<br /><br /> 下载该工作簿的一个快照。 该快照是数据的静态副本，没有切片器、筛选器、公式或数据连接。 该快照的内容类似于从浏览器窗口复制单元值。|  
  
##  <a name="excel-services-security-considerations-for-powerpivot-workbooks"></a><a name="excel"></a>PowerPivot 工作簿的 Excel Services 安全注意事项  
 PowerPivot 服务器端查询处理与 Excel Services 紧密耦合。 在文档级别开始产品集成，因为 PowerPivot 工作簿是包含或引用 PowerPivot 数据的 Excel 工作簿 (.xlsx) 文件。 PowerPivot 工作簿没有单独的文件扩展名。  
  
 当在 SharePoint 站点中打开 PowerPivot 工作簿时，Excel Services 读取嵌入的 PowerPivot 数据连接字符串，并将请求转发到本地 SQL Server Analysis Services OLE DB 访问接口。 然后，此访问接口将连接信息传递给场中的 PowerPivot 服务器。 为了使请求在两个服务器之间无缝传递，必须将 Excel Services 配置为使用 PowerPivot for SharePoint 要求的设置。  
  
 在 Excel Services 中，与安全性相关的配置设置在受信任位置、受信任的数据访问接口和受信任的数据连接库中指定。 下表介绍可实现或增强 PowerPivot 数据访问的设置。 如果某个设置未在此处列出，则它对于 PowerPivot 服务器连接没有影响。 有关如何逐步指定这些设置的说明，请参阅[PowerPivot for SharePoint&#41;的初始配置 &#40;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)中的 "启用 Excel Services" 一节。  
  
> [!NOTE]  
>  与安全性相关的大多数设置适用于受信任位置。 如果您希望保留默认值或为不同站点使用不同值，则可以为包含 PowerPivot 数据的站点创建其他受信任位置，然后仅为该站点配置以下设置。 有关详细信息，请参阅 [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)。  
  
|区域|设置|说明|  
|----------|-------------|-----------------|  
|Web 应用程序|Windows 身份验证访问接口|PowerPivot 将它从 Excel Services 获得的声明标记转换为 Windows 用户标识。 任何使用 Excel Services 作为资源的 Web 应用程序都必须配置为使用 Windows 身份验证提供程序。|  
|受信任位置|位置类型|此值必须设置为 **Microsoft SharePoint Foundation**。 PowerPivot 服务器检索 .xlsx 文件的副本，并将其加载到场中的 Analysis Services 服务器上。 此服务器只能从内容库中检索 .xlsx 文件。|  
||允许外部数据|此值必须设置为 **“受信任的数据连接库和嵌入连接”**。 PowerPivot 数据连接嵌入在工作簿中。 如果您不允许嵌入的连接，则用户可以查看数据透视表缓存，但将不能与 PowerPivot 数据交互。|  
||刷新时警告|如果您正在使用 PowerPivot 库来存储工作簿和报表，则应禁用此值。 PowerPivot 库包含一个文档预览功能，如果同时关闭“打开时刷新”和“刷新时警告”，则其效果最佳。|  
|受信任的数据访问接口|MSOLAP.4<br /><br /> MSOLAP.5|默认情况下包含 MSOLAP.4，但是 PowerPivot 数据访问要求 MSOLAP.4 访问接口为 SQL Server 2008 R2 版本。<br /><br /> MSOLAP.5 随 PowerPivot for SharePoint 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本一起安装。<br /><br /> 请勿从受信任的数据访问接口列表中删除这些访问接口。 在某些情况下，您可能需要在场中的其他 SharePoint 服务器上安装此访问接口的更多副本。 有关详细信息，请参阅 [在 SharePoint 服务器上安装 Analysis Services OLE DB 提供程序](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。|  
|受信任的数据连接库|可选。|可以在 PowerPivot 工作簿中使用 Office 数据连接 (.odc) 文件。 如果您使用 .odc 文件向本地 PowerPivot 工作簿提供连接信息，则可以将相同的 .odc 文件添加到此库。|  
|用户定义函数程序集|不适用。|PowerPivot for SharePoint 忽略您为 Excel Services 生成部署的用户定义函数程序集。 如果对于特定行为依赖于用户定义程序集，请注意 PowerPivot 查询处理将不使用您创建的用户定义函数。|  
  
## <a name="see-also"></a>另请参阅  
 [配置 PowerPivot 服务帐户](configure-power-pivot-service-accounts.md)   
 [将 PowerPivot 无人参与的数据刷新帐户配置 &#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [在管理中心中为 PowerPivot 站点创建受信任位置](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)   
 [PowerPivot 安全体系结构](https://go.microsoft.com/fwlink/?linkID=220970)  
  
  
