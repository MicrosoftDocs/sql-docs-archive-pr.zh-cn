---
title: 配置 PowerPivot 服务帐户 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
author: minewiskan
ms.author: owend
ms.openlocfilehash: aac841c3f88d8c43680d1414a50687e9de1d5a3c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588710"
---
# <a name="configure-powerpivot-service-accounts"></a><span data-ttu-id="f92e8-102">配置 PowerPivot 服务帐户</span><span class="sxs-lookup"><span data-stu-id="f92e8-102">Configure PowerPivot Service Accounts</span></span>
  <span data-ttu-id="f92e8-103">[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装包括支持服务器操作的两个服务。</span><span class="sxs-lookup"><span data-stu-id="f92e8-103">A [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installation includes two services that support server operations.</span></span> <span data-ttu-id="f92e8-104">\*\*SQL Server Analysis Services (powerpivot) \*\*服务是一种 Windows 服务，它在应用程序服务器上提供 PowerPivot 数据处理和查询支持。</span><span class="sxs-lookup"><span data-stu-id="f92e8-104">The **SQL Server Analysis Services (PowerPivot)** service is a Windows service that provides PowerPivot data processing and query support on an application server.</span></span> <span data-ttu-id="f92e8-105">当您在 SharePoint 集成模式下安装 Analysis Services 时，在 SQL Server 安装期间始终为此服务指定登录帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-105">The login account for this service is always specified during SQL Server Setup when you install Analysis Services in SharePoint integrated mode.</span></span>  
  
 <span data-ttu-id="f92e8-106">必须为 PowerPivot 服务应用程序指定第二个帐户，这是在 SharePoint 场中基于应用程序池标识运行的共享 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="f92e8-106">A second account must be specified for the PowerPivot service application, a shared web service that runs under an application pool identity in a SharePoint farm.</span></span> <span data-ttu-id="f92e8-107">在您使用 PowerPivot 配置工具或 PowerShell 配置 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安装时指定此帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-107">This account is specified when you configure a [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] installation using either the PowerPivot Configuration tool or PowerShell.</span></span>  
  
 <span data-ttu-id="f92e8-108">每个服务都应该在专用帐户下运行，以便您可以在场中审核连接或启用 Kerberos 身份验证协议。</span><span class="sxs-lookup"><span data-stu-id="f92e8-108">Each service should run under a dedicated account so that you can audit connections or enable Kerberos authentication protocol in the farm.</span></span>  
  
 <span data-ttu-id="f92e8-109">一旦设置好服务帐户后，对上述帐户的任何更改都必须通过 SharePoint 管理中心进行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-109">Once the service accounts are set, any changes to either account must be made through SharePoint Central Administration.</span></span> <span data-ttu-id="f92e8-110">如果您使用替代工具（例如“服务”控制台应用程序、IIS 管理器或 SQL Server 配置管理器），则对于场中的数据库访问或者对于物理服务器上的本地文件访问，将不会更新权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-110">If you use alternative tools (such as the Services console application, IIS Manager, or SQL Server Configuration Manager), permissions will not be updated for database access in the farm or for local file access on the physical server.</span></span>  
  
 <span data-ttu-id="f92e8-111">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="f92e8-111">This topic contains the following sections:</span></span>  
  
 [<span data-ttu-id="f92e8-112">更新 SQL Server Analysis Services (PowerPivot) 实例的过期密码</span><span class="sxs-lookup"><span data-stu-id="f92e8-112">Update an expired password for SQL Server Analysis Services (PowerPivot) instance</span></span>](#bkmk_passwordssas)  
  
 [<span data-ttu-id="f92e8-113">更新 PowerPivot 服务应用程序的过期密码</span><span class="sxs-lookup"><span data-stu-id="f92e8-113">Update an expired password for the PowerPivot Service Application</span></span>](configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [<span data-ttu-id="f92e8-114">更改运行每个服务所基于的帐户</span><span class="sxs-lookup"><span data-stu-id="f92e8-114">Change the account under which each service runs</span></span>](#bkmk_newacct)  
  
 [<span data-ttu-id="f92e8-115">创建或更改 PowerPivot 服务应用程序的应用程序池</span><span class="sxs-lookup"><span data-stu-id="f92e8-115">Create or change the application pool for a PowerPivot service application</span></span>](#bkmk_appPool)  
  
 [<span data-ttu-id="f92e8-116">帐户要求和权限</span><span class="sxs-lookup"><span data-stu-id="f92e8-116">Account Requirements and Permissions</span></span>](#requirements)  
  
 [<span data-ttu-id="f92e8-117">故障排除：手动授予管理权限</span><span class="sxs-lookup"><span data-stu-id="f92e8-117">Troubleshooting: Grant Administrative Permissions Manually</span></span>](#updatemanually)  
  
 [<span data-ttu-id="f92e8-118">故障排除：解决由于管理中心或 SharePoint Foundation Web 应用程序服务密码过期而导致的 HTTP 503 错误</span><span class="sxs-lookup"><span data-stu-id="f92e8-118">Troubleshooting: Resolve HTTP 503 Errors Due to Expired Passwords for Central Administration or the SharePoint Foundation Web Application Service</span></span>](#expired)  
  
##  <a name="update-an-expired-password-for-sql-server-analysis-services-powerpivot-instance"></a><a name="bkmk_passwordssas"></a><span data-ttu-id="f92e8-119">更新 SQL Server Analysis Services (PowerPivot) 实例的过期密码</span><span class="sxs-lookup"><span data-stu-id="f92e8-119">Update an expired password for SQL Server Analysis Services (PowerPivot) instance</span></span>  
  
1.  <span data-ttu-id="f92e8-120">指向“开始”，单击 **“管理工具”**，再单击 **“服务”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-120">Point to Start, click **Administrative Tools**, and then click **Services**.</span></span> <span data-ttu-id="f92e8-121">双击 " \*\*SQL Server Analysis Services (PowerPivot) \*\*"。</span><span class="sxs-lookup"><span data-stu-id="f92e8-121">Double-click **SQL Server Analysis Services (PowerPivot)**.</span></span> <span data-ttu-id="f92e8-122">单击 **“登录”**，然后为该帐户输入新密码。</span><span class="sxs-lookup"><span data-stu-id="f92e8-122">Click **Log On**, and then enter the new password for the account.</span></span>  
  
2.  <span data-ttu-id="f92e8-123">在“管理中心”的“安全性”部分中，单击 **“配置托管帐户”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-123">In Central Administration, in the Security section, click **Configure managed accounts**.</span></span>  
  
3.  <span data-ttu-id="f92e8-124">单击 **“编辑”** 更改特定帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-124">Click **Edit** to change a specific account.</span></span>  
  
4.  <span data-ttu-id="f92e8-125">选择 **“立即更改密码”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-125">Select **Change password now**.</span></span>  
  
5.  <span data-ttu-id="f92e8-126">选择 **“将帐户密码设置为新值”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-126">Select **Set account password to new value**.</span></span> <span data-ttu-id="f92e8-127">在该托管帐户下运行的所有服务都将使用更新后的凭据。</span><span class="sxs-lookup"><span data-stu-id="f92e8-127">All services that run under the managed account will use the updated credentials.</span></span>  
  
##  <a name="update-an-expired-password-for-the-powerpivot-service-application"></a><a name="bkmk_passwordapp"></a><span data-ttu-id="f92e8-128">更新 PowerPivot 服务应用程序的过期密码</span><span class="sxs-lookup"><span data-stu-id="f92e8-128">Update an expired password for the PowerPivot Service Application</span></span>  
  
1.  <span data-ttu-id="f92e8-129">在“管理中心”的“安全性”部分中，单击 **“配置托管帐户”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-129">In Central Administration, in the Security section, click **Configure managed accounts**.</span></span>  
  
2.  <span data-ttu-id="f92e8-130">单击 **“编辑”** 更改特定帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-130">Click **Edit** to change a specific account.</span></span>  
  
3.  <span data-ttu-id="f92e8-131">选择 **“立即更改密码”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-131">Select **Change password now**.</span></span>  
  
4.  <span data-ttu-id="f92e8-132">选择 **“将帐户密码设置为新值”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-132">Select **Set account password to new value**.</span></span> <span data-ttu-id="f92e8-133">在该托管帐户下运行的所有服务都将使用更新后的凭据。</span><span class="sxs-lookup"><span data-stu-id="f92e8-133">All services that run under the managed account will use the updated credentials.</span></span>  
  
##  <a name="change-the-account-under-which-each-service-runs"></a><a name="bkmk_newacct"></a><span data-ttu-id="f92e8-134">更改运行每个服务所用的帐户</span><span class="sxs-lookup"><span data-stu-id="f92e8-134">Change the account under which each service runs</span></span>  
  
1.  <span data-ttu-id="f92e8-135">在“管理中心”的“安全性”部分中，单击 **“配置服务帐户”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-135">In Central Administration, in the Security section, click **Configure service accounts**.</span></span>  
  
2.  <span data-ttu-id="f92e8-136">选择\*\*\*\*“Windows 服务 - SQL Server Analysis Services”以更改 Analysis Services 服务帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-136">Select **Windows Service - SQL Server Analysis Services** to change the Analysis Services service account.</span></span>  
  
3.  <span data-ttu-id="f92e8-137">在 **“为此服务选择帐户”** 中，选择某个现有托管帐户或创建一个新帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-137">In **Select an account for this service**, choose an existing managed account or create a new one.</span></span> <span data-ttu-id="f92e8-138">该帐户必须是域用户帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-138">The account must be a domain user account.</span></span>  
  
4.  <span data-ttu-id="f92e8-139">选择 "**服务应用程序池-SharePoint Web 服务系统**" 以更改默认 PowerPivot 服务应用程序的应用程序池标识。</span><span class="sxs-lookup"><span data-stu-id="f92e8-139">Select **Service Application Pool - SharePoint Web Services System** to change the application pool identity of the default PowerPivot service application.</span></span> <span data-ttu-id="f92e8-140">根据配置您的安装的方式，可基于为 SharePoint 服务创建的现有服务应用程序池运行服务。</span><span class="sxs-lookup"><span data-stu-id="f92e8-140">Depending on how your installation was configured, the service might be running under an existing service application pool created for SharePoint services.</span></span> <span data-ttu-id="f92e8-141">默认情况下，PowerPivot 配置工具 **)  (Powerpivot 服务应用**程序将该服务注册为默认的 Powerpivot 服务应用程序。</span><span class="sxs-lookup"><span data-stu-id="f92e8-141">By default, the PowerPivot Configuration Tool registers the service as **Default PowerPivot Service Application (PowerPivot Service Application)**.</span></span>  
  
     <span data-ttu-id="f92e8-142">如果 SharePoint 管理员已手动配置该服务，则该服务最有可能具有自己的服务应用程序池。</span><span class="sxs-lookup"><span data-stu-id="f92e8-142">If the service was configured manually by a SharePoint administrator, the service most likely has its own service application pool.</span></span>  
  
5.  <span data-ttu-id="f92e8-143">在 **“为此服务选择帐户”** 中，选择某个现有托管帐户或创建一个新帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-143">In **Select an account for this service**, choose an existing managed account or create a new one.</span></span> <span data-ttu-id="f92e8-144">该帐户必须是域用户帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-144">The account must be a domain user account.</span></span>  
  
6.  <span data-ttu-id="f92e8-145">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="f92e8-145">Click **OK**.</span></span>  
  
##  <a name="create-or-change-the-application-pool-for-a-powerpivot-service-application"></a><a name="bkmk_appPool"></a><span data-ttu-id="f92e8-146">创建或更改 PowerPivot 服务应用程序的应用程序池</span><span class="sxs-lookup"><span data-stu-id="f92e8-146">Create or change the application pool for a PowerPivot service application</span></span>  
  
1.  <span data-ttu-id="f92e8-147">在“管理中心”的“应用程序管理”中，单击 **“管理服务应用程序”** 。</span><span class="sxs-lookup"><span data-stu-id="f92e8-147">In Central Administration, in Application Management, click **Manage service applications**.</span></span>  
  
2.  <span data-ttu-id="f92e8-148">选择但不要单击 PowerPivot 服务应用程序。</span><span class="sxs-lookup"><span data-stu-id="f92e8-148">Select, but do not click, the PowerPivot service application.</span></span> <span data-ttu-id="f92e8-149">单击应用程序名称将打开 PowerPivot 管理面板，其中未提供指向指定应用程序池的属性页的链接。</span><span class="sxs-lookup"><span data-stu-id="f92e8-149">Clicking on the application name opens the PowerPivot Management Dashboard, which does not provide a link to the properties page that specifies the application pool.</span></span>  <span data-ttu-id="f92e8-150">可以单击行中的空白区域或单击类型名称以选择 PowerPivot 服务应用程序。</span><span class="sxs-lookup"><span data-stu-id="f92e8-150">You can click the empty white space in the row, or click on type name, to select the PowerPivot service application.</span></span>  
  
3.  <span data-ttu-id="f92e8-151">在功能区上单击 **“属性”** 。</span><span class="sxs-lookup"><span data-stu-id="f92e8-151">Click **Properties** on the ribbon.</span></span>  
  
4.  <span data-ttu-id="f92e8-152">选择 **“创建新应用程序池”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-152">Select **Create a new application pool**.</span></span> <span data-ttu-id="f92e8-153">为应用程序池提供名称并为其标识指定托管帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-153">Provide a name for the application pool and specify a managed account for its identity.</span></span>  
  
##  <a name="account-requirements-and-permissions"></a><a name="requirements"></a><span data-ttu-id="f92e8-154">帐户要求和权限</span><span class="sxs-lookup"><span data-stu-id="f92e8-154">Account Requirements and Permissions</span></span>  
 <span data-ttu-id="f92e8-155">在规划 PowerPivot for SharePoint 部署时，必须规划以下服务帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-155">When planning a PowerPivot for SharePoint deployment, you must plan for the following service accounts.</span></span>  
  
-   <span data-ttu-id="f92e8-156">Analysis Services 服务帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-156">Analysis Services service account.</span></span> <span data-ttu-id="f92e8-157">Analysis Services 处理场中的 PowerPivot 查询和数据刷新作业。</span><span class="sxs-lookup"><span data-stu-id="f92e8-157">Analysis Services processes PowerPivot queries and data refresh jobs in the farm.</span></span> <span data-ttu-id="f92e8-158">安装 PowerPivot for SharePoint 时，在 SQL Server 安装期间始终指定该帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-158">This account is always specified during SQL Server Setup when you install PowerPivot for SharePoint.</span></span>  
  
-   <span data-ttu-id="f92e8-159">PowerPivot 服务应用程序池。</span><span class="sxs-lookup"><span data-stu-id="f92e8-159">PowerPivot Service Application Pool.</span></span> <span data-ttu-id="f92e8-160">PowerPivot 服务应用程序与 PowerPivot 系统服务相关联，它为场中的 PowerPivot 查询处理提供 SharePoint 集成和基础结构。</span><span class="sxs-lookup"><span data-stu-id="f92e8-160">A PowerPivot service application is associated with a PowerPivot System Service that provides SharePoint integration and infrastructure for PowerPivot query processing in a farm.</span></span> <span data-ttu-id="f92e8-161">您为 PowerPivot 服务应用程序指定的应用程序池是 PowerPivot 系统服务的服务标识。</span><span class="sxs-lookup"><span data-stu-id="f92e8-161">The application pool that you specify for a PowerPivot service application is the service identity of the PowerPivot System Service.</span></span> <span data-ttu-id="f92e8-162">在一个场中可有多个 PowerPivot 服务应用程序。</span><span class="sxs-lookup"><span data-stu-id="f92e8-162">You can have multiple PowerPivot service applications in a farm.</span></span> <span data-ttu-id="f92e8-163">所创建的每个应用程序都应在自己的应用程序池中运行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-163">Each one that you create should run in its own application pool.</span></span>  
  
#### <a name="analysis-services-service-account"></a><span data-ttu-id="f92e8-164">Analysis Services 服务帐户</span><span class="sxs-lookup"><span data-stu-id="f92e8-164">Analysis Services Service Account</span></span>  
  
|<span data-ttu-id="f92e8-165">要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-165">Requirement</span></span>|<span data-ttu-id="f92e8-166">说明</span><span class="sxs-lookup"><span data-stu-id="f92e8-166">Description</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="f92e8-167">设置要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-167">Provisioning requirement</span></span>|<span data-ttu-id="f92e8-168">在使用安装向导中的 " **Analysis Services 配置" 页** (或 `ASSVCACCOUNT` 命令行安装程序) 中的安装参数 SQL Server 时，必须指定此帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-168">This account must be specified during SQL Server Setup using the **Analysis Services - Configuration page** in the installation wizard (or the `ASSVCACCOUNT` installation parameter in a command line setup).</span></span><br /><br /> <span data-ttu-id="f92e8-169">您可以使用管理中心、PowerShell 或 PowerPivot 配置工具修改用户名或密码。</span><span class="sxs-lookup"><span data-stu-id="f92e8-169">You can modify the user name or password using Central Administration, PowerShell, or the PowerPivot Configuration Tool.</span></span> <span data-ttu-id="f92e8-170">不支持使用其他工具更改帐户和密码。</span><span class="sxs-lookup"><span data-stu-id="f92e8-170">Using other tools to change accounts and passwords is not supported.</span></span>|  
|<span data-ttu-id="f92e8-171">域用户帐户要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-171">Domain user account requirement</span></span>|<span data-ttu-id="f92e8-172">此帐户必须是 Windows 域用户帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-172">This account must be a Windows domain user account.</span></span> <span data-ttu-id="f92e8-173">禁止使用内置计算机帐户（如 Network Service 或 Local Service）。</span><span class="sxs-lookup"><span data-stu-id="f92e8-173">Built-in machine accounts (such as Network Service or Local Service) are prohibited.</span></span> <span data-ttu-id="f92e8-174">SQL Server 安装程序通过在指定计算机帐户时就阻止安装来强制执行域用户帐户要求。</span><span class="sxs-lookup"><span data-stu-id="f92e8-174">SQL Server Setup enforces the domain user account requirement by blocking installation whenever a machine account is specified.</span></span>|  
|<span data-ttu-id="f92e8-175">权限要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-175">Permission requirements</span></span>|<span data-ttu-id="f92e8-176">此帐户必须是 \<server> 本地计算机上 SQLServerMSASUser $ $PowerPivot 安全组和 WSS_WPG 安全组的成员。</span><span class="sxs-lookup"><span data-stu-id="f92e8-176">This account must be a member of the SQLServerMSASUser$\<server>$PowerPivot security group and the WSS_WPG security groups on the local computer.</span></span> <span data-ttu-id="f92e8-177">应自动授予这些权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-177">These permissions should be granted automatically.</span></span> <span data-ttu-id="f92e8-178">有关如何检查或授予权限的详细信息，请参阅本主题中[的手动授予 PowerPivot 服务帐户管理权限](#updatemanually)和[初始配置 &#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="f92e8-178">For more information on how to check or grant permissions, see [Grant the PowerPivot Service Account Administrative Permissions Manually](#updatemanually) in this topic and [Initial Configuration &#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).</span></span>|  
|<span data-ttu-id="f92e8-179">扩展要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-179">Scale-out requirements</span></span>|<span data-ttu-id="f92e8-180">如果您在场中安装多个 PowerPivot for SharePoint 服务器实例，则所有 Analysis Services 服务器实例都必须在同一域用户帐户下运行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-180">If you install multiple PowerPivot for SharePoint server instances in a farm, all of the Analysis Services server instances must run under the same domain user account.</span></span> <span data-ttu-id="f92e8-181">例如，如果你将第一个 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例配置为以 Contoso\ssas-srv01 身份运行，则随后在同一场中部署的所有其他 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例也必须以 Contoso\ssas-srv01（或碰巧为当前帐户）身份运行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-181">For example, if you configure the first [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instance to run as Contoso\ssas-srv01, then all additional [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instances that you deploy thereafter in the same farm must also run as Contoso\ssas-srv01 (or whatever the current account happens to be).</span></span><br /><br /> <span data-ttu-id="f92e8-182">如果将所有服务实例配置为在同一帐户下运行，则 PowerPivot 系统服务可以将查询处理或数据刷新作业分配到场中的任何 Analysis Services 服务实例。</span><span class="sxs-lookup"><span data-stu-id="f92e8-182">Configuring all service instances to run under the same account allows the PowerPivot System service to allocate query processing or data refresh jobs to any Analysis Services service instance in the farm.</span></span> <span data-ttu-id="f92e8-183">此外，它还可将管理中心的“托管帐户”功能用于 Analysis Services 服务器实例。</span><span class="sxs-lookup"><span data-stu-id="f92e8-183">In addition, it enables the use of the Managed Account feature in Central Administration for Analysis Services server instances.</span></span> <span data-ttu-id="f92e8-184">通过对所有 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例使用同一帐户，您可以只更改帐户或密码一次，而所有使用这些凭据的服务实例都会自动更新。</span><span class="sxs-lookup"><span data-stu-id="f92e8-184">By using the same account for all [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instances, you can change account or password once, and all service instances that use those credentials are updated automatically.</span></span><br /><br /> <span data-ttu-id="f92e8-185">SQL Server 安装程序强制执行使用同一帐户的要求。</span><span class="sxs-lookup"><span data-stu-id="f92e8-185">SQL Server Setup enforces the same-account requirement.</span></span> <span data-ttu-id="f92e8-186">在 SharePoint 场已安装 PowerPivot for SharePoint 实例的扩展部署中，如果您指定的 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]帐户与场中已使用的帐户不同，安装程序将阻止执行新的安装。</span><span class="sxs-lookup"><span data-stu-id="f92e8-186">In a scale-out deployment where a SharePoint farm already has an instance of PowerPivot for SharePoint installed, Setup will block the new installation if the [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] account you specified is different from the one already in use in the farm.</span></span>|  
  
#### <a name="powerpivot-service-application-pool"></a><span data-ttu-id="f92e8-187">PowerPivot 服务应用程序池</span><span class="sxs-lookup"><span data-stu-id="f92e8-187">PowerPivot Service Application Pool</span></span>  
  
|<span data-ttu-id="f92e8-188">要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-188">Requirement</span></span>|<span data-ttu-id="f92e8-189">说明</span><span class="sxs-lookup"><span data-stu-id="f92e8-189">Description</span></span>|  
|-----------------|-----------------|  
|<span data-ttu-id="f92e8-190">设置要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-190">Provisioning requirement</span></span>|<span data-ttu-id="f92e8-191">PowerPivot 系统服务是服务器场中的共享资源，在您创建服务应用程序时变得可用。</span><span class="sxs-lookup"><span data-stu-id="f92e8-191">PowerPivot System Service is a shared resource on the farm that becomes available when you create a service application.</span></span> <span data-ttu-id="f92e8-192">在创建服务应用程序时，必须指定服务应用程序池。</span><span class="sxs-lookup"><span data-stu-id="f92e8-192">The service application pool must be specified when the service application is created.</span></span> <span data-ttu-id="f92e8-193">可以通过两种方式指定应用程序池：使用 PowerPivot 配置工具或通过 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="f92e8-193">It can be specified two ways: using the PowerPivot Configuration Tool, or through PowerShell commands.</span></span><br /><br /> <span data-ttu-id="f92e8-194">您可能已配置了应用程序池标识以便基于唯一帐户运行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-194">You might have configured the application pool identity to run under a unique account.</span></span> <span data-ttu-id="f92e8-195">不过，如果您不想这样做，请考虑立即将其更改为在其他帐户下运行。</span><span class="sxs-lookup"><span data-stu-id="f92e8-195">But if you didn't, consider changing it now to run under a different account.</span></span>|  
|<span data-ttu-id="f92e8-196">域用户帐户要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-196">Domain user account requirement</span></span>|<span data-ttu-id="f92e8-197">应用程序池标识必须是 Windows 域用户帐户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-197">The application pool identity must be a Windows domain user account.</span></span> <span data-ttu-id="f92e8-198">禁止使用内置计算机帐户（如 Network Service 或 Local Service）。</span><span class="sxs-lookup"><span data-stu-id="f92e8-198">Built-in machine accounts (such as Network Service or Local Service) are prohibited.</span></span>|  
|<span data-ttu-id="f92e8-199">权限要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-199">Permission requirements</span></span>|<span data-ttu-id="f92e8-200">此帐户不需要计算机上的本地系统管理员权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-200">This account does not need local system Administrator permissions on the computer.</span></span> <span data-ttu-id="f92e8-201">但是，该帐户对安装在同一计算机上的本地 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 必须具有 Analysis Services 系统管理员权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-201">However, this account must have Analysis Services system administrator permissions on the local [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] that is installed on the same computer.</span></span> <span data-ttu-id="f92e8-202">将由 SQL Server 安装程序或当您在管理中心中设置或更改应用程序池标识时自动授予这些权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-202">These permissions are granted automatically by SQL Server Setup or when you set or change the application pool identity in Central Administration.</span></span><br /><br /> <span data-ttu-id="f92e8-203">管理权限是用于将查询转发到 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]所必需的。</span><span class="sxs-lookup"><span data-stu-id="f92e8-203">Administrative permissions are required for forwarding queries to the [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)].</span></span> <span data-ttu-id="f92e8-204">在监视运行状况、关闭处于非活动状态的会话和侦听跟踪事件时也需要这些权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-204">They are also required for monitoring health, closing inactive sessions, and listening for trace events.</span></span><br /><br /> <span data-ttu-id="f92e8-205">该帐户必须对 PowerPivot 服务应用程序数据库具有连接、读取和写入权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-205">The account must have connect, read, and write permissions to the PowerPivot service application database.</span></span> <span data-ttu-id="f92e8-206">在创建应用程序时将自动授予这些权限，并且在管理中心中更改权限和密码时将自动更新这些权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-206">These permissions are granted automatically when the application is created, and updated automatically when you change accounts or passwords in Central Administration.</span></span><br /><br /> <span data-ttu-id="f92e8-207">在检索文件前 PowerPivot 服务应用程序将检查 SharePoint 用户是否被授权查看数据，但它不模拟用户。</span><span class="sxs-lookup"><span data-stu-id="f92e8-207">The PowerPivot service application will check that a SharePoint user is authorized to view data before retrieving the file, but it does not impersonate the user.</span></span> <span data-ttu-id="f92e8-208">没有针对模拟的权限要求。</span><span class="sxs-lookup"><span data-stu-id="f92e8-208">There are no permission requirements for impersonation.</span></span>|  
|<span data-ttu-id="f92e8-209">扩展要求</span><span class="sxs-lookup"><span data-stu-id="f92e8-209">Scale-out requirements</span></span>|<span data-ttu-id="f92e8-210">无。</span><span class="sxs-lookup"><span data-stu-id="f92e8-210">None.</span></span>|  
  
##  <a name="troubleshooting-grant-administrative-permissions-manually"></a><a name="updatemanually"></a><span data-ttu-id="f92e8-211">故障排除：手动授予管理权限</span><span class="sxs-lookup"><span data-stu-id="f92e8-211">Troubleshooting: Grant Administrative Permissions Manually</span></span>  
 <span data-ttu-id="f92e8-212">如果更新凭据的人不是计算机上的本地管理员，则管理权限更新将会失败。</span><span class="sxs-lookup"><span data-stu-id="f92e8-212">Administrative permissions will fail to update if the person updating the credentials is not a local administrator on the computer.</span></span> <span data-ttu-id="f92e8-213">如果出现此情况，您可以手动授予管理权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-213">If this occurs, you can grant administrative permissions manually.</span></span> <span data-ttu-id="f92e8-214">为此，最简单的方法是在管理中心运行 PowerPivot 配置计时器作业。</span><span class="sxs-lookup"><span data-stu-id="f92e8-214">The easiest way to do this is to run the PowerPivot Configuration timer job in Central Administration.</span></span> <span data-ttu-id="f92e8-215">使用此方法，可以重置场中所有 PowerPivot 服务器的权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-215">With this approach, you can reset permissions for all PowerPivot servers in the farm.</span></span> <span data-ttu-id="f92e8-216">请注意，仅当同时以场管理员身份和计算机上的本地管理员身份运行 SharePoint 计时器作业时，此方法才有效。</span><span class="sxs-lookup"><span data-stu-id="f92e8-216">Note that this approach will only work if the SharePoint timer job is running as both farm administrator and as local administrator on the computer.</span></span>  
  
1.  <span data-ttu-id="f92e8-217">在“监视”中，单击 **“查看作业定义”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-217">In Monitoring, click **Review job definitions**.</span></span>  
  
2.  <span data-ttu-id="f92e8-218">选择 " **PowerPivot 配置计时器作业**"。</span><span class="sxs-lookup"><span data-stu-id="f92e8-218">Select **PowerPivot Configuration Timer Job**.</span></span>  
  
3.  <span data-ttu-id="f92e8-219">单击 "**立即运行**"。</span><span class="sxs-lookup"><span data-stu-id="f92e8-219">Click **Run Now**.</span></span>  
  
 <span data-ttu-id="f92e8-220">作为最后的手段，您可以通过向 PowerPivot 服务应用程序授予 Analysis Services 系统管理权限，然后专门将服务应用程序标识添加到 SQLServerMSASUser $ \<servername> $PowerPivot Windows 安全组，从而确保正确的权限。</span><span class="sxs-lookup"><span data-stu-id="f92e8-220">As a last resort, you can ensure correct permissions by granting Analysis Services System Administration permissions to the PowerPivot service application, and then specifically add the service application identity to the SQLServerMSASUser$\<servername>$PowerPivot Windows security group.</span></span> <span data-ttu-id="f92e8-221">必须对与 SharePoint 场集成的每个 Analysis Services 实例重复这些步骤。</span><span class="sxs-lookup"><span data-stu-id="f92e8-221">You must repeat these steps for every Analysis Services instance that is integrated with the SharePoint farm.</span></span>  
  
 <span data-ttu-id="f92e8-222">您必须是本地管理员才能更新 Windows 安全组。</span><span class="sxs-lookup"><span data-stu-id="f92e8-222">You must be a local administrator to update Windows security groups.</span></span>  
  
1.  <span data-ttu-id="f92e8-223">在 SQL Server Management Studio 中，以 \Powerpivot。连接到 Analysis Services 实例。 \<server name></span><span class="sxs-lookup"><span data-stu-id="f92e8-223">In SQL Server Management Studio, connect to the Analysis Services instance as \<server name>\POWERPIVOT.</span></span>  
  
2.  <span data-ttu-id="f92e8-224">右键单击服务器名称并选择“属性”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f92e8-224">Right-click the server name and select **Properties**.</span></span>  
  
3.  <span data-ttu-id="f92e8-225">单击 **“安全性”** 。</span><span class="sxs-lookup"><span data-stu-id="f92e8-225">Click **Security**.</span></span>  
  
4.  <span data-ttu-id="f92e8-226">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-226">Click **Add**.</span></span>  
  
5.  <span data-ttu-id="f92e8-227">键入用于 PowerPivot 服务应用程序池的帐户名称，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-227">Type the name of the account that is used for PowerPivot service application pool, and then click **OK**.</span></span>  
  
6.  <span data-ttu-id="f92e8-228">在“管理工具”中，单击 **“计算机管理”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-228">In Administrative Tools, click **Computer Management**.</span></span>  
  
7.  <span data-ttu-id="f92e8-229">打开 **“本地用户和组”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-229">Open **Local Users and Groups**.</span></span>  
  
8.  <span data-ttu-id="f92e8-230">打开 **“组”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-230">Open **Groups**.</span></span>  
  
9. <span data-ttu-id="f92e8-231">双击 "SQLServerMSASUser $ \<servername> $PowerPivot。</span><span class="sxs-lookup"><span data-stu-id="f92e8-231">Double-click SQLServerMSASUser$\<servername>$PowerPivot.</span></span>  
  
10. <span data-ttu-id="f92e8-232">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-232">Click **Add**.</span></span>  
  
11. <span data-ttu-id="f92e8-233">键入用于 PowerPivot 服务应用程序池的帐户名称，然后单击 **"确定"**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-233">Type the name of the account that is used for PowerPivot service application pool, and then click **OK**.</span></span>  
  
##  <a name="troubleshooting-resolve-http-503-errors-due-to-expired-passwords-for-central-administration-or-the-sharepoint-foundation-web-application-service"></a><a name="expired"></a><span data-ttu-id="f92e8-234">故障排除：解决由于管理中心或 SharePoint Foundation Web 应用程序服务密码过期而导致的 HTTP 503 错误</span><span class="sxs-lookup"><span data-stu-id="f92e8-234">Troubleshooting: Resolve HTTP 503 Errors Due to Expired Passwords for Central Administration or the SharePoint Foundation Web Application Service</span></span>  
 <span data-ttu-id="f92e8-235">如果管理中心服务或 SharePoint Foundation Web 应用程序服务由于帐户重置或密码过期而停止工作，您在尝试打开 SharePoint 管理中心或 SharePoint 站点时将遇到 HTTP 503“服务不可用”错误消息。</span><span class="sxs-lookup"><span data-stu-id="f92e8-235">If Central Administration service or the SharePoint Foundation Web Application service stops working due to an account reset or password expiration, you will encounter HTTP 503 "Service unavailable" error messages when attempting to open SharePoint Central Administration or a SharePoint site.</span></span> <span data-ttu-id="f92e8-236">按以下步骤操作可将服务器恢复联机状态。</span><span class="sxs-lookup"><span data-stu-id="f92e8-236">Follow these steps to bring your server back online.</span></span> <span data-ttu-id="f92e8-237">一旦管理中心可用，您就可以继续更新过期帐户信息。</span><span class="sxs-lookup"><span data-stu-id="f92e8-237">Once Central Administration is available, you can proceed to update expired account information.</span></span>  
  
1.  <span data-ttu-id="f92e8-238">在“管理工具”中，单击 **“Internet Information Services 管理器”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-238">In Administrative tools, click **Internet Information Services Manager**.</span></span>  
  
2.  <span data-ttu-id="f92e8-239">针对属于具有过期密码的域用户帐户的站点或管理中心应用程序池标识，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="f92e8-239">For the identity of the site or Central Administration application pool is a domain user account that has an expired password, do the following:</span></span>  
  
    1.  <span data-ttu-id="f92e8-240">右键单击应用程序池名称并选择“高级设置”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="f92e8-240">Right-click the application pool name and select **Advanced Settings**.</span></span>  
  
    2.  <span data-ttu-id="f92e8-241">选择 "**标识**"，然后单击 "..."按钮，打开 "应用程序池标识" 对话框。</span><span class="sxs-lookup"><span data-stu-id="f92e8-241">Select **Identity** and click the ... button to open the Application Pool Identity dialog box.</span></span>  
  
    3.  <span data-ttu-id="f92e8-242">单击 **“设置”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-242">Click **Set**.</span></span>  
  
    4.  <span data-ttu-id="f92e8-243">键入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="f92e8-243">Type the username and password.</span></span>  
  
3.  <span data-ttu-id="f92e8-244">运行 IISRESET。</span><span class="sxs-lookup"><span data-stu-id="f92e8-244">Run IISRESET.</span></span> <span data-ttu-id="f92e8-245">为此，请以管理员身份打开命令提示符，键入 `iisreset` 命令。</span><span class="sxs-lookup"><span data-stu-id="f92e8-245">To do this, open an Administrator command prompt and type `iisreset` at the command.</span></span>  
  
4.  <span data-ttu-id="f92e8-246">在 SharePoint 管理中心的“安全性”部分中，选择 **“配置托管帐户”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-246">In SharePoint Central Administration, in Security, select **Configure managed accounts**.</span></span>  
  
5.  <span data-ttu-id="f92e8-247">单击 **“编辑”** 以更新具有过期密码的托管帐户的信息。</span><span class="sxs-lookup"><span data-stu-id="f92e8-247">Click **Edit** to update the information of the managed account that has the expired password.</span></span>  
  
6.  <span data-ttu-id="f92e8-248">选择 **“立即更改密码”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-248">Select **Change password now**.</span></span>  
  
7.  <span data-ttu-id="f92e8-249">单击 **“使用现有密码”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-249">Click **Use existing password**.</span></span>  
  
8.  <span data-ttu-id="f92e8-250">键入密码，然后单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="f92e8-250">Type the password, and then click **OK**.</span></span>  
  
 <span data-ttu-id="f92e8-251">如果安装了 Reporting Services，可以使用 Reporting Services 配置管理器来更新报表服务器的密码和与报表服务器数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="f92e8-251">If Reporting Services is installed, use the Reporting Services Configuration Manager to update passwords for the report server and the connection to the report server database.</span></span> <span data-ttu-id="f92e8-252">有关详细信息，请参阅[配置和管理报表服务器（Reporting Services SharePoint 模式）](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)。</span><span class="sxs-lookup"><span data-stu-id="f92e8-252">For more information, see [Configuration and Administration of a Report Server &#40;Reporting Services SharePoint Mode&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f92e8-253">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f92e8-253">See Also</span></span>  
 <span data-ttu-id="f92e8-254">[启动或停止 PowerPivot for SharePoint 服务器](start-or-stop-a-power-pivot-for-sharepoint-server.md) </span><span class="sxs-lookup"><span data-stu-id="f92e8-254">[Start or Stop a PowerPivot for SharePoint Server](start-or-stop-a-power-pivot-for-sharepoint-server.md) </span></span>  
 [<span data-ttu-id="f92e8-255">将 PowerPivot 无人参与的数据刷新帐户配置 &#40;PowerPivot for SharePoint&#41;</span><span class="sxs-lookup"><span data-stu-id="f92e8-255">Configure the PowerPivot Unattended Data Refresh Account &#40;PowerPivot for SharePoint&#41;</span></span>](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
  