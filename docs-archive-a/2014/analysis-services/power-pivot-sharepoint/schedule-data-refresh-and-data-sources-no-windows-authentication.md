---
title: 计划数据刷新和不支持 Windows 身份验证的数据源 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d8d875bc-7823-46b7-a939-867cefd4de12
author: minewiskan
ms.author: owend
ms.openlocfilehash: 63e37dec6f334395c0c1812c6f76d750c16c53ee
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587018"
---
# <a name="schedule-data-refresh-and-data-sources-that-do-not-support-windows-authentication-powerpivot-for-sharepoint"></a>计划数据刷新和不支持 Windows 身份验证的数据源 (PowerPivot for SharePoint)
  本主题介绍当数据源**不**支持 Windows 身份验证时，让 PowerPivot for SharePoint 计划数据刷新能够使用该数据源的工作流。 例如 Oracle 或 IDM DB2 数据源。 本主题中的图示和步骤引用 Oracle 数据源，但此工作流也适用于其他数据源。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 &#124; SharePoint 2013。|  
  
 **概述：** 创建两个安全存储区目标应用程序。 将第 1 个目标应用程序 (PowerPivotDataRefresh) 配置为使用 Windows 凭据。 针对诸如 Oracle 数据库等不支持 Windows 身份验证的数据源，使用这些凭据配置第 2 个目标应用程序。 对于无人参与的数据刷新帐户，第 2 个目标应用程序也将使用第 1 个目标应用程序。  
  
 ![as_powerpivot_refresh_no_windows_auth](../media/as-powerpivot-refresh-no-windows-auth.gif "as_powerpivot_refresh_no_windows_auth")  
  
-   **(1) PowerPivotDatarefresh：** 此安全存储区目标应用程序 ID 使用 Windows 身份验证进行设置。  
  
-   **(2) OracleAuthentication：** 此安全存储区目标应用程序 ID 使用 Oracle 凭据进行设置。  
  
-   ** (3) **对于**无人参与的数据刷新帐户**，PowerPivot 服务应用程序配置为使用目标应用程序 "PowerPivotDataRefresh"。  
  
-   **(4)** PowerPivot 工作簿使用 Oracle 数据。 工作簿刷新设置指定数据源连接以使用凭据的目标应用程序 **(2)** 。  
  
## <a name="prerequisites"></a>先决条件  
  
-   存在 PowerPivot 服务应用程序。  
  
-   存在 Secure Store Service 应用程序。  
  
-   存在带有 PowerPivot 数据模型的 Excel 工作簿。  
  
## <a name="to-create-a-target-application-id-that-uses-windows-authentication"></a>创建使用 Windows 身份验证的目标应用程序 ID  
  
1.  在 SharePoint 管理中心中，单击 "**管理服务应用程序**"。  
  
2.  单击 Secure Store Service 应用程序的名称。  
  
