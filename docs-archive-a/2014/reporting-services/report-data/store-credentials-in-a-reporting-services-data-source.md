---
title: 在 Reporting Services 数据源中存储凭据 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fccf8669d1f39d19a26b443ffcead8e86db66a34
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588924"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>在 Reporting Services 数据源中存储凭据
  可以配置存储的凭据， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 报表服务器可使用这些凭据来访问报表的外部数据。 如果报表在无人参与的状态下运行，则使用存储凭据，例如将报表作为电子邮件发布的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 订阅。 计划或触发报表处理时，报表服务器将检索和使用这些凭据。 本主题向你说明了为本机模式下和 SharePoint 模式下的报表服务器配置存储凭据的过程。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式|

 **本主题内容：**

-   [为特定于报表的数据源配置存储的凭据 (纯模式) ](#bkmk_stored_credentials_data_source_native)

-   [为特定于报表的数据源配置存储的凭据（SharePoint 模式）](#bkmk_stored_credentials_data_source_sharepoint)

-   [为共享数据源配置存储的凭据 (纯模式) ](#bkmk_stored_credentials_shared_data_source_native)

-   [为共享数据源配置存储凭据（SharePoint 模式）](#bkmk_stored_credentials_shared_data_source_sharepoint)

##  <a name="security-policy-requirements-for-stored-credentials"></a><a name="bkmk_top"></a> 存储凭据的安全策略要求
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") 要求为报表服务器上的以下其中一项安全策略配置用于存储凭据的帐户。 建议使用环境要求的最低级别权限来选择策略。

1.  **允许本地登录**。 有关详细信息，请参阅 [允许在本地登录](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx)。

2.  **作为批处理作业登录**。 有关详细信息，请参阅 [作为批处理作业登录](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx)。

3.  有关策略的一般信息，请参阅 [在组策略对象上编辑安全设置](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx)。

##  <a name="configure-stored-credentials-for-a-report-specific-data-source-native-mode"></a><a name="bkmk_stored_credentials_data_source_native"></a> 为特定于报表的数据源配置存储的凭据（本机模式）

1.  在本机模式下的报表管理器中，浏览至包含该报表的文件夹。 单击![报表管理器中 ssrs 项](../media/ssrs-report-manager-item-context-menu.png "ssrs 项目报表管理器中的上下文菜单")的上下文菜单上下文菜单。

2.  单击“管理” **** ，然后单击“数据源” ****。

3.  选择 **“自定义数据源”**。

4.  在“数据源类型” **** 列表中，选择处理数据源的数据所用的数据处理扩展。

5.  对于 "**连接字符串**"，指定 Report Server 用于连接到数据源的连接字符串。 下面的示例说明了用于连接到数据库的连接字符串 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] ：

    ```
    data source=<servername>;initial catalog=AdventureWorks2012
    ```

6.  对于“连接方法” ****，选择“安全存储在报表服务器中的凭据” ****。

7.  键入用户名和密码。

    -   如果帐户是 Windows 域用户帐户，请按以下格式指定该帐户： \<domain> \\<帐户 \> ，然后选择 "在与**数据源建立连接时用作 Windows 凭据"。**

    -   如果用户名和密码是数据库凭据，请不要选择 **“在与数据源建立连接时用作 Windows 凭据”**。 如果数据库服务器支持模拟或委托，则可以选择 **“与数据源建立连接之后模拟经过身份验证的用户”**。

8.  单击“**应用**”。

     ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [适用于存储凭据的安全策略要求](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-report-specific-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_data_source_sharepoint"></a>在 SharePoint 模式 (为特定于报表的数据源配置存储的凭据) 

1.  浏览到包含该报表的文档库，然后单击打开菜单 ![ssrs 项的文档库上下文菜单](../media/ssrs-sharepoint-item-context-menu.png "ssrs 项的文档库上下文菜单")。

2.  单击第二个打开菜单 ![ssrs 项的文档库上下文菜单](../media/ssrs-sharepoint-item-context-menu.png "ssrs 项的文档库上下文菜单")，然后单击“管理数据源”****。

3.  单击想要使用存储的凭据进行配置的“自定义” **** 数据源的名称。

4.  在“数据源类型” **** 列表中，选择处理数据源的数据所用的数据处理扩展。

5.  对于 "**连接字符串**"，指定 Report Server 用于连接到数据源的连接字符串。 下面的示例说明了用于连接到数据库的连接字符串 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] ：

    ```
    data source=<servername>;initial catalog=AdventureWorks2012
    ```

6.  对于“凭据” ****，选择“存储的凭据” ****。

7.  键入**用户名**和**密码**。

    -   如果帐户是 Windows 域用户帐户，请按以下格式指定该帐户： \<domain> \\<帐户 \> ，然后选择 "在与**数据源建立连接时用作 Windows 凭据"。**

    -   如果用户名和密码是数据库凭据，请勿选择“用作 Windows 凭据” ****。 如果数据库服务器支持模拟或委托，则可以选择 "**设置此帐户的执行上下文**"。

8.  单击“确定”  。

     ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [适用于存储凭据的安全策略要求](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-shared-data-source-native-mode"></a><a name="bkmk_stored_credentials_shared_data_source_native"></a> 为共享数据源配置存储凭据（本机模式）

1.  在本机模式下的报表管理器中，浏览至共享数据源项。 ![共享数据源图标](../media/hlp-16datasource.png "共享数据源图标")

2.  单击![报表管理器中 ssrs 项](../media/ssrs-report-manager-item-context-menu.png "ssrs 项目报表管理器中的上下文菜单")的上下文菜单上下文菜单，然后单击 "**管理**"。

3.  在 "**数据源类型**" 列表中，指定用于处理数据源中数据的数据处理扩展插件。

4.  对于 "**连接字符串**"，指定 Report Server 用于连接到数据源的连接字符串。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议您不要在连接字符串中指定凭据。

     下面的示例演示用于连接到本地数据库的连接字符串 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] ：

    ```
    data source=<localservername>; initial catalog=AdventureWorks2012
    ```

5.  键入用户名和密码。

    -   如果帐户是 Windows 域用户帐户，请按以下格式指定该帐户： \<domain> \\<帐户 \> ，然后选择 "在与**数据源建立连接时用作 Windows 凭据"。**

    -   如果用户名和密码是数据库凭据，请不要选择 **“在与数据源建立连接时用作 Windows 凭据”**。 如果数据库服务器支持模拟或委托，则可以选择 **“与数据源建立连接之后模拟经过身份验证的用户”**。

6.  单击“**应用**”。

     ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [适用于存储凭据的安全策略要求](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-shared-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a>在 SharePoint 模式 (为共享数据源配置存储的凭据) 

1.  在文档库中，浏览到共享数据源项。![共享数据源图标](../media/hlp-16datasource.png "共享数据源图标")

2.  单击上下文菜单 ![ssrs 项的文档库上下文菜单](../media/ssrs-sharepoint-item-context-menu.png "ssrs 项的文档库上下文菜单")，然后单击第二个上下文菜单 ![ssrs 项的文档库上下文菜单](../media/ssrs-sharepoint-item-context-menu.png "ssrs 项的文档库上下文菜单")。

3.  单击“编辑数据源定义” ****。

4.  在 "**数据源类型**" 列表中，指定用于处理数据源中数据的数据处理扩展插件。

5.  对于 "**连接字符串**"，指定 Report Server 用于连接到数据源的连接字符串。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议您不要在连接字符串中指定凭据。

     下面的示例演示用于连接到本地数据库的连接字符串 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] ：

    ```
    data source=<localservername>; initial catalog=AdventureWorks2012
    ```

6.  键入用户名和密码。

    -   如果该帐户是 Windows 域用户帐户，请按以下格式指定该帐户： \<domain> \\<帐户 \> ，然后选择 "用作**Windows 凭据"。**

    -   如果用户名和密码是数据库凭据，请勿选择“用作 Windows 凭据” ****。 如果数据库服务器支持模拟或委托，则可选择 **Set Execution context to this account**。

7.  单击“确定” 。

     ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于返回页首链接的箭头图标") [适用于存储凭据的安全策略要求](#bkmk_top)

## <a name="see-also"></a>另请参阅
 [为报表数据源指定凭据和连接信息](../../integration-services/connection-manager/data-sources.md) [&#40;报表管理器&#41;](configure-data-source-properties-for-a-report-report-manager.md) [创建、删除或修改共享数据源 &#40;报表管理器](../create-delete-or-modify-a-shared-data-source-report-manager.md) [&#41;&#40;报表管理器](../data-sources-properties-page-report-manager.md)[新建数据源 "页](../new-data-source-page-report-manager.md)&#41;&#40;报表管理器


