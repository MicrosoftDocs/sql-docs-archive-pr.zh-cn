---
title: 对扩展事件使用 PowerShell 提供程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: rothja
ms.author: jroth
ms.openlocfilehash: a9efbd389545dcde8285a38b06f41580fb65de6c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587819"
---
# <a name="use-the-powershell-provider-for-extended-events"></a><span data-ttu-id="c717a-102">对扩展事件使用 PowerShell 提供程序</span><span class="sxs-lookup"><span data-stu-id="c717a-102">Use the PowerShell Provider for Extended Events</span></span>
  <span data-ttu-id="c717a-103">您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供程序管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件。</span><span class="sxs-lookup"><span data-stu-id="c717a-103">You can manage [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extended Events by using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell provider.</span></span> <span data-ttu-id="c717a-104">XEvent 子文件夹位于 SQLSERVER 驱动器下。</span><span class="sxs-lookup"><span data-stu-id="c717a-104">The XEvent subfolder is available under the SQLSERVER drive.</span></span> <span data-ttu-id="c717a-105">您可以使用以下任意一种方法访问该文件夹：</span><span class="sxs-lookup"><span data-stu-id="c717a-105">You can access the folder by using either of the following methods:</span></span>  
  
-   <span data-ttu-id="c717a-106">在命令提示符处，键入 `sqlps`，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="c717a-106">At a command prompt, type `sqlps`, and then press ENTER.</span></span> <span data-ttu-id="c717a-107">键入 `cd xevent`，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="c717a-107">Type `cd xevent`, and then press ENTER.</span></span> <span data-ttu-id="c717a-108">在这里，你可以使用**cd**和 `dir` 命令 (或**设置位置**和**get-childitem** cmdlet) 导航到服务器名称和实例名称。</span><span class="sxs-lookup"><span data-stu-id="c717a-108">From there, you can use the **cd** and `dir` commands (or **Set-Location** and **Get-Childitem** cmdlets) to navigate to the server name and instance name.</span></span>  
  
-   <span data-ttu-id="c717a-109">在对象资源管理器中，展开实例名称，展开“管理”\*\*\*\*，右键单击“扩展事件”\*\*\*\*，然后单击“启动 PowerShell”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c717a-109">In Object Explorer, expand the instance name, expand **Management**, right-click **Extended Events**, and then click **Start PowerShell**.</span></span> <span data-ttu-id="c717a-110">这将在以下路径中启动 PowerShell：</span><span class="sxs-lookup"><span data-stu-id="c717a-110">This starts PowerShell in the following path:</span></span>  
  
     <span data-ttu-id="c717a-111">PS SQLSERVER： \ XEvent \\ *ServerName* \\ *InstanceName*></span><span class="sxs-lookup"><span data-stu-id="c717a-111">PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*></span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="c717a-112">您可以从 **“扩展事件”** 下的任意节点启动 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c717a-112">You can start PowerShell from any node under **Extended Events**.</span></span> <span data-ttu-id="c717a-113">例如，你可以右键单击“会话”\*\*\*\*，然后单击“启动 PowerShell”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="c717a-113">For example, you can right-click **Sessions**, and then click **Start PowerShell**.</span></span> <span data-ttu-id="c717a-114">这将在下一级别（即“会话”文件夹）启动 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c717a-114">This starts PowerShell one level deeper, at the Sessions folder.</span></span>  
  
 <span data-ttu-id="c717a-115">您可以浏览 XEvent 文件夹树以查看现有的扩展事件会话及其关联的事件、目标和谓词。</span><span class="sxs-lookup"><span data-stu-id="c717a-115">You can browse the XEvent folder tree to view existing Extended Events sessions and their associated events, targets and predicates.</span></span> <span data-ttu-id="c717a-116">例如，从 PS SQLSERVER： \ XEvent \\ *ServerName* \\ *InstanceName*> 路径中，如果键入，请 `cd sessions` 按 enter，键入 `dir` ，然后按 enter，可以看到该实例上存储的会话的列表。</span><span class="sxs-lookup"><span data-stu-id="c717a-116">For example, from the PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*> path, if you type `cd sessions`, press ENTER, type `dir`, and then press ENTER, you can see the list of sessions that are stored on that instance.</span></span> <span data-ttu-id="c717a-117">您还可以查看会话是否正在运行（如果正在运行，那么可以查看运行了多长时间），以及会话是否配置为在实例启动时启动。</span><span class="sxs-lookup"><span data-stu-id="c717a-117">You can also view whether the session is running (and if this is the case, for how long), and whether the session is configured to start when the instance starts.</span></span>  
  
 <span data-ttu-id="c717a-118">若要查看与会话关联的事件、它们的谓词以及目标，您可以将目录更改为该会话的名称，然后查看事件或目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="c717a-118">To view the events, their predictates, and the targets that are associated with a session, you can change directories to the session name, and then view either the events or targets folder.</span></span> <span data-ttu-id="c717a-119">例如，若要查看与默认系统运行状况会话关联的事件及其谓词，请在 PS SQLSERVER： \ XEvent \\ *ServerName* \\ *InstanceName*\Sessions> 路径中，键入 `cd system_health\events,` 按 enter，键入 `dir` ，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="c717a-119">For example, to view the events and their predicates that are associated with the default system health session, from the PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*\Sessions> path, type `cd system_health\events,` press ENTER, type `dir`, and then press ENTER.</span></span>  
  
 <span data-ttu-id="c717a-120">[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供程序是一种非常强大的工具，您可以用其创建、更改和管理扩展事件会话。</span><span class="sxs-lookup"><span data-stu-id="c717a-120">The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell provider is a powerful tool that you can use to create, alter, and manage Extended Events sessions.</span></span> <span data-ttu-id="c717a-121">下面一节提供将 PowerShell 脚本与扩展事件结合使用的一些基本示例。</span><span class="sxs-lookup"><span data-stu-id="c717a-121">The following section provides some basic examples of using PowerShell scripts with Extended Events.</span></span>  
  
## <a name="examples"></a><span data-ttu-id="c717a-122">示例</span><span class="sxs-lookup"><span data-stu-id="c717a-122">Examples</span></span>  
 <span data-ttu-id="c717a-123">在下面的示例中，请注意以下事项：</span><span class="sxs-lookup"><span data-stu-id="c717a-123">In the following examples, note the following:</span></span>  
  
-   <span data-ttu-id="c717a-124">脚本必须从 PS SQLSERVER： \\> 提示符下运行 (可通过 `sqlps` 在命令提示符处键入) 来运行。</span><span class="sxs-lookup"><span data-stu-id="c717a-124">The scripts must be run from the PS SQLSERVER:\\> prompt (available by typing `sqlps` at a command prompt).</span></span>  
  
-   <span data-ttu-id="c717a-125">脚本使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的默认实例。</span><span class="sxs-lookup"><span data-stu-id="c717a-125">The scripts use the default instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span>  
  
-   <span data-ttu-id="c717a-126">脚本必须使用 .ps1 扩展名保存。</span><span class="sxs-lookup"><span data-stu-id="c717a-126">The scripts must be saved with a .ps1 extension.</span></span>  
  
-   <span data-ttu-id="c717a-127">PowerShell 执行策略必须允许脚本运行。</span><span class="sxs-lookup"><span data-stu-id="c717a-127">The PowerShell execution policy must allow the script to run.</span></span> <span data-ttu-id="c717a-128">若要设置执行策略，请使用 **Set-Executionpolicy** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c717a-128">To set the execution policy, use the **Set-Executionpolicy** cmdlet.</span></span> <span data-ttu-id="c717a-129">（有关详细信息，请键入 `get-help set-executionpolicy -detailed`，然后按 Enter）。</span><span class="sxs-lookup"><span data-stu-id="c717a-129">(For more information, type `get-help set-executionpolicy -detailed`, and then press ENTER.)</span></span>  
  
 <span data-ttu-id="c717a-130">下面的脚本将创建一个名为“TestSession”的新会话。</span><span class="sxs-lookup"><span data-stu-id="c717a-130">The following script creates a new session that is named 'TestSession'.</span></span>  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 <span data-ttu-id="c717a-131">下面的脚本将环形缓冲区目标添加到上一个示例所创建的会话中。</span><span class="sxs-lookup"><span data-stu-id="c717a-131">The following script adds the ring buffer target to the session that was created in the previous example.</span></span> <span data-ttu-id="c717a-132">（本示例演示了 `Alter` 方法的用法。</span><span class="sxs-lookup"><span data-stu-id="c717a-132">(This example shows the use of the `Alter` method.</span></span> <span data-ttu-id="c717a-133">请注意，在首次创建会话后即可添加目标。）</span><span class="sxs-lookup"><span data-stu-id="c717a-133">Be aware that you can add the target when you first create the session.)</span></span>  
  
```powershell
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir | where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 <span data-ttu-id="c717a-134">下面的脚本将创建一个使用谓词表达式的新会话。</span><span class="sxs-lookup"><span data-stu-id="c717a-134">The following script creates a new session that uses a predicate expression.</span></span> <span data-ttu-id="c717a-135">在本示例中，该会话将收集有关 c:\temp.log 文件何时发生写入操作的信息（通过 sqlserver.file_written 事件）。</span><span class="sxs-lookup"><span data-stu-id="c717a-135">In this case, the session collects information for when the c:\temp.log file is written to (through the sqlserver.file_written event).</span></span>  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -ArgumentList $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a><span data-ttu-id="c717a-136">安全性</span><span class="sxs-lookup"><span data-stu-id="c717a-136">Security</span></span>  
 <span data-ttu-id="c717a-137">若要创建、更改或删除扩展事件会话，您必须拥有 ALTER ANY EVENT SESSION 权限。</span><span class="sxs-lookup"><span data-stu-id="c717a-137">To create, alter, or drop an Extended Events session, you must have the ALTER ANY EVENT SESSION permission.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c717a-138">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c717a-138">See Also</span></span>  
 <span data-ttu-id="c717a-139">[SQL Server PowerShell](../../powershell/sql-server-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="c717a-139">[SQL Server PowerShell](../../powershell/sql-server-powershell.md) </span></span>  
 <span data-ttu-id="c717a-140">[使用 system_health 会话](use-the-ssms-xe-profiler.md) </span><span class="sxs-lookup"><span data-stu-id="c717a-140">[Use the system_health Session](use-the-ssms-xe-profiler.md) </span></span>  
 [<span data-ttu-id="c717a-141">扩展事件工具</span><span class="sxs-lookup"><span data-stu-id="c717a-141">Extended Events Tools</span></span>](extended-events-tools.md)  