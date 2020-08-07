---
title: 多维数据集设计器 (Analysis Services 多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Cube Designer
ms.assetid: a6692467-da88-4312-8b03-d812f2ae5a96
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6ceb921e1a9d5e5e4e7d67f1c2556e8b37d5d50
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588161"
---
# <a name="cube-designer-analysis-services---multidimensional-data"></a><span data-ttu-id="d0738-102">多维数据集设计器（Analysis Services - 多维数据）</span><span class="sxs-lookup"><span data-stu-id="d0738-102">Cube Designer (Analysis Services - Multidimensional Data)</span></span>
  <span data-ttu-id="d0738-103">可以使用 **中的** 多维数据集设计器 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ，编辑现有多维数据集的各种属性，包括多维数据集中包含的度量值组和度量值、多维数据集维度和维度关系、计算、关键绩效指标 (KPI)、操作、分区、透视和翻译，还可以浏览多维数据集中包含的数据。</span><span class="sxs-lookup"><span data-stu-id="d0738-103">Use **Cube Designer** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] to edit various properties of an existing cube, including the measure groups and measures, cube dimensions and dimension relationships, calculations, key performance indicators (KPIs), actions, partitions, perspectives, and translations included in the cube, as well as to browse the data contained by the cube.</span></span> <span data-ttu-id="d0738-104">通过执行以下操作可以显示 **“多维数据集设计器”** 对话框：</span><span class="sxs-lookup"><span data-stu-id="d0738-104">You can display the **Cube Designer** dialog box by:</span></span>  
  
-   <span data-ttu-id="d0738-105">在“解决方案资源管理器”中右键单击某个多维数据集，然后从上下文菜单中选择“打开”或“视图设计器”。\*\*\*\*\*\*\*\*\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="d0738-105">Right-clicking a cube in **Solution Explorer** and selecting **Open** or **View Designer** from the context menu.</span></span>  
  
-   <span data-ttu-id="d0738-106">在“解决方案资源管理器”中双击某个多维数据集。\*\*\*\*</span><span class="sxs-lookup"><span data-stu-id="d0738-106">Double-clicking a cube in **Solution Explorer**.</span></span>  
  
 <span data-ttu-id="d0738-107">**多维数据集设计器** 包含以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="d0738-107">The **Cube Designer** contains the following tabs:</span></span>  
  
## <a name="tabs"></a><span data-ttu-id="d0738-108">选项卡</span><span class="sxs-lookup"><span data-stu-id="d0738-108">Tabs</span></span>  
  
