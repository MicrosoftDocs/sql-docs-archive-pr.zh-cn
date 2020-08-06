---
title: 连接到服务器（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca227d1a3bbc13160962ba2fcad23ff011c950f3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690314"
---
# <a name="connect-to-server-database-engine"></a><span data-ttu-id="edb8c-102">连接到服务器（数据库引擎）</span><span class="sxs-lookup"><span data-stu-id="edb8c-102">Connect to Server (Database Engine)</span></span>
  <span data-ttu-id="edb8c-103">连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 时，可以使用此对话框查看或指定选项。</span><span class="sxs-lookup"><span data-stu-id="edb8c-103">Use this dialog to view or specify options when connecting to [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].</span></span> <span data-ttu-id="edb8c-104">大多数情况下，可以通过在“服务器名称”  框中输入数据库服务器的计算机名称并单击“连接”  来进行连接。</span><span class="sxs-lookup"><span data-stu-id="edb8c-104">In most cases, you can connect by entering the computer name of the database server in the **Server name** box and then clicking **Connect**.</span></span> <span data-ttu-id="edb8c-105">如果要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，请使用后面跟有 **\sqlexpress**的计算机名称。</span><span class="sxs-lookup"><span data-stu-id="edb8c-105">If you are connecting to [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], use the computer name followed by **\sqlexpress**.</span></span>  
  
 <span data-ttu-id="edb8c-106">许多因素都会对您能否连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产生影响。</span><span class="sxs-lookup"><span data-stu-id="edb8c-106">Many factors can affect your ability to connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
