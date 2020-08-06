---
title: 配置服务器启动选项（SQL Server 配置管理器）| Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 405a96208c774a6326a69cf9826a14ca3552eae1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688199"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a><span data-ttu-id="9b13f-102">配置服务器启动选项（SQL Server 配置管理器）</span><span class="sxs-lookup"><span data-stu-id="9b13f-102">Configure Server Startup Options (SQL Server Configuration Manager)</span></span>
  <span data-ttu-id="9b13f-103">本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中配置在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 每次启动时使用的启动选项。</span><span class="sxs-lookup"><span data-stu-id="9b13f-103">This topic describes how to configure startup options that will be used every time the [!INCLUDE[ssDE](../../includes/ssde-md.md)] starts in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] by using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.</span></span> <span data-ttu-id="9b13f-104">有关启动选项列表，请参阅 [数据库引擎服务启动选项](database-engine-service-startup-options.md)。</span><span class="sxs-lookup"><span data-stu-id="9b13f-104">For a list of startup options, see [Database Engine Service Startup Options](database-engine-service-startup-options.md).</span></span>  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> <span data-ttu-id="9b13f-105">开始之前</span><span class="sxs-lookup"><span data-stu-id="9b13f-105">Before You Begin</span></span>  
  
### <a name="limitations-and-restrictions"></a><span data-ttu-id="9b13f-106">限制和局限</span><span class="sxs-lookup"><span data-stu-id="9b13f-106">Limitations and Restrictions</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="9b13f-107">配置管理器将启动参数写入注册表。</span><span class="sxs-lookup"><span data-stu-id="9b13f-107">Configuration Manager writes startup parameters to the registry.</span></span> <span data-ttu-id="9b13f-108">这些参数将在下次启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)]时生效。</span><span class="sxs-lookup"><span data-stu-id="9b13f-108">They take effect upon the next startup of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span>  
  
 <span data-ttu-id="9b13f-109">在群集上，更改必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处于联机状态的情况下，在活动服务器上进行，并且在重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 时生效。</span><span class="sxs-lookup"><span data-stu-id="9b13f-109">On a cluster, changes must be made on the active server when [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is online, and will take effect when the [!INCLUDE[ssDE](../../includes/ssde-md.md)] is restarted.</span></span> <span data-ttu-id="9b13f-110">在其他节点上，启动选项的注册表更新将在下次故障转移时进行。</span><span class="sxs-lookup"><span data-stu-id="9b13f-110">The registry update of the startup options on the other node will occur upon the next failover.</span></span>  
  
###  <a name="security"></a><a name="Security"></a> <span data-ttu-id="9b13f-111">Security</span><span class="sxs-lookup"><span data-stu-id="9b13f-111">Security</span></span>  
  
####  <a name="permissions"></a><a name="Permissions"></a> <span data-ttu-id="9b13f-112">权限</span><span class="sxs-lookup"><span data-stu-id="9b13f-112">Permissions</span></span>  
 <span data-ttu-id="9b13f-113">只有可以更改注册表中的相关项的用户才能配置服务器启动选项。</span><span class="sxs-lookup"><span data-stu-id="9b13f-113">Configuring server startup options is restricted to users who can change the related entries in the registry.</span></span> <span data-ttu-id="9b13f-114">其中包括以下用户。</span><span class="sxs-lookup"><span data-stu-id="9b13f-114">This includes the following users.</span></span>  
  
-   <span data-ttu-id="9b13f-115">本地管理员组的成员。</span><span class="sxs-lookup"><span data-stu-id="9b13f-115">Members of the local administrators group.</span></span>  
  
-   <span data-ttu-id="9b13f-116">如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为在域帐户下运行，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用该域帐户。</span><span class="sxs-lookup"><span data-stu-id="9b13f-116">The domain account that is used by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], if the [!INCLUDE[ssDE](../../includes/ssde-md.md)] is configured to run under a domain account.</span></span>  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> <span data-ttu-id="9b13f-117">使用 SQL Server 配置管理器</span><span class="sxs-lookup"><span data-stu-id="9b13f-117">Using SQL Server Configuration Manager</span></span>  
  
#### <a name="to-configure-startup-options"></a><span data-ttu-id="9b13f-118">配置启动选项</span><span class="sxs-lookup"><span data-stu-id="9b13f-118">To configure startup options</span></span>  
  
