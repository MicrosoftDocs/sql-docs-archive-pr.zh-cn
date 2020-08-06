---
title: 规划 Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 558368c4f03f41537bf87ab979179f297c4fbb67
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586512"
---
# <a name="planning-for-reporting-services-and-power-view-browser-support-reporting-services-2014"></a>规划 Reporting Services 和 Power View 浏览器支持 (Reporting Services 2014)
  在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中，可以使用 Web 浏览器查看报表和运行报表管理器。 并非所有浏览器都支持所有的报表功能。 本主题将说明对于报表管理器管理功能、查看报表、Visual Studio 中的报表查看器控件的支持和要求。 本主题还将概述对于支持的浏览器的功能可用性、身份验证要求和脚本要求。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]SharePoint 模式 |[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]本机模式  
  
 **本主题内容：**  
  
- [Power View 浏览器方案](#bkmk_powerview)  
  
- [报表管理器的浏览器要求（本机模式）](#bkmk_reportmanager)  
  
- [查看报表的浏览器要求](#bkmk_reportviewer)  
  
- [身份验证要求](#bkmk_authentication)  
  
- [Visual Studio 中 ReportViewer Web 服务器控件的浏览器支持](#bkmk_controls)  
  
##  <a name="power-view-browser-scenarios"></a><a name="bkmk_powerview"></a>Power View 浏览器方案

 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 支持的受支持的浏览器和浏览器版本的列表取决于打开的文档类型。 Excel 2013 工作簿和 **"**  
  
|文档类型|环境|浏览器支持|  
|-------------------|-----------------|---------------------|  
|Power View 报表 (.RDLX)|**SharePoint Server：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] SharePoint 集成模式上的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 和 Power View Web 应用程序。|请参阅[Sharepoint Server 上的 Power View 和 Reporting Services Sharepoint 集成模式](#bkmk_powerview_on_SSRS)。|  
|使用 Power View 工作表的 Excel 2013 工作簿|**SharePoint 服务器：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]在 Excel Services 中。<br /><br /> **SharePoint Online (Office 365) ：** [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]在 Excel Web App 上。|请参阅[SharePoint Online 上的 Excel Services 或 Excel Web 应用上的 Power View](#bkmk_powerview_on_ExcelServices)。|  
  
###  <a name="power-view-on-sharepoint-server-and-reporting-services-sharepoint-integrated-mode"></a><a name="bkmk_powerview_on_SSRS"></a>SharePoint Server 上的 Power View 和 Reporting Services SharePoint 集成模式  
 下表总结了当用户在具有为 SharePoint 安装和配置的 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 服务应用程序和 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序的 SharePoint 场中打开 Power View 报表 (.RDLX) 时支持的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 浏览器版本。  
  
- 此表适用于 SharePoint 2010 和 SharePoint 2013。  
  
- 有关 SharePoint 2013 浏览器支持的详细信息，请参阅[在 sharepoint 2013 (中计划浏览器支持](https://technet.microsoft.com//library/cc263526\(office.15\).aspx) https://technet.microsoft.com/library/cc263526(office.15).aspx) 。  
  
- 有关 SharePoint 2010 浏览器支持的详细信息，请参阅 ([Sharepoint Server 2010) 计划浏览器 (支持](https://technet.microsoft.com/library/cc263526\(office.14\).aspx) https://technet.microsoft.com/library/cc263526(office.14).aspx) 。  
  
|**浏览器**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 10（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Mozilla Firefox (最新公开发布的版本) **|32 位|32 位|32 位|32 位|32 位|不支持|  
|**Apple Safari (最新公开发布的版本) **|不支持|不支持|不支持|不支持|不支持|32 位、64 位|  
  
> [!NOTE]  
> “32 位”指的是浏览器，而不是操作系统。 例如，在 64 位的 Windows 7 上可以使用 32 位的 Internet Explorer 9。  
  
#### <a name="inprivate-browsing-feature-in-internet-explorer"></a>Internet Explorer 中的 InPrivate 浏览功能

 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 不支持 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 8 和 Internet Explorer 9 中的 InPrivate 浏览功能。 有关 InPrivate 浏览的详细信息，请参阅[什么是 Inprivate 浏览？](https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing) (https://windows.microsoft.com/Windows7/What-is-InPrivate-Browsing).  
  
###  <a name="power-view-on-excel-services-or-the-excel-web-app-on-sharepoint-online"></a><a name="bkmk_powerview_on_ExcelServices"></a>在 SharePoint Online 上的 Excel Services 或 Excel Web 应用上 Power View

 下表汇总了当用户在运行 Excel Services 的 SharePoint Server 上使用 Power View 工作表打开 Excel 2013 工作簿时支持的 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 的浏览器版本：  
  
-   有关 SharePoint 2013 浏览器支持的详细信息，请参阅[在 sharepoint 2013 (中计划浏览器支持](https://technet.microsoft.com/library/cc263526\(office.15\).aspx) https://technet.microsoft.com/library/cc263526(office.15).aspx) 。  
  
|**浏览器**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|  
|**Internet Explorer 11（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 10（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|  
|**Mozilla Firefox (最新公开发布的版本) **|32 位|32 位|32 位|32 位|32 位|32 位、64 位|  
|**Apple Safari (最新公开发布的版本) **|不支持|不支持|不支持|不支持|不支持|32 位、64 位|  
|**Google Chrome (最新公开发布的版本) **|限时，32位** (\*) **|限时，32位** (\*) **|限时，32位** (\*) **|限时，32位** (\*) **|限时，32位** (\*) **|不支持|  
  
 ** (\*) ** Chrome 将停止支持由 Silverlight 使用的 Netscape 插件 API (NPAPI) 。 Power View 依赖于 Silverlight。  有关详细信息，请参阅 [“NPAPI 最终倒计时”](http://blog.chromium.org/2014/11/the-final-countdown-for-npapi.html)。  
  
##  <a name="report-manager-browser-requirements-native-mode"></a><a name="bkmk_reportmanager"></a> (本机模式下的浏览器要求报表管理器) 

 下面是可以用于运行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 本机模式报表管理器以便管理报表和报表服务器的支持的浏览器的当前列表。  
  
|浏览者|  
|-------------|  
|Internet Explorer 7 或更新版本且必须启用了脚本撰写功能。|  
|Mozilla FireFox (最新公开发布的版本) |  
|Apple Safari (最新公开发布的版本) |  
|Google Chrome (最新公开发布的版本) |  
  
##  <a name="browser-requirements-for-viewing-reports"></a><a name="bkmk_reportviewer"></a>查看报表的浏览器要求

 以下是报表查看器支持的浏览器和功能的当前列表。 报表查看器支持从 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表管理器和 SharePoint 库查看报表。  
  
|**浏览器**|**Windows 8 和 8.1**|**Windows 7**|**Windows Server 2012 和 2012 R2**|**Windows Server 2008 R2**|**Windows Server 2008**|**Mac OS X 10.6-10。9**|**适用于 iPad 的 iOS 6-7**|  
|-----------------|---------------------------|-------------------|-----------------------------------------|--------------------------------|-----------------------------|------------------------------|----------------------------|  
|**Internet Explorer 11（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|不支持|不支持|  
|**Internet Explorer 10（适用于台式机）**|32 位、64 位|32 位、64 位|32 位、64 位|不支持|不支持|不支持|不支持|  
|**Internet Explorer 9**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 8**|不支持|32 位、64 位|不支持|32 位、64 位|32 位、64 位|不支持|不支持|  
|**Internet Explorer 7**|不支持|不支持|不支持|不支持|32 位、64 位|不支持|不支持|  
|**Mozilla Firefox (最新公开发布的版本) **|32 位|32 位|32 位|32 位|32 位|不支持|不支持|  
|**Apple Safari (最新公开发布的版本) **|不支持|不支持|不支持|不支持|不支持|32 位、64 位|支持<sup> (1) </sup>的有限功能|  
|**Google Chrome (最新公开发布的版本) **|32 位|32 位|32 位|32 位|32 位|不支持|不支持|  
  
 **<sup>(1)</sup>**  支持以下功能：  
  
- 导出为 PDF 和 TIFF 格式。  
  
- 在 iOS 设备上的 Apple Safari 中以交互方式查看报表。 功能支持包括展开/折叠、参数窗格和交互式排序。  
  
- 有关详细信息，请参阅[在 Microsoft Surface 设备和 Apple IOS 设备上查看 Reporting Services 报表](../../2014/reporting-services/view-reporting-services-reports-surface-ios-devices.md)。  
  
 **注意** 如果从 Macintosh 计算机访问报表服务器，则建议使用 Safari。 如果你使用的是与集成的 SharePoint 产品 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ，请参阅[ (Windows SharePoint Services) 计划浏览器支持](https://go.microsoft.com/fwlink/?LinkId=183583)。  
  
### <a name="url-access-for-viewing-reports"></a>查看报表的 URL 访问

 若要直接查看报表而不是通过报表管理器查看报表，可以使用 URL 访问链接到报表和报表查看器。 URL 访问支持多种浏览器。  
  
 有关 URL 访问的详细信息，请参阅以下主题：  
  
- [URL 访问参数引用](url-access-parameter-reference.md)  
  
###  <a name="authentication-requirements"></a><a name="bkmk_authentication"></a>身份验证要求

 浏览器支持必须由报表服务器处理的特定身份验证方案，以使客户端请求获得成功。 下表标识 Windows 操作系统上运行的各浏览器支持的默认身份验证类型。  
  
|**浏览器类型**|**支持**|**浏览器默认值**|**服务器默认值**|  
|----------------------|------------------|-------------------------|------------------------|  
|**Internet Explorer**|协商、Kerberos、NTLM、基本|Negotiate|是的。 默认身份验证设置使用 Internet Explorer。|  
|**Firefox**|NTLM、基本|NTLM|是的。 默认身份验证设置使用 Firefox。|  
|**Safari**|基本|基本|是的。 默认身份验证设置使用 Safari。|  
|**Chrome**|协商、NTLM、基本|协商|是的。 默认身份验证设置使用 Chrome。|  
  
### <a name="script-requirements"></a>脚本要求

 若要使用报表查看器，请将浏览器配置为可以运行脚本。  
  
 如果未启用脚本功能，则打开报表时将显示如下错误消息：  
  
- **您的浏览器不支持脚本或已配置为不允许脚本运行。请单击此处在没有脚本的情况下查看此报表**。  
  
 如果选择查看不支持脚本的报表，则报表将会以 HTML 格式呈现，同时不具有报表工具栏和文档结构图等报表查看器功能。  
  
> [!NOTE]  
> 报表工具栏是 HTML 查看器组件的一部分。 默认情况下，该工具栏显示在浏览器窗口中呈现的每个报表的返回页首。 报表查看器提供的功能包括能够在报表中搜索信息、滚动到特定的页以及调整页大小以便查看。 有关报表工具栏或 HTML 查看器的详细信息，请参阅 [HTML Viewer and the Report Toolbar](html-viewer-and-the-report-toolbar.md)。  
  
##  <a name="browser-support-for-reportviewer-web-server-controls-in-visual-studio"></a><a name="bkmk_controls"></a>Visual Studio 中 ReportViewer Web 服务器控件的浏览器支持

 ReportViewer Web 服务器控件用于在 ASP.NET Web 应用程序中嵌入报表功能。 这些控件随 Visual Studio 一起提供，并且支持与本主题中所述的其他组件不同的浏览器和浏览器版本。 用于查看应用程序的浏览器类型确定您可以在应用程序中提供的 ReportViewer 功能类型。 使用本主题中提供的表确定哪些支持的浏览器受报表功能的限制以及支持的平台。  
  
 由于支持的浏览器的呈现引擎不同，一些高级报表功能可能会在不同的浏览器中以不同的方式显示。  例如，文本旋转。  
  
### <a name="scripting-requirements"></a>脚本要求

 使用启用了脚本支持的浏览器。 如果浏览器无法运行脚本，则不能查看报表。  
  
### <a name="browser-requirements-for-viewing-reports-with-the-reportviewer-web-server-controls"></a>使用 ReportViewer Web 服务器控件查看报表的浏览器要求

 对交互式报表功能的支持因浏览器类型而异。 以下支持矩阵显示在各个平台上支持的浏览器类型，所受的限制在“注释”列中列出。  
  
|||||||||  
|-|-|-|-|-|-|-|-|  
|**浏览器**|**Windows 8** 和 **Windows 8.1**|**Windows 7**|**Windows Server 2012**和**2012 R2**|**Windows Server 2008** 和 **2008 R2**|**Windows Server 2003**|**Mac OS X 10.6-10。9**|**说明**|  
|**桌面版 Internet Explorer 11 (**|是|是|是|不支持|不支持|不支持|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 10（适用于台式机）**|是|是|是|不支持|不支持|不支持|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 9**|不支持|是|不支持|是|是|是|Internet Explorer 支持全部 ReportViewer 功能。|  
|**Internet Explorer 8.0**|不支持|是|不支持|是|是<sup>1</sup>|不支持|Internet Explorer 支持全部 ReportViewer 功能。 <sup>1</sup>|  
|**Internet Explorer 7.0**|不支持|是|不支持|是|是<sup>1</sup>|不支持|Internet Explorer 支持全部 ReportViewer 功能。 <sup>1</sup>|  
|**Firefox (最新公开发布的版本) **|是|是|是|是|是|不支持|不支持打印和缩放。|  
|**Safari (最新公开发布的版本) **|不支持|不支持|不支持|不支持|不支持|是|不支持打印和缩放。<br /><br /> 在此浏览器中禁用了用于在参数化报表上选择日期的日历控件。 用户必须在参数提示区域中手动键入要使用的日期。|  
|**Chrome (最新公开发布的版本) **|是|是|是|是|是|不支持|不支持打印和缩放。|  
  
 <sup>1</sup>在标准模式下，Internet Explorer 7.0 和8.0 不在报表中显示斜线。 如果在报表中使用斜线，请将 ASP.NET 页设置为在 Internet Explorer 怪异模式下运行。 为此，请 \<!DOCTYPE> 在 ASP.NET 页中查找标记。 如果，如果使用母板页，可以在 .master 文件中查找它。 此标记类似于以下内容：  
  
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
```
  
 将 \<!DOCTYPE> 标记替换为以下标记：  
  
```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">  
```
  
 有关 Internet Explorer 中兼容模式的详细信息，请参阅[定义文档兼容性](https://go.microsoft.com/fwlink/?LinkId=180380) (https://go.microsoft.com/fwlink/?LinkId=180380) 。  
  
 有关使用 ReportViewer 控件的详细信息，请参阅 ([部署报表和 ReportViewer 控件](https://msdn.microsoft.com/library/ms251723.aspx) https://msdn.microsoft.com/library/ms251723.aspx) 。  
  
## <a name="next-steps"></a>后续步骤

 [Reporting Services 工具](tools/reporting-services-tools.md)[报表管理器 &#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) [HTML 查看器和报表工具栏](html-viewer-and-the-report-toolbar.md)
