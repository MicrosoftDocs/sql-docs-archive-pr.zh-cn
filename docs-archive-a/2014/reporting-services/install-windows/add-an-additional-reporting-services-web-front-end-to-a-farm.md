---
title: 向场中添加另一个 Reporting Services Web 前端 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d7a11bda-ae26-49ac-b071-37d83cae5afe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 958bff78538336f70de5b76f7619cca8b8105e1a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694325"
---
# <a name="add-an-additional-reporting-services-web-front-end-to-a-farm"></a>向场中添加另一个 Reporting Services Web 前端
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式包括应用程序服务器和 Web 前端 (WFE) 服务器所需的组件。 本主题主要介绍如何为 WFE 服务器安装所需的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件，包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能（例如订阅、数据警报和 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]）使用的应用程序页。 WFE 所需的主要 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装是安装用于 SharePoint 2010 产品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。

## <a name="prerequisites"></a>必备条件

-   您必须是本地管理员才能运行 SQL Server 安装程序。

-   必须将计算机加入到域中。

-   您需要知道承载 SharePoint 配置和内容数据库的现有数据库服务器的名称。

-   该数据库服务器必须配置为允许远程数据库连接。  如果没有这样配置，将无法将新的服务器连接到场，因为这个新服务器将无法建立与 SharePoint 配置数据库的连接。

-   新服务器将需要安装有与当前场服务器正在运行的 SharePoint 相同的版本。 例如，如果该场已安装了 SharePoint 2010 Service Pack 1 (SP1)，则您还需要在新的服务器上安装 SP1，然后才能将其联接到该场。

-   查看以下其他主题以了解系统和版本要求：

     [在 SharePoint 2010 场中使用 SQL Server BI 功能的指南](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)

## <a name="steps"></a>步骤
 本主题中的步骤假定 SharePoint 场管理员正在安装和配置服务器。 下图说明一个典型的三层环境，下面的列表中将说明图中的编号项：

-   (1) 多个 Web 前端 (WFE) 服务器。 WFE 服务器要求用于 SharePoint 2010 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 外接程序。 以下步骤将第二个应用程序服务器添加到这一层。

-   (2) 运行 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和网站的两个应用程序服务器，例如管理中心。

-   (3) 两个 SQL Server 数据库服务器。

-   (4) 表示软件或硬件的网络负载平衡解决方案 (NLB)

 ![将 SSRS 添加到新 SharePoint WFE](../../../2014/sql-server/install/media/rs-sharepointscale-wfe.gif "将 SSRS 添加到新 SharePoint WFE")

 下面的步骤假定管理员正在安装和配置服务器。

|步骤|说明和链接|
|----------|--------------------------|
|运行 SharePoint 2010 产品准备工具|您必须拥有 SharePoint 2010 安装介质。 准备工具是安装介质中的 **PrerequisiteInstaller.exe** 。|
|安装 SharePoint 2010 产品。|1) 选择 "**服务器场**" 安装类型。<br /><br /> 2) 为服务器类型选择 "**完成**"。<br /><br /> 3) 安装完成后，如果你的现有 SharePoint 场已安装 SharePoint 2010 SP1，则不要运行 SharePoint 产品配置向导。 您应该在运行 SharePoint 产品配置向导之前安装 SharePoint SP1。|
|安装 SharePoint Server 2010 SP1。|如果现有 SharePoint 场安装了 SharePoint 2010 SP1，请从中下载并安装 SharePoint 2010 SP1： [https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697) 。<br /><br /> 有关 SharePoint 2010 SP1 的详细信息，请参阅 [安装 Office 2010 SP1 和 SharePoint 2010 SP1 时的已知问题](https://support.microsoft.com/kb/2532126)：|
|运行 SharePoint 产品配置向导以便向场中添加服务器。|1) 在**Microsoft sharepoint 2010 products**计划组中，单击 " **Microsoft Sharepoint 2010 产品配置向导**"。<br /><br /> 2) 在 "**连接到服务器场**" 页上，选择 "**连接到现有场**" 并单击 "**下一步**"。<br /><br /> 3) 在 "**指定配置数据库设置**" 页上，键入用于现有场的数据库服务器的名称以及配置数据库的名称。 单击“下一步”。<br />**&#42;&#42; 重要 &#42;&#42;** 如果你看到类似于以下内容的错误消息，并且已验证你具有权限，则在**SQL Server Configuration Manager**中验证为 SQL Server 网络配置启用了哪些协议。 "无法连接到数据库服务器。 请确保数据库存在，是 Sql Server，并且您具有访问服务器的相应权限。 "<br />**&#42;&#42; 重要 &#42;&#42;** 如果你看到 "**服务器场产品和修补程序状态**" 页，则需要查看该页上的信息，然后用所需文件更新服务器，然后才能继续将服务器加入到场。<br /><br /> 4) 在 "**指定场安全设置**" 页上键入场密码，然后单击 "**下一步**"。 在确认页上单击 **“下一步”** 以便运行向导。<br /><br /> 5) 单击 "**下一步**" 运行**场配置向导**。|
|验证服务器已添加到 SharePoint 场。|1) 在 SharePoint 管理中心的“系统设置”组中，单击“管理此场中的服务器”********。<br /><br /> 2) 确认新的服务器是否已添加且状态是否正确。<br /><br /> 3) 要从 WFE 角色中删除此服务器，请单击 "**管理服务器上的服务**" 并停止服务 " **Microsoft SharePoint Foundation Web 应用程序**"。|
|安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 用于 SharePoint 2010 产品的外接程序。|有几种方法可安装外接程序。 以下步骤使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装向导。 有关安装外接程序的详细信息，请参阅[安装或卸载用于 sharepoint 的 Reporting Services 外接程序 &#40;sharepoint 2010 和 sharepoint 2013&#41;](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)。 运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装：<br /><br /> 1) 在“设置角色”页上，选择“SQL Server 功能安装”********<br /><br /> 2) 在 "**功能选择**" 页上，选择 " **Reporting Services 用于 SharePoint 产品的外接程序**"<br /><br /> 3) 在接下来的几个页面上单击 "**下一步**" 以完成安装选项。<br /><br /> 有关安装 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的详细信息，请参阅 [安装适用于 SharePoint 2010 的 Reporting Services SharePoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。|
|验证新服务器是否正常运行。|1) 在 SharePoint 管理中心的“系统设置”组中，单击“管理此场中的服务器”********。<br /><br /> 2) 验证列表中是否包含新的服务器。|
|更新您的 NLB 解决方案。|如果需要，更新您的硬件或软件的 NLB 环境，以便包括新的服务器。|

## <a name="see-also"></a>另请参阅
 [将 Web 或应用程序服务器添加到场 (Sharepoint server 2010) ](https://technet.microsoft.com/library/bb218968.aspx?missingurl=%2fen-us%2flibrary%2fe1aeaddf-6ee4-43a9-82b7-db20b68c71db\(Office.14\)) [配置服务 (sharepoint server 2010) ](https://technet.microsoft.com/library/ee794878.aspx)