|<span data-ttu-id="d0738-109">选项卡</span><span class="sxs-lookup"><span data-stu-id="d0738-109">Tab</span></span>|<span data-ttu-id="d0738-110">定义</span><span class="sxs-lookup"><span data-stu-id="d0738-110">Definition</span></span>|  
|---------|----------------|  
|<span data-ttu-id="d0738-111">**多维数据集结构**</span><span class="sxs-lookup"><span data-stu-id="d0738-111">**Cube Structure**</span></span>|<span data-ttu-id="d0738-112">使用此选项卡可以创建和修改度量值组和度量值、添加多维数据集维度以及通过关联的数据源视图显示多维数据集中包含的对象。</span><span class="sxs-lookup"><span data-stu-id="d0738-112">Use this tab to create and modify measure groups and measures, add cube dimensions, and display the objects included in the cube from the associated data source view.</span></span> <span data-ttu-id="d0738-113">有关此选项卡的详细信息，请参阅[多维数据集结构（多维数据集设计器）（Analysis Services - 多维数据）](cube-structure-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-113">For more information about this tab, see [Cube Structure &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-114">**维度用法**</span><span class="sxs-lookup"><span data-stu-id="d0738-114">**Dimension Usage**</span></span>|<span data-ttu-id="d0738-115">使用此选项卡可以创建和修改多维数据集中包含的多维数据集维度和度量值组之间的关系。</span><span class="sxs-lookup"><span data-stu-id="d0738-115">Use this tab to create and modify relationships between cube dimensions and measure groups included in the cube.</span></span> <span data-ttu-id="d0738-116">有关此选项卡的详细信息，请参阅[维度用法（多维数据集设计器）（Analysis Services - 多维数据）](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-116">For more information about this tab, see [Dimension Usage &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-117">**计算**</span><span class="sxs-lookup"><span data-stu-id="d0738-117">**Calculations**</span></span>|<span data-ttu-id="d0738-118">使用此选项卡可以创建和修改多维数据集中包含的计算，包括计算成员、命名集和多维表达式 (MDX) 脚本。</span><span class="sxs-lookup"><span data-stu-id="d0738-118">Use this tab to create and modify calculations, including calculated members, named sets, and Multidimensional Expressions (MDX) scripts, included in the cube.</span></span> <span data-ttu-id="d0738-119">有关此选项卡的详细信息，请参阅[计算（多维数据集设计器）（Analysis Services - 多维数据）](calculations-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-119">For more information about this tab, see [Calculations &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-120">**KPI**</span><span class="sxs-lookup"><span data-stu-id="d0738-120">**KPIs**</span></span>|<span data-ttu-id="d0738-121">使用此选项卡可以创建和修改多维数据集中包含的 KPI。</span><span class="sxs-lookup"><span data-stu-id="d0738-121">Use this tab to create and modify KPIs included in the cube.</span></span> <span data-ttu-id="d0738-122">有关此选项卡的详细信息，请参阅[KPI（多维数据集设计器）（Analysis Services - 多维数据）](kpis-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-122">For more information about this tab, see [KPIs &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-123">**操作**</span><span class="sxs-lookup"><span data-stu-id="d0738-123">**Actions**</span></span>|<span data-ttu-id="d0738-124">使用此选项卡可以创建和修改多维数据集中包含的操作，包括钻取操作和报表操作。</span><span class="sxs-lookup"><span data-stu-id="d0738-124">Use this tab to create and modify actions, including drillthrough actions and report actions, included in the cube.</span></span> <span data-ttu-id="d0738-125">有关此选项卡的详细信息，请参阅[操作（多维数据集设计器）（Analysis Services - 多维数据）](actions-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-125">For more information about this tab, see [Actions &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](actions-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-126">**分区**</span><span class="sxs-lookup"><span data-stu-id="d0738-126">**Partitions**</span></span>|<span data-ttu-id="d0738-127">使用此选项卡可以创建和修改多维数据集中包含的分区，包括度量值组和分区的主动缓存设置。</span><span class="sxs-lookup"><span data-stu-id="d0738-127">Use this tab to create and modify partitions, including proactive caching settings for measure groups and partitions, included in the cube.</span></span> <span data-ttu-id="d0738-128">有关此选项卡的详细信息，请参阅[分区（多维数据集设计器）（Analysis Services - 多维数据）](partitions-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-128">For more information about this tab, see [Partitions &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](partitions-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-129">**透视**</span><span class="sxs-lookup"><span data-stu-id="d0738-129">**Perspectives**</span></span>|<span data-ttu-id="d0738-130">使用此选项卡可以创建和修改多维数据集中包含的透视。</span><span class="sxs-lookup"><span data-stu-id="d0738-130">Use this tab to create and modify perspectives included in the cube.</span></span> <span data-ttu-id="d0738-131">有关此选项卡的详细信息，请参阅[透视（多维数据集设计器）（Analysis Services - 多维数据）](perspectives-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-131">For more information about this tab, see [Perspectives &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](perspectives-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-132">**翻译**</span><span class="sxs-lookup"><span data-stu-id="d0738-132">**Translations**</span></span>|<span data-ttu-id="d0738-133">使用此选项卡可以创建和修改多维数据集中包含的度量值组、度量值、多维数据集维度、透视、KPI、操作、命名集和计算成员的翻译。</span><span class="sxs-lookup"><span data-stu-id="d0738-133">Use this tab to create and modify translations for measure groups, measures, cube dimensions, perspectives, KPIs, actions, named sets, and calculated members included in the cube.</span></span> <span data-ttu-id="d0738-134">有关此选项卡的详细信息，请参阅[翻译（多维数据集设计器）（Analysis Services - 多维数据）](translations-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-134">For more information about this tab, see [Translations &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](translations-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
|<span data-ttu-id="d0738-135">**浏览器**</span><span class="sxs-lookup"><span data-stu-id="d0738-135">**Browser**</span></span>|<span data-ttu-id="d0738-136">使用此选项卡可以浏览多维数据集的数据和元数据。</span><span class="sxs-lookup"><span data-stu-id="d0738-136">Use this tab to browse data and metadata for the cube.</span></span> <span data-ttu-id="d0738-137">有关此选项卡的详细信息，请参阅[浏览者（多维数据集设计器）（Analysis Services - 多维数据）](browser-cube-designer-analysis-services-multidimensional-data.md)。</span><span class="sxs-lookup"><span data-stu-id="d0738-137">For more information about this tab, see [Browser &#40;Cube Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](browser-cube-designer-analysis-services-multidimensional-data.md).</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="d0738-138">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d0738-138">See Also</span></span>  
 <span data-ttu-id="d0738-139">[多维数据集对象 &#40;Analysis Services 多维数据&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md) </span><span class="sxs-lookup"><span data-stu-id="d0738-139">[Cube Objects &#40;Analysis Services - Multidimensional Data&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md) </span></span>  
 <span data-ttu-id="d0738-140">[多维模型中的多维数据集](multidimensional-models/cubes-in-multidimensional-models.md) </span><span class="sxs-lookup"><span data-stu-id="d0738-140">[Cubes in Multidimensional Models](multidimensional-models/cubes-in-multidimensional-models.md) </span></span>  
 [<span data-ttu-id="d0738-141">&#40;多维数据的 Analysis Services 设计器和对话框&#41;</span><span class="sxs-lookup"><span data-stu-id="d0738-141">Analysis Services Designers and Dialog Boxes &#40;Multidimensional Data&#41;</span></span>](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  