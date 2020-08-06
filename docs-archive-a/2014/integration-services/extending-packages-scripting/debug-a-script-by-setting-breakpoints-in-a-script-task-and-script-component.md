---
title: 通过在脚本任务和脚本组件中设置断点来调试脚本 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45e7ffc6680c33e3b17b9b39fba0aabd8fa4028c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579643"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a><span data-ttu-id="29224-102">通过在脚本任务和脚本组件中设置断点来调试脚本</span><span class="sxs-lookup"><span data-stu-id="29224-102">Debug a Script by Setting Breakpoints in a Script Task and Script Component</span></span>
  <span data-ttu-id="29224-103">此过程描述如何在脚本任务和脚本组件所使用的脚本中设置断点。</span><span class="sxs-lookup"><span data-stu-id="29224-103">This procedure describes how to set breakpoints in the scripts that are used in the Script task and Script component.</span></span>  
  
 <span data-ttu-id="29224-104">在脚本中设置断点后，“设置断点 - \<object name>”对话框会列出这些断点以及内置断点。</span><span class="sxs-lookup"><span data-stu-id="29224-104">After you set breakpoints in the script, the **Set Breakpoints - \<object name>** dialog box lists the breakpoints, along with the built-in breakpoints.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="29224-105">在某些情况下，将忽略脚本任务和脚本组件中的断点。</span><span class="sxs-lookup"><span data-stu-id="29224-105">Under certain circumstances, breakpoints in the Script task and Script component are ignored.</span></span> <span data-ttu-id="29224-106">有关详细信息，请参阅[编码和调试脚本](../control-flow/script-task.md)任务中的**调试脚本任务**部分和调试脚本**组件**部分 [编码和调试脚本组件] (。/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.</span><span class="sxs-lookup"><span data-stu-id="29224-106">For more information, see the **Debugging the Script Task** section in [Coding and Debugging the Script Task](../control-flow/script-task.md) and the **Debugging the Script Component** section in [Coding and Debugging the Script Component](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md.</span></span>  
  
### <a name="to-set-a-breakpoint-in-script"></a><span data-ttu-id="29224-107">在脚本中设置断点</span><span class="sxs-lookup"><span data-stu-id="29224-107">To set a breakpoint in script</span></span>  
  
1.  <span data-ttu-id="29224-108">在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。</span><span class="sxs-lookup"><span data-stu-id="29224-108">In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], open the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] project that contains the package you want.</span></span>  
  
2.  <span data-ttu-id="29224-109">双击包含要在其中设置断点的脚本的包。</span><span class="sxs-lookup"><span data-stu-id="29224-109">Double-click the package that contains the script in which you want to set breakpoints.</span></span>  
  
3.  <span data-ttu-id="29224-110">若要打开脚本任务，请单击“控制流”  选项卡，然后双击该脚本任务。</span><span class="sxs-lookup"><span data-stu-id="29224-110">To open the Script task, click the **Control Flow** tab, and then double-click the Script task.</span></span>  
  
4.  <span data-ttu-id="29224-111">若要打开脚本组件，请单击“数据流”  选项卡，然后双击该脚本组件。</span><span class="sxs-lookup"><span data-stu-id="29224-111">To open the Script component, click the **Data Flow** tab, and then double-click the Script component.</span></span>  
  
5.  <span data-ttu-id="29224-112">单击“脚本”  ，然后单击“编辑脚本”  。</span><span class="sxs-lookup"><span data-stu-id="29224-112">Click **Script** and then click **Edit Script**.</span></span>  
  
6.  <span data-ttu-id="29224-113">在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 中，找到要设置断点的脚本行，右键单击该行，指向“断点”，再单击“插入断点”   。</span><span class="sxs-lookup"><span data-stu-id="29224-113">In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), locate the line of script on which you want to set a breakpoint, right-click that line, point to **Breakpoint**, and then click **Insert Breakpoint**.</span></span>  
  
     <span data-ttu-id="29224-114">断点图标随即出现在该行代码上。</span><span class="sxs-lookup"><span data-stu-id="29224-114">The breakpoint icon appears on the line of code.</span></span>  
  
7.  <span data-ttu-id="29224-115">在 **“文件”** 菜单中，单击 **“退出”** 。</span><span class="sxs-lookup"><span data-stu-id="29224-115">On the **File** menu, click **Exit**.</span></span>  
  
8.  <span data-ttu-id="29224-116">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="29224-116">Click **OK**.</span></span>  
  
9. <span data-ttu-id="29224-117">若要保存包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。</span><span class="sxs-lookup"><span data-stu-id="29224-117">To save the package, click **Save Selected Items** on the **File** menu.</span></span>  
  
  