3.  在 "**管理**" 页上，单击 "**新建**"。 ![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application")  
  
4.  在 **“创建新的安全存储区目标应用程序”** 页上，配置下列值：  
  
    -   **目标应用程序 ID：** PowerPivotDataRefresh。  
  
    -   **显示名称：** PowerPivotDataRefresh。  
  
    -   **联系人电子邮件：** ？  
  
    -   **目标应用程序类型：** 组。  
  
    -   **目标应用程序页 URL：** 无。  
  
5.  单击“下一步”。  
  
6.  在“凭据”页上，将 **“Windows 用户名”** 和 **“Windows 密码”** 这两个字段的名称和类型都保留为默认值。  
  
7.  单击“下一步”。  
  
8.  在 **“成员资格设置”** 页上，添加至少一个 **“目标应用程序管理员”** ，然后添加需要目标应用程序的访问权限的成员。  
  
9. 单击“确定”  。  
  
10. 一个新的目标应用程序 ID 会添加到列表中。 选择目标应用程序 ID，然后单击 "**设置凭据**"![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key")。  
  
11. 键入 Windows 用户名和 Windows 密码，然后单击 **“确定”**。  
  
## <a name="to-create-a-target-application-id-that-uses-oracle-credentials"></a>创建使用 Oracle 凭据的目标应用程序 ID  
  
1.  在 SharePoint 管理中心中，单击 "**管理服务应用程序**"。  
  
2.  单击 Secure Store Service 应用程序的名称。  
  
3.  在 "**管理**" 页上，单击 "**新建**![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application")"。  
  
4.  在 **“创建新的安全存储区目标应用程序”** 页上，配置下列值：  
  
    -   **目标应用程序 ID：** OracleAuthentication。  
  
    -   **显示名称：** OracleAuthentication。  
  
    -   **联系人电子邮件：** ？  
  
    -   **目标应用程序类型：** 组。  
  
    -   **目标应用程序页 URL：** 无。  
  
5.  单击“下一步”。  
  
6.  在 "**凭据**" 页上，将第一个字段名称更改为 `Oracle User ID` ，并将**字段类型**更改为 `User Name` 。  
  
     将第二个字段名称更改为 `Oracle Password` ，并将**字段类型**更改为 `Password` 。  
  
7.  单击“下一步”。  
  
8.  在 **“成员资格设置”** 页上，添加至少一个 **“目标应用程序管理员”** ，然后添加需要目标应用程序的访问权限的成员。  
  
9. 单击“确定”  。  
  
10. 一个新的目标应用程序 ID 会添加到列表中。 选择目标应用程序 ID，然后单击 "**设置凭据**"![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key")。  
  
11. 键入 Oracle 用户 ID 和 Oracle 密码，然后单击 **“确定”**。  
  
 有关详细信息，请参阅[使用 SQL Server Authentication (SharePoint Server 2013) ](https://technet.microsoft.com/library/gg298949.aspx) (中的 "为 SQL Server 身份验证创建目标应用程序" 部分 https://technet.microsoft.com/library/gg298949.aspx) 。  
  
## <a name="to-configure-the-powerpivot-service-application"></a>若要配置 PowerPivot 服务应用程序  
  
1.  在 SharePoint 管理中心中，单击“管理服务应用程序”。  
  
2.  单击 PowerPivot 服务应用程序的名称，例如 "默认 PowerPivot 服务应用程序"。  
  
3.  在“操作”节中，单击 **“配置服务应用程序设置”** 。  
  
4.  在 "**数据刷新**" 部分中，将**PowerPivot 无人参与的数据刷新帐户**设置为， `PowerPivotDataRefresh` 然后单击 **"确定"**。  
  
     ![as_powerpivot_refresh_new_refresh_acount](../media/as-powerpivot-refresh-new-refresh-acount.gif "as_powerpivot_refresh_new_refresh_acount")  
  
## <a name="to-configure-the-workbook"></a>配置工作簿  
  
1.  在 PowerPivot 库中浏览到工作簿，然后单击 "**管理数据刷新**"![as_powerpivot_refresh_manage_reresh](../media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh")。  
  
2.  如果出现 **“数据刷新历史记录”** 页，单击 **“配置计划”**。  
  
3.  单击 **“启用”** 。  
  
4.  单击 **“也尽快刷新”**。  
  
5.  在 **“凭据”** 节中，单击 **“使用管理员配置的数据刷新帐户”**。  
  
6.  清除 **“所有数据源”**。  
  
7.  针对使用 Oracle 数据的数据源，选择 **“刷新”** 。 在 Microsoft Excel 的 **“数据”**-&gt; **“连接”**-&gt; **“属性”** 菜单中，可以更改此数据源的名称。  
  
8.  在数据源下，选择 **“使用默认计划”**。  
  
9. 选择 **“使用在 Secure Store Service (SSS) 中保存的凭据连接以登录数据源。在 SSS ID 框中输入用于查找凭据的 ID”**。  
  
10. 在 " **ID：** " 框中，键入 `OracleAuthentication` 。  
  
11. 单击“确定”  。  
  
     如果出现类似以下的错误消息： `The provided Secure Store target application is either incorrectly configured or does not exist`。  
  
     通常有两个解决方案：  
  
    -   确认目标应用程序 ID 正确无误。  
  
    -   确认已为该目标应用程序设置凭据。  
  
## <a name="to-verify-data-refresh-with-the-new-authentication"></a>使用新身份验证信息来验证数据刷新  
 单击 **“确定”** 时，将出现 **“刷新历史记录”** 页。 数分钟内，刷新历史记录中应会出现一个新项，因为在上述步骤中选中了 **“也尽快刷新”**。 **PowerPivot 数据刷新计时器作业**的计时器作业默认值是 1 分钟。 如果刷新历史记录中未出现新项，请等待数分钟，然后刷新浏览器。 如果仍未出现新项，请确认计时器作业的当前值。  
  
## <a name="more-information"></a>更多信息  
  
-   [配置 SharePoint 2013 中的 Secure Store Service](https://technet.microsoft.com/library/ee806866.aspx)。  
  
-   请参阅利用 SharePoint 2013 的 PowerPivot 数据刷新的 "计划的数据刷新" 部分[，并 SQL Server 2012 SP1 (Analysis Services) ](https://msdn.microsoft.com/library/jj879294.aspx#bkmk_windows_auth_interactive_data_refresh)。  
  
  
