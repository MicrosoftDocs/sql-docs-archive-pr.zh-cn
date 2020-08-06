---
title: 创建报表数据源 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9205eac497fc047b471f5b80becec36495474d88
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691961"
---
# <a name="create-a-report-data-source"></a>创建报表数据源
  为了 Power View 可连接到多维模型，您必须在 SharePoint 库中创建一个共享的报表数据源定义（也称为 .rsds 文件）。 该 .rsds 文件指定用于连接到多维模型的 Analysis Services 服务器实例、连接类型、连接字符串以及凭据的名称。 当用户单击 .rsds 时，将在浏览器中打开新的空白 Power View 报表（.rdlx 文件）。  
  
 为了创建 .rsds 连接，您必须安装了 SQL Server 2012（或更高版本）Reporting Services 和用于 SharePoint 2010 或 SharePoint 2013 的 Reporting Services 外接程序。  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>创建到多维模型的报表数据源 (.rsds) 连接  
 在开始之前，您需要知道：  
  
-   在多维模式下运行的 Analysis Services 服务器实例的名称。  
  
-   要连接到的多维数据库的名称。  
  
-   多维数据集的名称（如果存在多个多维数据集）。  
  
-   （可选）透视名称。  
  
-   （可选）区域设置标识符。  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>创建共享报表数据源 (.rsds) 文件 (SharePoint 2010)  
  
1.  在库功能区上单击 **“文档”** 选项卡。  
  
2.  单击 "**新建文档**" "  >  **报表数据源**"。  
  
    > [!NOTE]  
    >  如果在菜单上没有看到 **“报表数据源”** 项，说明尚未启用此库的报表数据源内容类型。 有关详细信息，请参阅[将报表服务器内容类型添加到库 &#40;Reporting Services 在 SharePoint 集成模式下&#41;" ](../../reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
3.  在 **“数据源属性”** 页上，在 **“名称”** 中键入连接 .rsds 文件的名称。  
  
4.  在 **“数据源类型”** 中，选择 **“Power View 的 Microsoft BI 语义模型”**。  
  
5.  在 **“连接字符串”** 中，指定 Analysis Services 服务器名称、数据库名称、多维数据集名称和所有可选设置。  
  
     连接字符串： `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'`  
  
    > [!NOTE]  
    >  如果有多个多维数据集，必须指定多维数据集名称。  
  
     （可选）多维数据集可以有透视，这些透视为用户提供一个选择视图，其中在客户端上只能看到某些维度和/或度量值组。 若要指定透视，请输入透视名称作为 Cube 属性的值： `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>'`  
  
     （可选）多维数据集可以具有为模型内各种语言指定的元数据和数据翻译。 若要查看 (数据和元数据的翻译) 需要将 "区域设置标识符" 属性添加到连接字符串：`Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'; Locale Identifier=<identifier number>`  
  
6.  在 **“凭据”** 中，指定报表服务器如何获取访问外部数据源的凭据。  
  
    -   若要使用打开报表的用户凭据访问数据，请选择“Windows 身份验证(集成)”****。 如果 SharePoint 站点或场使用窗体身份验证或通过可信帐户连接至报表服务器，请不要选择此选项。 若要为此报表计划订阅或数据处理，请不要选择此选项。 如果您的域启用了 Kerberos 身份验证或者数据源与报表服务器位于同一台计算机上，则此选项最为有效。 如果未启用 Kerberos 身份验证，则只能将 Windows 凭据传递到另一台计算机。 也就是说，如果外部数据源位于需要另行连接的其他计算机上，则会出现错误而不会获得期望的数据。  
  
    -   若要使用户在每次运行报表时都输入其凭据，请选择 **“凭据提示”** 。 若要为此报表计划订阅或数据处理，请不要选择此选项。  
  
    -   若要使用一组凭据访问数据，请选择 **“已存储凭据”** 。 凭据在存储之前是加密的。 您可以选择用于确定如何对已存储凭据进行身份验证的选项。 如果已存储的凭据属于 Windows 用户帐户，请选择“用作 Windows 凭据”。 如果要设置数据库服务器的执行上下文，请选择 **“设置此帐户的执行上下文”** 。  
  
    -   如果在连接字符串中指定凭据，或者如果要使用最低特权帐户运行报表，请选择“不需要提供凭据”****。  
  
7.  单击 **“测试连接”** 以进行验证。  
  
8.  如果您想要数据源处于活动状态，则选择 **“启用此数据源”** 。 如果配置了数据源但该数据源未处于活动状态，则在用户尝试创建报表时，将会收到错误消息。  
  
  
