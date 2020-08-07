---
title: 部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 91a0ff978020c29ecc5c52a336f8b7aab065fc1e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588890"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>部署清单：通过将 PowerPivot 服务器添加到 SharePoint 2010 场进行扩展
  如果您预期在 SharePoint 场中对 PowerPivot 查询处理有大量请求，则可以通过添加额外的 PowerPivot for SharePoint 实例来无缝地添加新的查询和数据处理支持。  
  
 安装新的实例后，您就有了额外的容量进行 PowerPivot 数据查询或处理 PowerPivot 数据刷新作业。 此外，您也可以选择将每台服务器配置为只处理一种类型的请求：查询或数据刷新。  
  
## <a name="prerequisites"></a>必备条件  
 已安装并已配置 SharePoint Server 2010。  
  
 已应用 SharePoint Server 2010 SP1，并且已升级场。  
  
 场中的现有 PowerPivot for SharePoint 实例为 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]（新安装或从 SQL Server 2008 R2 升级）。  
  
 您要在其上安装新 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint 服务器的计算机已加入场中。 场中的计算机和其他服务器必须位于同一域中。  
  
 查看以下其他主题以了解系统和版本要求：  
  
-   [在 SharePoint 2010 场中使用 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  在多服务器场中，所有 PowerPivot for SharePoint 实例必须具有相同的版本。 如果已对场中的其他 PowerPivot 服务器应用 Service Pack 或更新，则将要添加的新实例也必须进行相应的更新，使其版本与场中现有实例的版本一致。 在应用更新之前，新实例将不可用。  
  
## <a name="steps"></a>步骤  
 使用此核对清单将其他 PowerPivot 服务器添加到 SharePoint 场。 这些说明假定您已在场中设置了一个 PowerPivot for SharePoint 服务器，并且正要添加第二个服务器以处理额外的处理负荷。 除了在安装要求、安装后配置和验证方面存在差异外，用于部署扩展解决方案的步骤与向现有场添加单个 PowerPivot 服务器的步骤完全相同。  
  
|步骤|链接|  
|----------|----------|  
|确定已在场中的 Analysis Services 实例的服务帐户|您安装的每个附加实例在运行时使用的帐户必须与第一个实例使用的帐户相同。 使用以下两种方法之一可以确定服务帐户：<br /><br /> 在 "管理中心" 的 "安全性" 部分，单击 "**配置服务帐户**"。 选择 " **Windows 服务-SQL Server Analysis Services**"。 在选择该服务后，服务帐户名称将显示在页面中。<br /><br /> 在已安装 PowerPivot 服务的服务器上，在 "管理工具" 中打开 "**服务**" 控制台应用程序。 双击**SQL Server Analysis Services**。 单击 "**登录**" 选项卡以查看服务帐户。<br />** \* \* 重要 \* 提示 \* ：** 只使用管理中心更改服务帐户。 如果您使用其他工具或方法，将无法在场中正确更新权限。|  
|运行安装程序以安装 PowerPivot for SharePoint 的第二个实例|[安装 PowerPivot for SharePoint](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 选择已加入场中但在其上尚无 PowerPivot 实例的应用程序服务器。<br /><br /> 在安装过程中，当系统提示您指定服务帐户时，请输入上一步中的帐户。 Analysis Services 服务的所有实例都必须在同一域帐户下运行。 为了遵循这一要求，您必须在 SharePoint 中使用托管帐户功能，以便在同一位置更新同一类型的所有服务实例的密码。|  
|配置第二个实例|您可以使用以下两种方法之一配置实例： [PowerPivot 配置工具](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools)或[使用 Windows PowerShell 的 powerpivot 配置](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)<br /><br /> 配置第二个实例时，您只需要设置本地服务。 所有其他配置任务（例如创建服务应用程序或配置数据刷新）均在初始配置期间执行，并由您所安装的后续实例使用。|  
|安装后任务|无需特别执行进一步的步骤。 您不需要创建服务应用程序、激活功能、部署解决方案或更改服务应用程序标识。 现有 Web 应用程序和服务应用程序将自动发现和使用新的服务器软件。<br /><br /> （可选）如果您安装第二个服务器是为了将一个服务器用于查询而将另一个用于数据刷新，则现在可以配置服务器实例属性以指定由每个服务器处理的请求类型。 有关详细信息，请参阅[配置专用数据刷新或仅限查询的处理 &#40;PowerPivot for SharePoint&#41;](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)。|  
|验证第二个实例的安装|您可以使用以下步骤来验证您刚安装的服务器上的 PowerPivot 查询处理。<br /><br /> 1) 在 "管理中心" 中，打开 "管理服务器上的服务" 页，确认服务器及其服务是否出现。<br />-在 "服务器" 中，单击向下箭头，单击 "更改服务器"，然后选择具有新 PowerPivot for SharePoint 安装的服务器。<br />-验证是否已启动 SQL Server Analysis Services 和 SQL Server PowerPivot 系统服务。<br /><br /> 2) 在管理中心，停止其他 PowerPivot for SharePoint 服务器，使刚刚安装的服务器是唯一可用的服务器。 有关详细信息，请参阅[启动或停止 PowerPivot for SharePoint 服务器](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server)。<br /><br /> 3) 单击某一 PowerPivot 工作簿可从库中打开它。<br /><br /> 4) 单击切片器或数据透视以启动查询。 该服务器将在后台加载 PowerPivot 数据。 在下一步骤中，您将连接到该服务器以便确认数据已加载并且缓存。<br /><br /> 5) 从 "开始" 菜单中的 Microsoft SQL Server 程序组开始 SQL Server Management Studio。 如果未在您的服务器上安装此工具，则可以跳到最后一步以便确认缓存文件是否存在。<br /><br /> 6) 在 "服务器类型" 中选择 " **Analysis Services**"。<br /><br /> 7) 在 "服务器名称" 中，输入** \<server-name> \powerpivot**，其中 **\<server-name>** 是安装了新 PowerPivot for SharePoint 的计算机的名称。<br /><br /> 8) 单击 "**连接**"。<br /><br /> 9) 在对象资源管理器中，单击 "**数据库**" 查看加载的 PowerPivot 数据文件的列表。<br /><br /> 10) 在计算机文件系统上，检查以下文件夹以确定文件是否已缓存到磁盘。 存在缓存文件将进一步证实您的部署正常工作。 若要查看文件缓存，请转到 \Program Files\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup 文件夹。<br /><br /> 11) 重新启动之前停止的服务。|  
  
## <a name="see-also"></a>另请参阅  
 [初始配置 &#40;PowerPivot for SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 安装](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [在管理中心中管理和配置 PowerPivot 服务器](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
  