1.  <span data-ttu-id="9b13f-119">在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中，单击 **“SQL Server 服务”** 。</span><span class="sxs-lookup"><span data-stu-id="9b13f-119">In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, click **SQL Server Services**.</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="9b13f-120">因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理控制台程序的一个管理单元而不是单独的程序，所以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器在新版本的 Windows 中不显示为一个应用程序。</span><span class="sxs-lookup"><span data-stu-id="9b13f-120">Because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager is a snap-in for the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console program and not a stand-alone program, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager does not appear as an application in newer versions of Windows.</span></span>  
    >   
    >  -   <span data-ttu-id="9b13f-121">**Windows 10**：</span><span class="sxs-lookup"><span data-stu-id="9b13f-121">**Windows 10**:</span></span>  
    >          <span data-ttu-id="9b13f-122">若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**开始" 页**上，键入) 的 sqlservermanager12.msc ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="9b13f-122">To open [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, on the **Start Page**, type SQLServerManager12.msc (for [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]).</span></span> <span data-ttu-id="9b13f-123">对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请将 12 替换为较小的数字。</span><span class="sxs-lookup"><span data-stu-id="9b13f-123">For previous versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replace 12 with a smaller number.</span></span> <span data-ttu-id="9b13f-124">单击 SQLServerManager12.msc 可打开“配置管理器”。</span><span class="sxs-lookup"><span data-stu-id="9b13f-124">Clicking SQLServerManager12.msc opens the Configuration Manager.</span></span> <span data-ttu-id="9b13f-125">若要将 Configuration Manager 固定到 "起始页" 或 "任务栏"，请右键单击 "Sqlservermanager12.msc"，然后单击 "**打开文件位置**"。</span><span class="sxs-lookup"><span data-stu-id="9b13f-125">To pin the Configuration Manager to the Start Page or Task Bar, right-click SQLServerManager12.msc, and then click **Open file location**.</span></span> <span data-ttu-id="9b13f-126">在 Windows 文件资源管理器中，右键单击 "Sqlservermanager12.msc"，然后单击 "**固定到\*\*\*\*任务栏**"。</span><span class="sxs-lookup"><span data-stu-id="9b13f-126">In the Windows File Explorer, right-click SQLServerManager12.msc, and then click **Pin to Start** or **Pin to taskbar**.</span></span>  
    > -   <span data-ttu-id="9b13f-127">**Windows 8**：</span><span class="sxs-lookup"><span data-stu-id="9b13f-127">**Windows 8**:</span></span>  
    >          <span data-ttu-id="9b13f-128">若要打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager，请在 "**搜索**" 超级按钮中的 "**应用**" 下，键入**sqlservermanager version>.msc （ \<version> **如 `SQLServerManager12.msc` ），然后按**enter**。</span><span class="sxs-lookup"><span data-stu-id="9b13f-128">To open [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, in the **Search** charm, under **Apps**, type **SQLServerManager\<version>.msc** such as `SQLServerManager12.msc`, and then press **Enter**.</span></span>  
  
2.  <span data-ttu-id="9b13f-129">在右侧窗格中，右键单击 " **SQL Server (" ***<instance_name>***) **"，然后单击"**属性**"。</span><span class="sxs-lookup"><span data-stu-id="9b13f-129">In the right pane, right-click **SQL Server (***<instance_name>***)**, and then click **Properties**.</span></span>  
  
3.  <span data-ttu-id="9b13f-130">在 **“启动参数”** 选项卡上的 **“指定启动参数”** 框中，键入该参数，然后单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="9b13f-130">On the **Startup Parameters** tab, in the **Specify a startup parameter** box, type the parameter, and then click **Add**.</span></span>  
  
     <span data-ttu-id="9b13f-131">例如，若要在单用户模式下启动，请 `-m` 在 "**指定启动参数**" 框中键入，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="9b13f-131">For example, to start in single-user mode, type `-m` in the **Specify a startup parameter** box and then click **Add**.</span></span> <span data-ttu-id="9b13f-132">（以单用户模式重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，请停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。</span><span class="sxs-lookup"><span data-stu-id="9b13f-132">(When you restart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in single-user mode, stop the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.</span></span> <span data-ttu-id="9b13f-133">否则， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可能会首先连接，并阻止你作为第二个用户连接。）</span><span class="sxs-lookup"><span data-stu-id="9b13f-133">Otherwise, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent might connect first and prevent you from connecting as a second user.)</span></span>  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  <span data-ttu-id="9b13f-134">重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="9b13f-134">Restart the [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span>  
  
    > [!WARNING]  
    >  <span data-ttu-id="9b13f-135">完成单用户模式的使用之后，在 "启动参数" 框中选择 " `-m` **现有参数**" 框中的参数，然后单击 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="9b13f-135">After you are finished using single-user mode, in the Startup Parameters box, select the `-m` parameter in the **Existing Parameters** box, and then click **Remove**.</span></span> <span data-ttu-id="9b13f-136">重新启动 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还原为典型的多用户模式。</span><span class="sxs-lookup"><span data-stu-id="9b13f-136">Restart the [!INCLUDE[ssDE](../../includes/ssde-md.md)] to restore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to the typical multi-user mode.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9b13f-137">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9b13f-137">See Also</span></span>  
 <span data-ttu-id="9b13f-138">[在单用户模式下启动 SQL Server](start-sql-server-in-single-user-mode.md) </span><span class="sxs-lookup"><span data-stu-id="9b13f-138">[Start SQL Server in Single-User Mode](start-sql-server-in-single-user-mode.md) </span></span>  
 <span data-ttu-id="9b13f-139">[在系统管理员被锁定时连接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md) </span><span class="sxs-lookup"><span data-stu-id="9b13f-139">[Connect to SQL Server When System Administrators Are Locked Out](connect-to-sql-server-when-system-administrators-are-locked-out.md) </span></span>  
 [<span data-ttu-id="9b13f-140">启动、停止或暂停 SQL Server 代理服务</span><span class="sxs-lookup"><span data-stu-id="9b13f-140">Start, Stop, or Pause the SQL Server Agent Service</span></span>](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
