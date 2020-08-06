---
title: SSIS 工具箱 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.toolboxcommon.F1
- sql12.dts.designer.toolbox.F1
- sql12.dts.designer.toolboxfavorites.F1
ms.assetid: 552ff592-eeef-46e8-b4a2-9b2384c869aa
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ed35218c84c77d3116ab8c897fe51fab5d6359aa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690731"
---
# <a name="ssis-toolbox"></a><span data-ttu-id="3e009-102">SSIS 工具箱</span><span class="sxs-lookup"><span data-stu-id="3e009-102">SSIS Toolbox</span></span>
  <span data-ttu-id="3e009-103">安装在本地计算机上的所有组件（包括为 SQL Server 2008 和 2008 R2 生成的第三方组件）现在都自动显示在新的“SSIS 工具箱”中。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="3e009-103">All components that are installed on the local machine, including third-party components built for SQL Server 2008 and 2008 R2, now automatically appear in the new **SSIS Toolbox**.</span></span> <span data-ttu-id="3e009-104">当安装其他组件时，在此工具箱内右键单击，然后单击“刷新工具箱”即会添加组件。 </span><span class="sxs-lookup"><span data-stu-id="3e009-104">When you install additional components, right-click inside the toolbox and then click **Refresh Toolbox** to add the components.</span></span>  
  
 <span data-ttu-id="3e009-105">您可以轻松地从此工具箱访问有关某组件的详细信息，只需单击该组件就可以在工具箱底部查看说明。</span><span class="sxs-lookup"><span data-stu-id="3e009-105">You can easily access more information about a component from the toolbox, by clicking the component to view a description at the bottom of the toolbox.</span></span> <span data-ttu-id="3e009-106">单击说明旁边的“帮助”按钮可显示联机丛书主题。</span><span class="sxs-lookup"><span data-stu-id="3e009-106">Click the Help button next to the description to display the Books Online topic.</span></span> <span data-ttu-id="3e009-107">对于某些组件，您也可以访问演示如何配置和使用这些组件的示例。</span><span class="sxs-lookup"><span data-stu-id="3e009-107">For certain components, you can also access samples that demonstrate how to configure and use the components.</span></span> <span data-ttu-id="3e009-108">在 [MSDN](https://go.microsoft.com/fwlink/?LinkId=259189)上提供这些示例。</span><span class="sxs-lookup"><span data-stu-id="3e009-108">The samples are available on [MSDN](https://go.microsoft.com/fwlink/?LinkId=259189).</span></span> <span data-ttu-id="3e009-109">若要从 **“SSIS 工具箱”** 访问示例，请单击在说明的下方出现的 **“查找示例”** 链接。</span><span class="sxs-lookup"><span data-stu-id="3e009-109">To access the samples from the **SSIS Toolbox**, click the **Find Samples** link that appears below the description.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="3e009-110">与以前的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]版本不同，不能从工具箱中删除已安装组件。</span><span class="sxs-lookup"><span data-stu-id="3e009-110">Unlike previous versions of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], you cannot remove installed components from the toolbox.</span></span>  
  
 <span data-ttu-id="3e009-111">在 **“SSIS 工具箱”** 中，控制流组件和数据流组件组织为不同的类别。</span><span class="sxs-lookup"><span data-stu-id="3e009-111">In the **SSIS Toolbox**, control flow and data flow components are organized into categories.</span></span>  <span data-ttu-id="3e009-112">您可以展开和折叠类别方便查看，也可以根据您的喜好更改组件的组织方式。</span><span class="sxs-lookup"><span data-stu-id="3e009-112">You can expand and collapse categories for viewing and you can change the organization of components according to your preferences.</span></span>  <span data-ttu-id="3e009-113">通过在此工具箱内右键单击，然后单击“还原工具箱默认值”，可以还原默认组织方式。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="3e009-113">You can restore the default organization, by right-clicking inside the toolbox and then click **Restore Toolbox Defaults**.</span></span>  
  
 <span data-ttu-id="3e009-114">选定 **“控制流”** 、 **“数据流”** 和 **“事件处理程序”** 选项卡时， **“收藏夹”** 和 **“公共”** 类别会显示在此工具箱中。</span><span class="sxs-lookup"><span data-stu-id="3e009-114">The **Favorites** and **Common** categories appear in the toolbox when you select the **Control Flow**, **Data Flow**, and **Event Handlers** tabs.</span></span> <span data-ttu-id="3e009-115">当您选择 "**控制流**" 选项卡或 "**事件处理程序**" 选项卡时，"**其他任务**" 类别将显示在工具箱中。选择 **"数据流" 选项卡**时，"工具箱" 中将显示**其他 "转换**"、"**其他源**" 和 "**其他目标**" 类别。</span><span class="sxs-lookup"><span data-stu-id="3e009-115">The **Other Tasks** category appears in the toolbox when you select the **Control Flow** tab or the **Event Handlers** tab. The **Other Transforms**, **Other Sources**, and **Other Destinations** categories appear in the toolbox when you select the **Data Flow** tab.</span></span>  
  
 <span data-ttu-id="3e009-116">创建新的 SSIS 项目或打开现有的项目时， **“SSIS 工具箱”** 自动显示。</span><span class="sxs-lookup"><span data-stu-id="3e009-116">When you create a new SSIS project or open an existing project, the **SSIS Toolbox** is automatically displayed.</span></span> <span data-ttu-id="3e009-117">也可以通过单击位于包设计图面右上角的工具箱按钮打开 SSIS 工具箱。</span><span class="sxs-lookup"><span data-stu-id="3e009-117">You can also open the toolbox by clicking the toolbox button that is located in the top-right corner of the package design surface.</span></span>  
  
 <span data-ttu-id="3e009-118">您可以停靠此工具箱，并将其设置为停靠时折叠，也可以关闭此工具箱。</span><span class="sxs-lookup"><span data-stu-id="3e009-118">You can dock the toolbox, set it to collapse when docked, and you can close the toolbox.</span></span>  
  
## <a name="related-tasks"></a><span data-ttu-id="3e009-119">Related Tasks</span><span class="sxs-lookup"><span data-stu-id="3e009-119">Related Tasks</span></span>  
  
-   [<span data-ttu-id="3e009-120">移动 SSIS 工具箱项</span><span class="sxs-lookup"><span data-stu-id="3e009-120">Move SSIS Toolbox Items</span></span>](../../2014/integration-services/move-ssis-toolbox-items.md)  
  
  
