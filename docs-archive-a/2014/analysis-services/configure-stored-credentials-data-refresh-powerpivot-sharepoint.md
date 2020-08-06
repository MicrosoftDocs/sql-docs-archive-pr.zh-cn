---
title: 为 PowerPivot 数据刷新配置存储的凭据 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 987eff0f-bcfe-4bbd-81e0-9aca993a2a75
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5a1350c5d776891397401e9d3127b7849281b106
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579231"
---
# <a name="configure-stored-credentials-for-powerpivot-data-refresh-powerpivot-for-sharepoint"></a>为 PowerPivot 数据刷新配置存储的凭据 (PowerPivot for SharePoint)
  只要您在 Secure Store Service 中创建一个目标应用程序来存储要使用的凭据，PowerPivot 数据刷新作业就可以在任何 Windows 用户帐户下运行。 同样，如果您想要提供的数据库登录名不同于最初用于导入 PowerPivot for Excel 中的数据的数据库登录名，则可以将这些凭据映射到 Secure Store Service 目标应用程序，然后在数据刷新计划中指定该目标应用程序。  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 在您按照本主题中的说明执行后，将能够使用 PowerPivot 数据刷新计划页中的以下凭据选项：  
  
 ![SSAS_PowerPivotDataRefreshCreds_Stored](media/ssas-powerpivotdatarefreshcreds-stored.gif "SSAS_PowerPivotDataRefreshCreds_Stored")  
  
 本主题介绍如何设置用于在 SharePoint 2010 场中进行 PowerPivot 数据刷新的用户名和密码。 您必须首先已启用 Secure Store Service 并生成了主密钥，之后才能采用这些步骤。 有关详细信息，请参阅[通过 SharePoint 2010 进行 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 本主题包含以下各节：  
  
 [配置用于数据刷新的任何 Windows 帐户](#configAny)  
  
 [配置用于访问外部或第三方数据源的预定义帐户](#config3rd)  
  
 如果在配置或使用数据刷新时遇到问题，请参考 TechNet wiki 上的[PowerPivot 数据刷新故障排除](https://go.microsoft.com/fwlink/?LinkID=223279)页，了解可能的解决方法。  
  
##  <a name="configure-any-windows-account-for-data-refresh"></a><a name="configAny"></a>配置用于数据刷新的任何 Windows 帐户  
 在某一 SharePoint 用户定义数据刷新计划时，该用户必须指定执行数据刷新所基于的用户标识。 有关的选项包括选择 PowerPivot 无人参与的数据刷新帐户，输入其 Windows 域用户帐户，以及输入对数据刷新目的有效的某个其他 Windows 用户帐户。 本节中的步骤针对最后一个选项：指定某个其他 Windows 帐户。  
  
 如果您想要采用其他方法，来代替使用 PowerPivot 无人参与的数据刷新帐户（可用于 SharePoint 上的所有 PowerPivot 用户）或者工作簿所有者的凭据，则可以选择此方法。 例如，您可能要建立可用于不同工作组的一系列数据刷新帐户，以便帮助您在组织级别跟踪和管理数据刷新活动。  
  
> [!IMPORTANT]  
>  使用此目标应用程序（及其存储的凭据）的人员和应用程序必须列为此应用程序的成员。 您必须添加将使用此目标应用程序的每个 PowerPivot 服务应用程序的标识、您的 Windows 帐户，以及将在其数据刷新计划中指定此目标应用程序的人员的组或用户帐户。 您可以在创建目标应用程序时指定所有这些帐户。 如果您不知道将需要访问此应用程序的所有用户和组帐户，可以在创建目标应用程序以后再添加它们。  
  
 为数据刷新配置存储的凭据这一过程分为 4 个部分：  
  
-   创建存储凭据的目标应用程序。  
  
-   对该帐户授予“参与讨论”权限。  
  
-   授予该帐户读取权限以便在数据刷新过程中访问外部数据源。  
  
-   确认当您在数据刷新计划中指定此目标应用程序时数据刷新将生效。  
  
### <a name="step-1-create-a-target-application"></a>步骤 1：创建目标应用程序  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。  
  
2.  单击 " **Secure Store Service**"。  
  
3.  在 "管理目标应用程序" 中，单击 "**新建**"。  
  
4.  在“目标应用程序 ID”中，键入文本字符串。 此字符串必须唯一，但是还应该容易记住。 每当用户希望使用存储在此应用程序中的凭据时，将在数据刷新计划页中键入此字符串。  
  
5.  在“显示名称”中，输入一个说明性名称。 此名称仅用于显示目的。 不会在数据刷新计划中将其用于指定目标应用程序。  
  
6.  在“联系人电子邮件”中，键入您的电子邮件地址。  
  
7.  在 "目标应用程序类型" 中选择 "**组**"。  
  
    > [!IMPORTANT]  
    >  选择“组”帐户类型是必需的，因为这将允许您指定请求对凭据进行访问的所有用户和服务帐户。 对于每个请求，PowerPivot 系统服务都会确认请求者是否为目标应用程序的成员。  
  
8.  跳过“目标应用程序页 URL”。 PowerPivot 数据刷新不会使用它。  
  
9. 单击“下一步”。  
  
10. 在 "**为安全存储目标应用程序指定凭据字段**" 页上，接受默认值。 字段名称和类型应该是 Windows 用户名和 Windows 密码。  
  
11. 单击“下一步”。  
  
12. 在“目标应用程序管理员”中，指定应该对目标应用程序设置具有管理权限（例如，能够从成员列表添加或删除帐户）的 SharePoint 用户的 Windows 域用户帐户。  
  
13. 在“成员”中，添加以下用户和组帐户：  
  
    1.  作为创建该应用程序的人员，将您的 Windows 用户帐户添加到“成员”列表中。  
  
    2.  添加 PowerPivot 服务应用程序的应用程序池标识，以便它可以在数据刷新计划运行时检索凭据。 若要查看应用程序池标识，请在 "**管理服务应用**程序" 中，通过单击名称旁边的空白区域选择 PowerPivot 服务应用程序 (这将选择行) ，然后单击 "**属性**"。 此页上显示的安全帐户是要作为目标应用程序的成员来添加的帐户。  
  
    3.  在数据刷新计划中添加将输入此目标应用程序的 Windows 用户和组帐户。  
  
14. 单击“确定”  。  
  
15. 选择刚创建的目标应用程序，单击向下箭头并选择 "**设置凭据"。**  
  
16. 在“凭据所有者”中，请注意凭据所有者的列表是只读的。 对凭据具有所有权的帐户是目标应用程序的成员。 若要添加或删除凭据所有者，则必须在目标应用程序成员列表中添加或删除帐户。  
  
     在“Windows 用户名”和“Windows 密码”中，键入将用于运行数据刷新的 Windows 用户帐户的凭据。  
  
17. 单击“确定”  。  
  
###  <a name="step-2-grant-contribute-permissions-to-the-account"></a><a name="bkmk_grant"></a>步骤2：向帐户授予 "参与讨论" 权限  
 在您可以使用存储的凭据之前，对于使用该帐户的任何 PowerPivot 工作簿，必须授予“参与讨论”权限。 此权限级别是从库中打开工作簿、然后在刷新数据后将其保存回库中所必需的。  
  
 分配权限这个步骤将由网站集管理员来执行。 SharePoint 权限可以在根网站集或其下的任何级别分配，包括单独的文档和项。 设置权限的方式将因您所需的粒度而异。 下面的步骤说明可用于授予权限的一个方法。  
  
1.  在 SharePoint 站点上的 "站点操作" 中，单击 "**网站权限**"。  
  
2.  单击“授予权限”  。  
  
3.  在“选择用户”中，键入您在目标应用程序中指定的 Windows 域用户帐户的名称。  
  
4.  在 "授予权限" 中，选择 "**直接授予用户权限**"。  
  
5.  选择 "**参与**"，然后单击 **"确定"**。  
  
###  <a name="step-3-grant-read-permissions-to-access-external-data-sources-used-in-data-refresh"></a><a name="bkmk_dbread"></a>步骤3：授予读取权限以便访问在数据刷新中使用的外部数据源  
 在将数据导入到某一 PowerPivot 工作簿时，与外部数据的连接常常基于可信连接或者使用当前用户标识来连接到数据源的模拟连接。 只有在当前用户有权读取其导入的数据时，这些连接类型才有效。  
  
 在数据刷新方案中，现在将重复使用过去用于导入数据的相同连接字符串来刷新数据。 如果该连接字符串假定当前用户（例如，包含 Integrated_Security=SSPI 的字符串），则 PowerPivot 系统服务会将在目标应用程序中指定的用户标识作为当前用户传递。 只有在帐户对外部数据源具有读取权限时，此连接才会成功。  
  
 因此，您必须向该帐户授予对数据刷新过程中使用的所有外部数据源的只读权限。  
  
 如果您是组织中使用的数据源的管理员，则可以创建一个登录名，然后分配必需的权限。 否则，您必须与数据所有者联系并且提供帐户信息。 请确保指定映射到目标应用程序的 Windows 域用户帐户。 这是你在本主题的 "步骤1：创建目标应用程序" 中指定的帐户。  
  
###  <a name="step-4-verify-account-availability-in-data-refresh-configuration-pages"></a><a name="bkmk_verify"></a>步骤4：在数据刷新配置页中验证帐户可用性  
  
1.  打开包含 PowerPivot 数据的已发布工作簿的数据刷新配置页。 有关如何打开该页的说明，请参阅[计划数据刷新 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)。  
  
2.  验证是否在 "数据刷新配置" 页中启用了 "**使用保存在 Secure Store Service (SSS) 登录数据源**" 选项，然后输入目标应用程序的名称。  
  
3.  选中 "**也尽快刷新**" 复选框，然后单击 **"确定"**。  
  
4.  在包含该工作簿的库中，选择该工作簿，单击右侧显示的向下箭头，然后选择 "**管理 PowerPivot 数据刷新**"。 如果数据刷新作业正在返回大量数据，您可能需要等待几分钟。  
  
 如果发生错误，你可以在数据刷新历史记录页中单击 "**配置计划**"，尝试使用不同的凭据。 您还可能需要检查原始工作簿中的数据源连接信息，以便查看在数据刷新过程中使用的连接字符串。 该连接字符串将提供与您可用于解决问题的服务器位置和数据库有关的信息。  
  
 有关故障排除的详细信息，请参阅 TechNet Wiki 上的[PowerPivot 数据刷新故障排除](https://go.microsoft.com/fwlink/p/?LinkID=223279)。  
  
##  <a name="configure-a-predefined-account-for-accessing-external-or-third-party-data-sources"></a><a name="config3rd"></a>配置用于访问外部或第三方数据源的预定义帐户  
 数据库服务器通常附带有自己的身份验证方法。 如果 PowerPivot 工作簿要求提供数据库凭据以便在数据刷新期间访问外部数据源，则可以为这些凭据创建一个目标应用程序 ID，然后在“计划数据刷新”页的“数据源”部分指定该目标应用程序。  
  
 仅当您希望为用户提供选项，允许其覆盖 PowerPivot 工作簿中已嵌入的数据库凭据时，才需要此步骤。  
  
 此步骤仅适用于连接字符串已包含用户名和密码的情况。 请注意，在连接字符串中具有凭据不大常见，因此，您能否使用此选项有时候会受到限制。 在大多数情况下，如果您在使用数据库身份验证来连接到数据源，则在连接字符串中将仅具有用户 ID 和密码。 有关如何检查连接字符串以查看它是否包括用户 ID 和密码的详细信息，请参阅[PowerPivot 数据刷新与 SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)中的 "授予创建计划和访问外部数据的权限" 一节。  
  
1.  在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。  
  
2.  单击 " **Secure Store Service**"。  
  
3.  在 "管理目标应用程序" 中，单击 "**新建**"。  
  
4.  在“目标应用程序 ID”中，键入文本字符串。 此字符串必须唯一，但是还应该容易记住。 每当用户希望使用存储在此应用程序中的凭据时，将在数据刷新计划页中键入此字符串。  
  
5.  在“显示名称”中，输入一个说明性名称。 此名称仅用于显示目的。 不会在数据刷新计划中将其用于指定目标应用程序。  
  
6.  在“联系人电子邮件”中，键入您的电子邮件地址。  
  
7.  在 "目标应用程序类型" 中选择 "**组**"。  
  
8.  跳过“目标应用程序页 URL”。 PowerPivot 数据刷新不会使用它。  
  
9. 单击“下一步”。  
  
10. 在 "**为安全存储目标应用程序指定凭据字段**" 页中，仅在数据源使用 Windows 身份验证时才接受默认值。 否则，选择对您的数据源有效的字段类型，然后编辑字段名称以便匹配您选择的类型。  
  
     例如，您可以为字段名称指定 SQL Server 用户名和 SQL Server 用户密码，然后为字段类型选择用户名和密码。  
  
11. 单击“下一步”。  
  
12. 在“目标应用程序管理员”中，指定应该对应用程序设置具有管理权限的 SharePoint 用户的 Windows 域用户帐户。  
  
13. 在“成员”中，添加以下用户和组帐户：  
  
    1.  作为创建该应用程序的人员，将您的 Windows 用户帐户添加到“成员”列表中。  
  
    2.  添加将使用该目标应用程序以访问其存储的凭据的每个 PowerPivot 服务应用程序的应用程序池标识。 若要查看标识，请在 "**管理服务应用程序**" 中，通过单击名称旁边的空白区域选择 PowerPivot 服务应用程序 (这将选择行) ，然后单击 "**属性**"。 此页上显示的安全帐户是您想要作为目标应用程序的成员来添加的帐户。  
  
    3.  在数据刷新计划页的数据源部分中添加将输入此目标应用程序的 Windows 用户和组帐户。  
  
14. 单击“确定”  。  
  
15. 选择刚创建的目标应用程序，单击向下箭头并选择 "**设置凭据"。**  
  
16. 输入将用于连接到数据源的凭据（例如，SQL Server 登录名的用户名和密码）。  
  
17. 单击“确定”。  
  
## <a name="see-also"></a>另请参阅  
 [计划数据刷新 &#40;PowerPivot for SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [使用 SharePoint 2010 进行 PowerPivot 数据刷新](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
