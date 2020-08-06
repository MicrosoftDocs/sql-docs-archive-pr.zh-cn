---
title: 步骤 1：创建新的 Integration Services 项目 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d6d16d7febcdecb01eb7a93167c2a18d225a9c2d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586845"
---
# <a name="step-1-creating-a-new-integration-services-project"></a><span data-ttu-id="09e0c-102">步骤 1：创建新的 Integration Services 项目</span><span class="sxs-lookup"><span data-stu-id="09e0c-102">Step 1: Creating a New Integration Services Project</span></span>
  <span data-ttu-id="09e0c-103">若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中创建包，第一步是创建一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。</span><span class="sxs-lookup"><span data-stu-id="09e0c-103">The first step in creating a package in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] is to create an [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] project.</span></span> <span data-ttu-id="09e0c-104">此项目包含在数据转换解决方案中使用的数据源、数据源视图和包等对象的模板。</span><span class="sxs-lookup"><span data-stu-id="09e0c-104">This project includes the templates for the objects - data sources, data source views, and packages - that you use in a data transformation solution.</span></span>  
  
 <span data-ttu-id="09e0c-105">将在本 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教程中创建的包用于解释受区域设置影响的数据的值。</span><span class="sxs-lookup"><span data-stu-id="09e0c-105">The packages that you will create in this [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tutorial interpret the values of locale-sensitive data.</span></span> <span data-ttu-id="09e0c-106">如果您的计算机未配置为使用区域选项“英语(美国)”，则需要在包中设置其他属性。</span><span class="sxs-lookup"><span data-stu-id="09e0c-106">If your computer is not configured to use the regional option English (United States), you need to set additional properties in the package.</span></span> <span data-ttu-id="09e0c-107">第 2 课到第 5 课中使用的包是从第 1 课中创建的包复制而来的，因此不需要更新复制的包中受区域设置影响的属性。</span><span class="sxs-lookup"><span data-stu-id="09e0c-107">The packages that you use in lessons 2 through 5 are copied from the package created in lesson 1, and you need not update locale-sensitive properties in the copied packages.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="09e0c-108">本教程需要 Microsoft SQL Server Data Tools。</span><span class="sxs-lookup"><span data-stu-id="09e0c-108">This tutorial requires Microsoft SQL Server Data Tools.</span></span>  
>   
>  <span data-ttu-id="09e0c-109">有关安装 SQL Server Data Tools 的详细信息，请参阅 [SQL Server Data Tools 下载](https://msdn.microsoft.com/data/hh297027)。</span><span class="sxs-lookup"><span data-stu-id="09e0c-109">For more information on installing the SQL Server Data Tools see [SQL Server Data Tools Download](https://msdn.microsoft.com/data/hh297027).</span></span>  
  
### <a name="to-create-a-new-integration-services-project"></a><span data-ttu-id="09e0c-110">创建新的 Integration Services 项目</span><span class="sxs-lookup"><span data-stu-id="09e0c-110">To create a new Integration Services project</span></span>  
  
1.  <span data-ttu-id="09e0c-111">在 **“开始”** 菜单上，依次指向 **“所有程序”** 、 **Microsoft SQL Server**，再单击 **SQL Server Data Tools**。</span><span class="sxs-lookup"><span data-stu-id="09e0c-111">On the **Start** menu, point to **All Programs**, point to **Microsoft SQL Server**, and click **SQL Server Data Tools**.</span></span>  
  
2.  <span data-ttu-id="09e0c-112">在“文件”\*\*\*\* 菜单中，指向“新建”\*\*\*\*，再单击“项目”\*\*\*\*，以创建一个新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。</span><span class="sxs-lookup"><span data-stu-id="09e0c-112">On the **File** menu, point to **New**, and click **Project** to create a new [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] project.</span></span>  
  
3.  <span data-ttu-id="09e0c-113">在“新建项目”\*\*\*\* 对话框中，展开“已安装的模板”\*\*\*\* 下的“商业智能”\*\*\*\* 节点，并在“模板”\*\*\*\* 窗格中选择“Integration Services 项目”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="09e0c-113">In the **New Project** dialog box, expand the **Business Intelligence** node under **Installed Templates**, and select **Integration Services Project** in the **Templates** pane.</span></span>  
  
4.  <span data-ttu-id="09e0c-114">在“名称”\*\*\*\* 框中，将默认名称更改为 **SSIS Tutorial**。</span><span class="sxs-lookup"><span data-stu-id="09e0c-114">In the **Name** box, change the default name to **SSIS Tutorial**.</span></span> <span data-ttu-id="09e0c-115">或者，清除“创建解决方案的目录”\*\*\*\* 复选框。</span><span class="sxs-lookup"><span data-stu-id="09e0c-115">Optionally, clear the **Create directory for solution** check box.</span></span>  
  
5.  <span data-ttu-id="09e0c-116">接受默认位置，或单击“浏览”\*\*\*\*，以浏览并找到要使用的文件夹。</span><span class="sxs-lookup"><span data-stu-id="09e0c-116">Accept the default location, or click **Browse** to browse to locate the folder you want to use.</span></span> <span data-ttu-id="09e0c-117">在“项目位置”\*\*\*\* 对话框中，单击文件夹，再单击“选择文件夹”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="09e0c-117">In the **Project Location** dialog box, click the folder and click **Select Folder**.</span></span>  
  
6.  <span data-ttu-id="09e0c-118">单击“确定”  。</span><span class="sxs-lookup"><span data-stu-id="09e0c-118">Click **OK**.</span></span>  
  
     <span data-ttu-id="09e0c-119">默认情况下，将创建一个名为 **Package.dtsx**的空包，并将该包添加到项目中的“SSIS 包”之下。</span><span class="sxs-lookup"><span data-stu-id="09e0c-119">By default, an empty package, titled **Package.dtsx**, will be created and added to your project under SSIS Packages.</span></span>  
  
7.  <span data-ttu-id="09e0c-120">在“解决方案资源管理器”\*\*\*\* 工具栏中，右键单击“Package.dtsx”\*\*\*\*，再单击“重命名”\*\*\*\*，将默认包重命名为 **Lesson 1.dtsx**。</span><span class="sxs-lookup"><span data-stu-id="09e0c-120">In **Solution Explorer** toolbar, right-click **Package.dtsx**, click **Rename**, and rename the default package to **Lesson 1.dtsx**.</span></span>  
  
## <a name="next-task-in-lesson"></a><span data-ttu-id="09e0c-121">课程中的下一个任务</span><span class="sxs-lookup"><span data-stu-id="09e0c-121">Next Task in Lesson</span></span>  
 [<span data-ttu-id="09e0c-122">步骤 2：添加和配置平面文件连接管理器</span><span class="sxs-lookup"><span data-stu-id="09e0c-122">Step 2: Adding and Configuring a Flat File Connection Manager</span></span>](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
  
