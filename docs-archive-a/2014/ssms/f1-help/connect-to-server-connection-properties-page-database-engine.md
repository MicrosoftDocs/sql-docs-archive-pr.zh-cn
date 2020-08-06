---
title: 连接到服务器（“连接属性”页）（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 41f2aa3fd5004a371515ee5d8905c7bb73699829
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692623"
---
# <a name="connect-to-server-connection-properties-page-database-engine"></a><span data-ttu-id="58b1d-102">连接到服务器（“连接属性”页）（数据库引擎）</span><span class="sxs-lookup"><span data-stu-id="58b1d-102">Connect to Server (Connection Properties Page) Database Engine</span></span>
  <span data-ttu-id="58b1d-103">使用此选项卡可在连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例或在“已注册的服务器”  中注册 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 时查看或指定选项。</span><span class="sxs-lookup"><span data-stu-id="58b1d-103">Use this tab to view or specify options when connecting to an instance of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] or registering [!INCLUDE[ssDE](../../includes/ssde-md.md)] in **Registered Servers**.</span></span> <span data-ttu-id="58b1d-104">只有在连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例时，此对话框中才显示“连接”  和“选项”  。</span><span class="sxs-lookup"><span data-stu-id="58b1d-104">**Connect** and **Options** only appear in this dialog box when connecting to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span> <span data-ttu-id="58b1d-105">注册 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 时，此对话框中仅显示“测试”  和“保存”  。</span><span class="sxs-lookup"><span data-stu-id="58b1d-105">**Test** and **Save** only appear in this dialog box when registering [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span>  
  
## <a name="options"></a><span data-ttu-id="58b1d-106">选项</span><span class="sxs-lookup"><span data-stu-id="58b1d-106">Options</span></span>  
 <span data-ttu-id="58b1d-107">**连接到数据库**</span><span class="sxs-lookup"><span data-stu-id="58b1d-107">**Connect to database**</span></span>  
 <span data-ttu-id="58b1d-108">从列表中选择要连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="58b1d-108">Select a database to connect to from the list.</span></span> <span data-ttu-id="58b1d-109">如果选择 **\<default>** ，则将连接到服务器的默认数据库。</span><span class="sxs-lookup"><span data-stu-id="58b1d-109">If you select **\<default>**, you will be connected to the default database for the server.</span></span> <span data-ttu-id="58b1d-110">如果选择 **\<Browse server>** ，则可以浏览服务器以查找要连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="58b1d-110">If you select **\<Browse server>**, you can browse the server for the database to which to connect.</span></span>  
  
 <span data-ttu-id="58b1d-111">在通过 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，并且必须在“连接到服务器”  对话框的“连接属性”  选项卡上指定一个数据库。请确保选中“加密连接”  复选框。</span><span class="sxs-lookup"><span data-stu-id="58b1d-111">When connecting to an instance of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine through [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], you must use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication and specify a database in the **Connect to Server** dialog box, on the **Connection Properties** tab. Ensure that you select the **Encrypt connection** checkbox.</span></span>  
  
 <span data-ttu-id="58b1d-112">默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将连接到 **master**。</span><span class="sxs-lookup"><span data-stu-id="58b1d-112">By default, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connects to **master**.</span></span> <span data-ttu-id="58b1d-113">如果您指定一个用户数据库，在对象资源管理器中将只会看到该数据库及其对象。</span><span class="sxs-lookup"><span data-stu-id="58b1d-113">If you specify a user database, you will only see that database and its objects in Object Explorer.</span></span> <span data-ttu-id="58b1d-114">如果连接到 **master**，可以看到所有数据库。</span><span class="sxs-lookup"><span data-stu-id="58b1d-114">If you connect to **master**, you will be able to see all databases.</span></span> <span data-ttu-id="58b1d-115">有关详细信息，请参阅[AZURE SQL 数据库概述](/azure/sql-database/sql-database-technical-overview)。</span><span class="sxs-lookup"><span data-stu-id="58b1d-115">For more information, see the [Azure SQL Database Overview](/azure/sql-database/sql-database-technical-overview).</span></span>  
  
 <span data-ttu-id="58b1d-116">**网络协议**</span><span class="sxs-lookup"><span data-stu-id="58b1d-116">**Network protocol**</span></span>  
 <span data-ttu-id="58b1d-117">从该列表中选择某个协议。</span><span class="sxs-lookup"><span data-stu-id="58b1d-117">Select a protocol from the list.</span></span> <span data-ttu-id="58b1d-118">可用的客户端协议是您使用“计算机管理”中的“客户端网络配置”所配置的那些协议。</span><span class="sxs-lookup"><span data-stu-id="58b1d-118">The available client protocols are those that you configured using the Client Network Configuration in Computer Management.</span></span>  
  
 <span data-ttu-id="58b1d-119">**网络数据包大小**</span><span class="sxs-lookup"><span data-stu-id="58b1d-119">**Network packet size**</span></span>  
 <span data-ttu-id="58b1d-120">输入要发送的网络数据包的大小。</span><span class="sxs-lookup"><span data-stu-id="58b1d-120">Enter the size of the network packets to be sent.</span></span> <span data-ttu-id="58b1d-121">默认值为 4096 字节。</span><span class="sxs-lookup"><span data-stu-id="58b1d-121">The default is 4096 bytes.</span></span>  
  
 <span data-ttu-id="58b1d-122">**连接超时**</span><span class="sxs-lookup"><span data-stu-id="58b1d-122">**Connection timeout**</span></span>  
 <span data-ttu-id="58b1d-123">输入在超时之前等待建立连接的秒数。默认值为15秒。</span><span class="sxs-lookup"><span data-stu-id="58b1d-123">Enter the number of seconds to wait for a connection to be established before timing out. The default value is 15 seconds.</span></span>  
  
 <span data-ttu-id="58b1d-124">**执行超时**</span><span class="sxs-lookup"><span data-stu-id="58b1d-124">**Execution timeout**</span></span>  
 <span data-ttu-id="58b1d-125">输入在服务器上完成任务执行之前等待的时间（秒）。</span><span class="sxs-lookup"><span data-stu-id="58b1d-125">Enter the amount of time in seconds to wait before execution of a task is completed on the server.</span></span> <span data-ttu-id="58b1d-126">默认值为零秒，指示无超时。</span><span class="sxs-lookup"><span data-stu-id="58b1d-126">The default value is zero seconds, which indicates there is no time-out.</span></span>  
  
 <span data-ttu-id="58b1d-127">**加密连接**</span><span class="sxs-lookup"><span data-stu-id="58b1d-127">**Encrypt connection**</span></span>  
 <span data-ttu-id="58b1d-128">强制对连接进行加密。</span><span class="sxs-lookup"><span data-stu-id="58b1d-128">Forces encryption of the connection.</span></span>  
  
 <span data-ttu-id="58b1d-129">**使用自定义颜色**</span><span class="sxs-lookup"><span data-stu-id="58b1d-129">**Use custom color**</span></span>  
 <span data-ttu-id="58b1d-130">选择此选项可以指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器窗口中状态栏的背景颜色。</span><span class="sxs-lookup"><span data-stu-id="58b1d-130">Select to specify the background color for the status bar in a [!INCLUDE[ssDE](../../includes/ssde-md.md)] Query Editor window.</span></span> <span data-ttu-id="58b1d-131">若要指定颜色，请单击“选择”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="58b1d-131">To specify the color, click **Select**.</span></span> <span data-ttu-id="58b1d-132">在“颜色”\*\*\*\* 对话框中，从“基本颜色”\*\*\*\* 网格中选择一种预定义颜色，或者单击“定义自定义颜色”\*\*\*\* 定义并使用自定义颜色。</span><span class="sxs-lookup"><span data-stu-id="58b1d-132">In the **Color** dialog box, select a predefined color from the **Basic Colors** grid or click **Define Custom Colors** to define and use a custom color.</span></span>  
  
-   <span data-ttu-id="58b1d-133">如果在“对象资源管理器”\*\*\*\* 窗格中指定了服务器条目的颜色，则在打开查询编辑器窗口时将使用此颜色。</span><span class="sxs-lookup"><span data-stu-id="58b1d-133">When you specify a color for a server entry in the **Object Explorer** pane, that color is used when you open a Query Editor window.</span></span> <span data-ttu-id="58b1d-134">若要打开查询编辑器窗口，可以右键单击服务器条目，然后选择“新建查询”\*\*\*\*，或者如果“对象资源管理器”\*\*\*\* 窗格处于活动状态且其焦点位于此服务器上，则可以单击工具栏上的“新建查询”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="58b1d-134">To open a Query Editor window, either right-click the server entry and select **New Query**; or, when the **Object Explorer** pane is active and focused on this server, click **New Query** on the toolbar.</span></span>  
  
-   <span data-ttu-id="58b1d-135">如果在“已注册的服务器”\*\*\*\* 窗格中指定了服务器条目的颜色，则在打开查询编辑器窗口时将使用此颜色。</span><span class="sxs-lookup"><span data-stu-id="58b1d-135">When you specify a color for a server entry in the **Registered Servers** pane, that color is used when you open a Query Editor window.</span></span> <span data-ttu-id="58b1d-136">若要打开查询编辑器窗口，可以右键单击服务器条目，然后选择“新建查询”\*\*\*\*，或者如果“已注册的服务器”\*\*\*\* 窗格处于活动状态且其焦点位于此服务器上，则可以单击工具栏上的“新建查询”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="58b1d-136">To open a Query Editor window, either right-click the server entry and select **New Query**; or, when the **Registered Server** pane is active and focused on this server, click **New Query** on the toolbar.</span></span>  
  
-   <span data-ttu-id="58b1d-137">依次单击“文件”\*\*\*\* 菜单上的“新建”\*\*\*\* 和“数据库引擎查询”\*\*\*\* 后，在“连接到服务器”\*\*\*\* 对话框中指定的颜色即应用于此查询编辑器窗口。</span><span class="sxs-lookup"><span data-stu-id="58b1d-137">On the **File** menu, when you click **New** and then **Database Engine Query**, the color you that you specify in the **Connect to Server** dialog box applies to that Query Editor window.</span></span>  
  
 <span data-ttu-id="58b1d-138">**全部重置**</span><span class="sxs-lookup"><span data-stu-id="58b1d-138">**Reset All**</span></span>  
 <span data-ttu-id="58b1d-139">将所有手动输入的连接属性值替换为默认值。</span><span class="sxs-lookup"><span data-stu-id="58b1d-139">Replace all manually entered connection property values with their defaults.</span></span>  
  
 <span data-ttu-id="58b1d-140">**“连接”**</span><span class="sxs-lookup"><span data-stu-id="58b1d-140">**Connect**</span></span>  
 <span data-ttu-id="58b1d-141">使用列出的值尝试连接。</span><span class="sxs-lookup"><span data-stu-id="58b1d-141">Attempt a connection using the listed values.</span></span>  
  
 <span data-ttu-id="58b1d-142">**选项**</span><span class="sxs-lookup"><span data-stu-id="58b1d-142">**Options**</span></span>  
 <span data-ttu-id="58b1d-143">单击此选项更改对话框并隐藏其他服务器连接选项，例如记住密码。</span><span class="sxs-lookup"><span data-stu-id="58b1d-143">Click to change the dialog box and hide the additional server connection options, such as remembering the password.</span></span>  
  
 <span data-ttu-id="58b1d-144">**Test**</span><span class="sxs-lookup"><span data-stu-id="58b1d-144">**Test**</span></span>  
 <span data-ttu-id="58b1d-145">在“已注册的服务器”\*\*\*\* 中注册 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 时，单击此选项可以测试连接。</span><span class="sxs-lookup"><span data-stu-id="58b1d-145">When registering [!INCLUDE[ssDE](../../includes/ssde-md.md)] in **Registered Servers**, click to test the connection.</span></span>  
  
 <span data-ttu-id="58b1d-146">**保存**</span><span class="sxs-lookup"><span data-stu-id="58b1d-146">**Save**</span></span>  
 <span data-ttu-id="58b1d-147">保存“已注册的服务器”\*\*\*\* 中的设置。</span><span class="sxs-lookup"><span data-stu-id="58b1d-147">Saves the settings in **Registered Servers**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="58b1d-148">另请参阅</span><span class="sxs-lookup"><span data-stu-id="58b1d-148">See Also</span></span>  
 [<span data-ttu-id="58b1d-149">“连接属性”对话框</span><span class="sxs-lookup"><span data-stu-id="58b1d-149">Connection Properties Dialog Box</span></span>](../../database-engine/connection-properties-dialog-box.md)  
  
  