## <a name="options"></a><span data-ttu-id="edb8c-107">选项</span><span class="sxs-lookup"><span data-stu-id="edb8c-107">Options</span></span>  
 <span data-ttu-id="edb8c-108">**服务器类型**</span><span class="sxs-lookup"><span data-stu-id="edb8c-108">**Server type**</span></span>  
 <span data-ttu-id="edb8c-109">从对象资源管理器注册服务器时，请选择要连接到的服务器的类型： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="edb8c-109">When registering a server from Object Explorer, select the type of server to connect to: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], or [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].</span></span> <span data-ttu-id="edb8c-110">对话框的其余部分只显示适用于所选服务器类型的选项。</span><span class="sxs-lookup"><span data-stu-id="edb8c-110">The rest of the dialog shows only the options that apply to the selected server type.</span></span> <span data-ttu-id="edb8c-111">从“已注册的服务器”注册某服务器时，“服务器类型”  框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。</span><span class="sxs-lookup"><span data-stu-id="edb8c-111">When registering a server from Registered Servers, the **Server type** box is read-only, and matches the type of server displayed in the Registered Servers component.</span></span> <span data-ttu-id="edb8c-112">若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择“ [!INCLUDE[ssDE](../../includes/ssde-md.md)]”、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssEW](../../includes/ssew-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="edb8c-112">To register a different type of server, select [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)], or [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] from the Registered Servers toolbar before starting to register a new server.</span></span>  
  
 <span data-ttu-id="edb8c-113">**服务器名称**</span><span class="sxs-lookup"><span data-stu-id="edb8c-113">**Server name**</span></span>  
 <span data-ttu-id="edb8c-114">选择要连接到的服务器实例。</span><span class="sxs-lookup"><span data-stu-id="edb8c-114">Select the server instance to connect to.</span></span> <span data-ttu-id="edb8c-115">默认情况下，显示上次连接到的服务器实例。</span><span class="sxs-lookup"><span data-stu-id="edb8c-115">The server instance last connected to is displayed by default.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="edb8c-116">若要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的活动用户实例，请使用指定管道名称的 Named Pipes 协议进行连接，例如：np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query。有关详细信息，请参阅 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 文档。</span><span class="sxs-lookup"><span data-stu-id="edb8c-116">To connect to an active user instance of [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] connect using named pipes protocol specifying the pipe name, such as np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query For more information, see the [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] documentation.</span></span>  
  
 <span data-ttu-id="edb8c-117">**身份验证**</span><span class="sxs-lookup"><span data-stu-id="edb8c-117">**Authentication**</span></span>  
 <span data-ttu-id="edb8c-118">连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例时，有两种可用的身份验证模式。</span><span class="sxs-lookup"><span data-stu-id="edb8c-118">Two authentication modes are available when connecting to an instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span>  
  
 <span data-ttu-id="edb8c-119">**Windows 身份验证模式（Windows 身份验证）**</span><span class="sxs-lookup"><span data-stu-id="edb8c-119">**Windows Authentication Mode (Windows Authentication)**</span></span>  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] <span data-ttu-id="edb8c-120">Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。</span><span class="sxs-lookup"><span data-stu-id="edb8c-120">Windows Authentication mode allows a user to connect through a Windows user account.</span></span>  
  
 <span data-ttu-id="edb8c-121">**SQL Server 身份验证**</span><span class="sxs-lookup"><span data-stu-id="edb8c-121">**SQL Server Authentication**</span></span>  
 <span data-ttu-id="edb8c-122">当用户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="edb8c-122">When a user connects with a specified login name and password from a non-trusted connection, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] performs the authentication itself by checking to see if a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login account has been set up and if the specified password matches the one previously recorded.</span></span> <span data-ttu-id="edb8c-123">如果未设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="edb8c-123">If [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] does not have a login account set, authentication fails, and the user receives an error message.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="edb8c-124">请尽可能使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="edb8c-124">When possible, use Windows Authentication.</span></span>  
  
 <span data-ttu-id="edb8c-125">**用户名**</span><span class="sxs-lookup"><span data-stu-id="edb8c-125">**User name**</span></span>  
 <span data-ttu-id="edb8c-126">输入连接所使用的用户名。</span><span class="sxs-lookup"><span data-stu-id="edb8c-126">Enter the user name to connect with.</span></span> <span data-ttu-id="edb8c-127">只有在已选择使用 Windows 身份验证进行连接的情况下，此选项才可用。</span><span class="sxs-lookup"><span data-stu-id="edb8c-127">This option is only available if you have selected to connect using Windows Authentication.</span></span>  
  
 <span data-ttu-id="edb8c-128">**登录**</span><span class="sxs-lookup"><span data-stu-id="edb8c-128">**Login**</span></span>  
 <span data-ttu-id="edb8c-129">输入连接所用的登录名。</span><span class="sxs-lookup"><span data-stu-id="edb8c-129">Enter the login to connect with.</span></span> <span data-ttu-id="edb8c-130">只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接时，此选项才可用。</span><span class="sxs-lookup"><span data-stu-id="edb8c-130">This option is only available if you have selected to connect using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.</span></span>  
  
 <span data-ttu-id="edb8c-131">**密码**</span><span class="sxs-lookup"><span data-stu-id="edb8c-131">**Password**</span></span>  
 <span data-ttu-id="edb8c-132">输入登录名的密码。</span><span class="sxs-lookup"><span data-stu-id="edb8c-132">Enter the password for the login.</span></span> <span data-ttu-id="edb8c-133">只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接的情况下，此选项才可用。</span><span class="sxs-lookup"><span data-stu-id="edb8c-133">This option is only editable if you have selected to connect using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.</span></span>  
  
 <span data-ttu-id="edb8c-134">**“连接”**</span><span class="sxs-lookup"><span data-stu-id="edb8c-134">**Connect**</span></span>  
 <span data-ttu-id="edb8c-135">单击此项可连接到在上面选择的服务器。</span><span class="sxs-lookup"><span data-stu-id="edb8c-135">Click to connect to the server selected above.</span></span>  
  
 <span data-ttu-id="edb8c-136">**选项**</span><span class="sxs-lookup"><span data-stu-id="edb8c-136">**Options**</span></span>  
 <span data-ttu-id="edb8c-137">单击此项可显示其他服务器连接选项，如注册服务器和记住密码。</span><span class="sxs-lookup"><span data-stu-id="edb8c-137">Click to display additional server connection options, such as registering a server and remembering the password.</span></span>  
  
  
