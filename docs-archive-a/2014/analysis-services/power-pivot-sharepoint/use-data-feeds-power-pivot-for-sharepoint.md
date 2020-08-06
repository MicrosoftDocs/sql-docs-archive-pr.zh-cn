---
title: 使用 PowerPivot for SharePoint) 的数据馈送 (|Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 19e3c5b448005314696f8167156a2326dc5009e1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689615"
---
# <a name="use-data-feeds-powerpivot-for-sharepoint"></a>使用数据馈送 (PowerPivot for SharePoint)
  数据馈送是从联机数据源生成并流向目标文档或应用程序的一个或多个数据流。 如果使用 PowerPivot for Excel，数据馈送可帮助您将任意数据源中的现有公司或业务数据提取到 Excel 2010 工作簿中的 PowerPivot 窗口中。 将数据馈送导入工作簿后，以后可以在 SharePoint 服务器上计划的任何数据刷新操作中引用该数据馈送。  
  
 数据馈送的使用方式取决于您使用的是支持 Atom 数据馈送的应用程序中的内置导出功能，还是创建并使用自定义数据服务。 能够发布并读取 Atom XML 数据的应用程序提供了无缝的数据传输，可对用户隐藏数据源和数据服务的机制。 对于用户而言，他或她只是将数据从一个应用程序移到另一个应用程序。  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 Microsoft SharePoint 2010 提供可在 PowerPivot 工作簿中使用的数据馈送。 可以使用本主题中的信息了解如何从已有的报表和列表访问数据馈送。  
  
 本主题包含以下各节：  
  
 [先决条件](#prereq)  
  
 [从 SharePoint 列表创建数据馈送](#sharepointlist)  
  
 [从 Reporting Services 报表创建数据馈送](#rsreport)  
  
 [从数据服务文档创建数据馈送](#dsdoc)  
  
##  <a name="prerequisites"></a><a name="prereq"></a>先决条件  
 您必须具有 PowerPivot for Excel 才能将数据馈送导入 Excel 2010。  
  
 您必须具有以 Atom 1.0 格式提供数据的 Web 服务或数据服务。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 SharePoint 2010 都可以提供此格式的数据。  
  
 在将 SharePoint 列表导出为数据馈送之前，必须在该 SharePoint 服务器上安装 ADO.NET Data Services。 有关详细信息，请参阅 [安装 ADO.NET Data Services 以支持 SharePoint 列表的数据馈送导出](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
##  <a name="create-a-data-feed-from-a-sharepoint-list"></a><a name="sharepointlist"></a>从 SharePoint 列表创建数据馈送  
 在 SharePoint 2010 场中，SharePoint 列表在列表功能区上有一个“作为数据馈送导出”按钮。 可以单击此按钮将列表作为馈送导出。 为了获得最佳结果，您的工作站上应装有 Excel 2010 以及 PowerPivot 客户端应用程序。 PowerPivot 客户端应用程序将启动，以响应数据馈送导出操作，并创建包含该列表的新的 PowerPivot 表。  
  
1.  打开 SharePoint 站点上的列表。  
  
2.  在“列表工具”中，单击 **“列表”**。  
  
3.  在“连接和导出”中，单击 **“作为数据馈送导出”**。  
  
    > [!NOTE]  
    >  "**作为数据馈送导出**" 按钮通过 PowerPivot 添加到 SharePoint。 如果您尚未安装 PowerPivot for SharePoint 或您未激活 PowerPivot 功能，则此按钮将不可用。  
  
4.  如果在本地安装了 PowerPivot for Excel，请单击 "**打开**"，或者单击 "**保存**" 将 .atomsvc 文档保存到硬盘，以便以后导入操作。  
  
5.  如果选择 **“打开”**，请使用表导入向导将数据馈送导入工作表。 该数据馈送将作为新表添加到 PowerPivot 窗口中。  
  
 如果在 SharePoint 服务器上未安装 ADO.NET Data Services 3.5.1，则将出现错误。 有关此错误和如何纠正此错误的详细信息，请参阅 [安装 ADO.NET Data Services 以支持 SharePoint 列表的数据馈送导出](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)。  
  
##  <a name="create-a-data-feed-from-a-reporting-services-report"></a><a name="rsreport"></a> 从 Reporting Services 报表创建数据馈送  
 如果已部署 SQL Server 2008 R2 Reporting Services，则可以使用新的 Atom 呈现扩展插件从现有报表生成数据馈送。 为了获得最佳结果，您的工作站上应装有 Excel 2010 以及 PowerPivot for Excel。 PowerPivot 客户端应用程序将启动，以响应数据馈送导出操作，并在表和列流入时自动添加和关联这些表和列。  
  
 有关如何从报表导出数据馈送的说明，请参阅[报表生成器帮助文件](https://go.microsoft.com/fwlink/?LinkId=154494)中的[基于报表生成数据馈送（报表生成器和 SSRS）](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  若要设置重复执行的数据刷新计划，以便将报表数据重新导入到已发布到 SharePoint 库的 PowerPivot 工作簿中，必须将报表服务器配置为与 SharePoint 进行集成。 有关将 PowerPivot for SharePoint 和 Reporting Services 一起使用的详细信息，请参阅[&#40;Reporting Services SharePoint 模式&#41;配置和管理报表服务器](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)。  
  
##  <a name="create-a-data-feed-from-a-data-service-document"></a><a name="dsdoc"></a> 从数据服务文档创建数据馈送  
 如果具有生成 Atom 馈送的自定义数据服务，则可以设置数据服务文档，将其作为使数据对用户和应用程序可用的一种方式。 “数据服务文档”(.atomsvc) 文件指定一个或多个连接，这些连接指向以 Atom 线路格式发布数据的联机源**。 可以在“数据馈送库”** 中创建数据服务文档，该库是一个专用库，它可以为浏览已发布到 SharePoint 服务器的数据服务文档提供公共访问点。 如果信息工作者有权访问数据馈送库中的数据服务文档，他们就可以通过引用该文档的 SharePoint URL 将数据馈送导入自己的工作簿和应用程序。  
  
1.  打开由您的站点管理员创建的数据馈送库。 有关详细信息，请参阅[创建或自定义数据馈送库 &#40;PowerPivot for SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)。  
  
2.  在“库工具”中，单击 **“文档”**。  
  
3.  单击 **“新建文档”**。  
  
4.  提供文件名和描述。  
  
5.  指定一个或多个提供馈送的 URL：  
  
    1.  **“基本 URL”** 是可选的。 如果数据服务文档提供多个馈送，则应该指定此选项。 基本 URL 应该指定所有馈送共有的 URL 部分（例如服务器名称和站点）。 如果按照 Reporting Services 报表创建数据服务文档，则基本 URL 将是报表服务器 URL 和报表。  
  
    2.  **“Web 服务 URL”** 是必需的。 如果没有基本 URL，此值必须在地址中包含 http:// 或 https://。 如果指定了基本 URL，则 Web 服务 URL 为基本 URL 之后的部分。 例如，如果完整 URL 为 http://adventure-works/inventory/today.aspx ，则基 url 将为 http://adventure-works/inventory ，并且 WEB 服务 URL 将为/today.aspx。  
  
         Web 服务 URL 可以包括用来筛选或选择数据子集的参数。 提供馈送的应用程序或服务必须支持您在 URL 中指定的参数。  
  
6.  输入 **“表名”**，每个馈送对应一个表。 此值是必需的。 表名由使用数据馈送的客户端应用程序使用。 在 PowerPivot for Excel 中，表名用于在包含导入数据的 PowerPivot 窗口中对表命名。  
  
## <a name="see-also"></a>另请参阅  
 [在管理中心中为网站集激活 PowerPivot 功能集成](activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [使用数据馈送库共享数据馈送 &#40;PowerPivot for SharePoint&#41;](share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
