---
title: 处理选项和设置的 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process data option [Analysis Services]
- processing objects [Analysis Services]
- unprocess option [Analysis Services]
- process full option [Analysis Services]
- process index option [Analysis Services]
- process structure option [Analysis Services]
- process incremental option [Analysis Services]
- process update option [Analysis Services]
- process clear structure option [Analysis Services]
- process default option [Analysis Services]
ms.assetid: 2e858c74-ad3e-45f1-8745-efe2c0c3a7fa
author: minewiskan
ms.author: owend
ms.openlocfilehash: 00efad4483be1d4e646b33485f5fddf01dfb74b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579140"
---
# <a name="processing-options-and-settings-analysis-services"></a><span data-ttu-id="e803a-102">处理选项和设置 (Analysis Services)</span><span class="sxs-lookup"><span data-stu-id="e803a-102">Processing Options and Settings (Analysis Services)</span></span>
  <span data-ttu-id="e803a-103">在中处理对象时 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以选择处理选项以控制每个对象发生的处理的类型。</span><span class="sxs-lookup"><span data-stu-id="e803a-103">When you process objects in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], you can select a processing option to control the type of processing that occurs for each object.</span></span> <span data-ttu-id="e803a-104">处理类型因对象而异，并基于自上次处理对象后对象所发生的更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-104">Processing types differ from one object to another, and by changes that have occurred to the object since it was last processed.</span></span> <span data-ttu-id="e803a-105">如果允许 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自动选择处理方法，则将使用以最少时间将对象返回已完全处理状态的方法。</span><span class="sxs-lookup"><span data-stu-id="e803a-105">If you enable [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] to automatically select a processing method, it will use the method that returns the object to a fully processed state in the least time.</span></span>  
  
 <span data-ttu-id="e803a-106">通过处理设置可以控制要处理的对象以及用来处理这些对象的方法。</span><span class="sxs-lookup"><span data-stu-id="e803a-106">Processing settings let you control the objects that are processed, and the methods that are used to process those objects.</span></span> <span data-ttu-id="e803a-107">某些处理设置主要用于批处理作业。</span><span class="sxs-lookup"><span data-stu-id="e803a-107">Some processing settings are primarily used for batch processing jobs.</span></span> <span data-ttu-id="e803a-108">有关批处理的详细信息，请参阅[批处理 (Analysis Services)](batch-processing-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e803a-108">For more information about batch processing, see [Batch Processing &#40;Analysis Services&#41;](batch-processing-analysis-services.md).</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="e803a-109">本主题适用于多维和数据挖掘解决方案。</span><span class="sxs-lookup"><span data-stu-id="e803a-109">This topic applies to multidimensional and data mining solutions.</span></span> <span data-ttu-id="e803a-110">有关表格解决方案的信息，请参阅[处理数据库、表或分区](../tabular-models/process-database-table-or-partition-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e803a-110">For information about tabular solutions, see [Process Database, Table, or Partition](../tabular-models/process-database-table-or-partition-analysis-services.md).</span></span>  
  
## <a name="processing-options"></a><span data-ttu-id="e803a-111">处理选项</span><span class="sxs-lookup"><span data-stu-id="e803a-111">Processing Options</span></span>  
 <span data-ttu-id="e803a-112">下表介绍了可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中使用的处理方法，并标识了支持每种方法的对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-112">The following table describes the processing methods that are available in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], and identifies the objects for which each method is supported.</span></span>  
  
|<span data-ttu-id="e803a-113">Mode</span><span class="sxs-lookup"><span data-stu-id="e803a-113">Mode</span></span>|<span data-ttu-id="e803a-114">适用于</span><span class="sxs-lookup"><span data-stu-id="e803a-114">Applies to</span></span>|<span data-ttu-id="e803a-115">说明</span><span class="sxs-lookup"><span data-stu-id="e803a-115">Description</span></span>|  
|----------|----------------|-----------------|  
|<span data-ttu-id="e803a-116">**处理默认值**</span><span class="sxs-lookup"><span data-stu-id="e803a-116">**Process Default**</span></span>|<span data-ttu-id="e803a-117">多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-117">Cubes, databases, dimensions, measure groups, mining models, mining structures, and partitions.</span></span>|<span data-ttu-id="e803a-118">检测数据库对象的处理状态，进行必要的处理，将未处理对象或部分处理的对象转变成为已完全处理的对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-118">Detects the process state of database objects, and performs processing necessary to deliver unprocessed or partially processed objects to a fully processed state.</span></span> <span data-ttu-id="e803a-119">如果更改数据绑定，“处理默认值”将对受影响的对象执行“处理全部”。</span><span class="sxs-lookup"><span data-stu-id="e803a-119">If you change a data binding, Process Default will do a Process Full on the affected object.</span></span>|  
|<span data-ttu-id="e803a-120">**处理全部**</span><span class="sxs-lookup"><span data-stu-id="e803a-120">**Process Full**</span></span>|<span data-ttu-id="e803a-121">多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-121">Cubes, databases, dimensions, measure groups, mining models, mining structures, and partitions.</span></span>|<span data-ttu-id="e803a-122">处理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象及其包含的所有对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-122">Processes an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] object and all the objects that it contains.</span></span> <span data-ttu-id="e803a-123">对已被处理的对象执行“处理全部”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将删除该对象中的所有数据，然后再处理该对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-123">When Process Full is executed against an object that has already been processed, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] drops all data in the object, and then processes the object.</span></span> <span data-ttu-id="e803a-124">如果对对象进行了结构更改（例如，添加、删除或重命名属性层次结构），则需要此类处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-124">This kind of processing is required when a structural change has been made to an object, for example, when an attribute hierarchy is added, deleted, or renamed.</span></span>|  
|<span data-ttu-id="e803a-125">**处理清除**</span><span class="sxs-lookup"><span data-stu-id="e803a-125">**Process Clear**</span></span>|<span data-ttu-id="e803a-126">多维数据集、数据库、维度、度量值组、挖掘模型、挖掘结构和分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-126">Cubes, databases, dimensions, measure groups, mining models, mining structures, and partitions.</span></span>|<span data-ttu-id="e803a-127">删除指定对象和任何低级构成对象中的数据。</span><span class="sxs-lookup"><span data-stu-id="e803a-127">Drops the data in the object specified and any lower-level constituent objects.</span></span> <span data-ttu-id="e803a-128">该数据被删除后将不会被重新加载。</span><span class="sxs-lookup"><span data-stu-id="e803a-128">After the data is dropped, it is not reloaded.</span></span>|  
|<span data-ttu-id="e803a-129">**处理数据**</span><span class="sxs-lookup"><span data-stu-id="e803a-129">**Process Data**</span></span>|<span data-ttu-id="e803a-130">维度、多维数据集、度量值组和分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-130">Dimensions, cubes, measure groups, and partitions.</span></span>|<span data-ttu-id="e803a-131">只处理数据，而不生成聚合或索引。</span><span class="sxs-lookup"><span data-stu-id="e803a-131">Processes data only without building aggregations or indexes.</span></span> <span data-ttu-id="e803a-132">如果分区中有数据，则先删除数据，然后使用源数据重新填充分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-132">If there is data is in the partitions, it will be dropped before re-populating the partition with source data.</span></span>|  
|<span data-ttu-id="e803a-133">**处理添加**</span><span class="sxs-lookup"><span data-stu-id="e803a-133">**Process Add**</span></span>|<span data-ttu-id="e803a-134">维度、度量值组和分区</span><span class="sxs-lookup"><span data-stu-id="e803a-134">Dimensions, measure groups, and partitions</span></span><br /><br /> <span data-ttu-id="e803a-135">注意：“处理添加”  对于 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的维度处理不可用，但是你可以编写 XMLA 脚本执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e803a-135">Note: Process Add is not available for dimension processing in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], but you can write XMLA script performs this action.</span></span>|<span data-ttu-id="e803a-136">对于维度，添加新成员并更新维度属性标题和说明。</span><span class="sxs-lookup"><span data-stu-id="e803a-136">For dimensions, adds new members and updates dimension attribute captions and descriptions.</span></span><br /><br /> <span data-ttu-id="e803a-137">对于度量值组和分区，添加新的可用事实数据并只处理相关分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-137">For measure groups and partitions, adds newly available fact data and process only to the relevant partitions.</span></span>|  
|<span data-ttu-id="e803a-138">**处理更新**</span><span class="sxs-lookup"><span data-stu-id="e803a-138">**Process Update**</span></span>|<span data-ttu-id="e803a-139">维度</span><span class="sxs-lookup"><span data-stu-id="e803a-139">Dimensions</span></span>|<span data-ttu-id="e803a-140">强制重新读取数据并更新维度属性。</span><span class="sxs-lookup"><span data-stu-id="e803a-140">Forces a re-read of data and an update of dimension attributes.</span></span> <span data-ttu-id="e803a-141">将删除对相关分区的灵活聚合和索引。</span><span class="sxs-lookup"><span data-stu-id="e803a-141">Flexible aggregations and indexes on related partitions will be dropped.</span></span>|  
|<span data-ttu-id="e803a-142">**处理索引**</span><span class="sxs-lookup"><span data-stu-id="e803a-142">**Process Index**</span></span>|<span data-ttu-id="e803a-143">多维数据集、维度、度量值组和分区</span><span class="sxs-lookup"><span data-stu-id="e803a-143">Cubes, dimensions, measure groups, and partitions</span></span>|<span data-ttu-id="e803a-144">为所有已处理的分区创建或重新生成索引和聚合。</span><span class="sxs-lookup"><span data-stu-id="e803a-144">Creates or rebuilds indexes and aggregations for all processed partitions.</span></span> <span data-ttu-id="e803a-145">对于未处理的对象，此选项会生成错误。</span><span class="sxs-lookup"><span data-stu-id="e803a-145">For unprocessed objects, this option generates an error.</span></span><br /><br /> <span data-ttu-id="e803a-146">如果关闭“迟缓处理”，则需要使用此选项进行处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-146">Processing with this option is needed if you turn off Lazy Processing.</span></span>|  
|<span data-ttu-id="e803a-147">**处理结构**</span><span class="sxs-lookup"><span data-stu-id="e803a-147">**Process Structure**</span></span>|<span data-ttu-id="e803a-148">多维数据集和挖掘结构</span><span class="sxs-lookup"><span data-stu-id="e803a-148">Cubes and mining structures</span></span>|<span data-ttu-id="e803a-149">如果未处理多维数据集，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在必要时处理该多维数据集的所有维度。</span><span class="sxs-lookup"><span data-stu-id="e803a-149">If the cube is unprocessed, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] will process, if it is necessary, all the cube's dimensions.</span></span> <span data-ttu-id="e803a-150">然后， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将只创建多维数据集定义。</span><span class="sxs-lookup"><span data-stu-id="e803a-150">After that, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] will create only cube definitions.</span></span> <span data-ttu-id="e803a-151">如果将此选项应用于挖掘结构，则它将使用源数据填充挖掘结构。</span><span class="sxs-lookup"><span data-stu-id="e803a-151">If this option is applied to a mining structure, it populates the mining structure with source data.</span></span> <span data-ttu-id="e803a-152">此选项与“处理完全”选项之间的区别在于此选项不在挖掘模型自身中向下迭代处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-152">The difference between this option and the Process Full option is that this option does not iterate the processing down to the mining models themselves.</span></span>|  
|<span data-ttu-id="e803a-153">**处理清除结构**</span><span class="sxs-lookup"><span data-stu-id="e803a-153">**Process Clear Structure**</span></span>|<span data-ttu-id="e803a-154">挖掘结构</span><span class="sxs-lookup"><span data-stu-id="e803a-154">Mining structures</span></span>|<span data-ttu-id="e803a-155">从挖掘结构中删除所有定型数据。</span><span class="sxs-lookup"><span data-stu-id="e803a-155">Removes all training data from a mining structure.</span></span>|  
  
## <a name="processing-settings"></a><span data-ttu-id="e803a-156">处理设置</span><span class="sxs-lookup"><span data-stu-id="e803a-156">Processing Settings</span></span>  
 <span data-ttu-id="e803a-157">下表说明在创建处理操作时可以使用的处理设置。</span><span class="sxs-lookup"><span data-stu-id="e803a-157">The following table describes the processing settings that are available for use when you create a process operation.</span></span>  
  
|<span data-ttu-id="e803a-158">处理选项</span><span class="sxs-lookup"><span data-stu-id="e803a-158">Processing Option</span></span>|<span data-ttu-id="e803a-159">说明</span><span class="sxs-lookup"><span data-stu-id="e803a-159">Description</span></span>|  
|-----------------------|-----------------|  
|<span data-ttu-id="e803a-160">**Parallel**</span><span class="sxs-lookup"><span data-stu-id="e803a-160">**Parallel**</span></span>|<span data-ttu-id="e803a-161">用于批处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-161">Used for batch processing.</span></span> <span data-ttu-id="e803a-162">此设置会使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将处理任务分开在单个事务内并行执行。</span><span class="sxs-lookup"><span data-stu-id="e803a-162">This setting causes [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] to fork off processing tasks to run in parallel inside a single transaction.</span></span> <span data-ttu-id="e803a-163">如果出现故障，则结果是回滚所有更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-163">If there is a failure, the result is a roll-back of all changes.</span></span> <span data-ttu-id="e803a-164">您可以显式设置并行任务的最大数目，或者让服务器确定最佳分布。</span><span class="sxs-lookup"><span data-stu-id="e803a-164">You can set the maximum number of parallel tasks explicitly, or let the server decide the optimal distribution.</span></span> <span data-ttu-id="e803a-165">“并行”选项对于提高处理速度十分有用。</span><span class="sxs-lookup"><span data-stu-id="e803a-165">The Parallel option is useful for speeding up processing.</span></span>|  
|<span data-ttu-id="e803a-166">**按顺序（事务模式）**</span><span class="sxs-lookup"><span data-stu-id="e803a-166">**Sequential (Transaction Mode)**</span></span>|<span data-ttu-id="e803a-167">控制处理作业的执行行为。</span><span class="sxs-lookup"><span data-stu-id="e803a-167">Controls the execution behavior of the processing job.</span></span> <span data-ttu-id="e803a-168">使用 **“一项事务”** 进行处理时，将在处理作业成功后提交所有更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-168">When you process using **One Transaction**, all changes are committed after the processing job succeeds.</span></span> <span data-ttu-id="e803a-169">也就是说，受特定处理作业影响的所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象将保持对查询可用，直到提交进程为止。</span><span class="sxs-lookup"><span data-stu-id="e803a-169">This means that all [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objects affected by a particular processing job remain available for queries until the commit process.</span></span> <span data-ttu-id="e803a-170">这样，对象会暂时不可用。</span><span class="sxs-lookup"><span data-stu-id="e803a-170">This makes the objects temporarily unavailable.</span></span> <span data-ttu-id="e803a-171">使用 **“单独的事务”** 将使处理作业中受某进程影响的所有对象一旦在该进程成功后就无法用于查询。</span><span class="sxs-lookup"><span data-stu-id="e803a-171">Using **Separate Transactions** causes all objects that are affected by a process in processing job to be taken unavailable for queries as soon as that process succeeds.</span></span> <span data-ttu-id="e803a-172">两个可用选项是：</span><span class="sxs-lookup"><span data-stu-id="e803a-172">The two available options are:</span></span><br /><br /> <span data-ttu-id="e803a-173">**一项事务**。</span><span class="sxs-lookup"><span data-stu-id="e803a-173">**One Transaction**.</span></span> <span data-ttu-id="e803a-174">处理作业作为事务运行。</span><span class="sxs-lookup"><span data-stu-id="e803a-174">The processing job runs as a transaction.</span></span> <span data-ttu-id="e803a-175">如果处理作业内的所有进程都成功，则提交处理作业所做的所有更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-175">If all processes inside the processing job succeed, all changes by the processing job are committed.</span></span> <span data-ttu-id="e803a-176">如果有一个进程失败，则回滚处理作业所做的所有更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-176">If one process fails, all changes by the processing job are rolled back.</span></span> <span data-ttu-id="e803a-177">**“一项事务”** 是默认值。</span><span class="sxs-lookup"><span data-stu-id="e803a-177">**One Transaction** is the default value.</span></span><br /><br /> <span data-ttu-id="e803a-178">**单独的事务**。</span><span class="sxs-lookup"><span data-stu-id="e803a-178">**Separate Transactions**.</span></span> <span data-ttu-id="e803a-179">处理作业中的每个进程都作为独立的作业运行。</span><span class="sxs-lookup"><span data-stu-id="e803a-179">Each process in the processing job runs as a stand-alone job.</span></span> <span data-ttu-id="e803a-180">如果某个进程失败，则仅回滚该进程，处理作业继续执行。</span><span class="sxs-lookup"><span data-stu-id="e803a-180">If one process fails, only that process is rolled back and the processing job continues.</span></span> <span data-ttu-id="e803a-181">每个作业将在作业结束时提交所有进程更改。</span><span class="sxs-lookup"><span data-stu-id="e803a-181">Each job commits all process changes at the end of the job.</span></span>|  
|<span data-ttu-id="e803a-182">**写回表选项**</span><span class="sxs-lookup"><span data-stu-id="e803a-182">**Writeback Table Option**</span></span>|<span data-ttu-id="e803a-183">控制在处理过程中如何处理写回表。</span><span class="sxs-lookup"><span data-stu-id="e803a-183">Controls how writeback tables are handled during processing.</span></span> <span data-ttu-id="e803a-184">此选项应用于多维数据集中的写回分区，有下列选项可供使用：</span><span class="sxs-lookup"><span data-stu-id="e803a-184">This option applies to writeback partitions in a cube, and uses the following options:</span></span><br /><br /> <span data-ttu-id="e803a-185">**使用现有**的。</span><span class="sxs-lookup"><span data-stu-id="e803a-185">**Use Existing**.</span></span> <span data-ttu-id="e803a-186">使用现有的写回表。</span><span class="sxs-lookup"><span data-stu-id="e803a-186">Uses the existing writeback table.</span></span> <span data-ttu-id="e803a-187">这是默认值。</span><span class="sxs-lookup"><span data-stu-id="e803a-187">This is default value.</span></span><br /><br /> <span data-ttu-id="e803a-188">**Create**。</span><span class="sxs-lookup"><span data-stu-id="e803a-188">**Create**.</span></span> <span data-ttu-id="e803a-189">创建一个新的写回表，如果已经存在一个写回表，则会导致进程失败。</span><span class="sxs-lookup"><span data-stu-id="e803a-189">Creates a new writeback table and causes the process to fail if one already exists.</span></span><br /><br /> <span data-ttu-id="e803a-190">**始终创建**。</span><span class="sxs-lookup"><span data-stu-id="e803a-190">**Create Always**.</span></span> <span data-ttu-id="e803a-191">即使已经存在一个写回表，也要创建一个新的写回表。</span><span class="sxs-lookup"><span data-stu-id="e803a-191">Creates a new writeback table even if one already exists.</span></span> <span data-ttu-id="e803a-192">现有表将被删除和替换。</span><span class="sxs-lookup"><span data-stu-id="e803a-192">An existing table is deleted and replaced.</span></span>|  
|<span data-ttu-id="e803a-193">**处理受影响的对象**</span><span class="sxs-lookup"><span data-stu-id="e803a-193">**Process Affected Objects**</span></span>|<span data-ttu-id="e803a-194">控制处理作业的对象范围。</span><span class="sxs-lookup"><span data-stu-id="e803a-194">Controls the object scope of the processing job.</span></span> <span data-ttu-id="e803a-195">受影响的对象由对象依赖关系定义。</span><span class="sxs-lookup"><span data-stu-id="e803a-195">An affected object is defined by object dependency.</span></span> <span data-ttu-id="e803a-196">例如，分区依赖于确定聚合的维度，但是维度不依赖于分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-196">For example, partitions are dependent on the dimensions that determine aggregation, but dimensions are not dependent on partitions.</span></span> <span data-ttu-id="e803a-197">您可以使用下列选项：</span><span class="sxs-lookup"><span data-stu-id="e803a-197">You can use the following options:</span></span><br /><br /> <span data-ttu-id="e803a-198">**False**。</span><span class="sxs-lookup"><span data-stu-id="e803a-198">**False**.</span></span> <span data-ttu-id="e803a-199">作业将处理作业中显式命名的对象以及所有依赖对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-199">The job processes the objects explicitly named in the job and all dependent objects.</span></span> <span data-ttu-id="e803a-200">例如，如果处理作业仅包含维度，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅处理作业中显式标识的那些对象。</span><span class="sxs-lookup"><span data-stu-id="e803a-200">For example, if the processing job contains only dimensions, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processes just those objects explicitly identified in the job.</span></span> <span data-ttu-id="e803a-201">如果处理作业包含分区，分区处理将自动调用受影响维度的处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-201">If the processing job contains partitions, partition processing automatically invokes processing of affected dimensions.</span></span> <span data-ttu-id="e803a-202">**“False”** 是默认设置。</span><span class="sxs-lookup"><span data-stu-id="e803a-202">**False** is the default setting.</span></span><br /><br /> <span data-ttu-id="e803a-203">**True**。</span><span class="sxs-lookup"><span data-stu-id="e803a-203">**True**.</span></span> <span data-ttu-id="e803a-204">作业将处理作业中显式命名的对象、所有依赖对象以及受正在处理的对象影响的所有对象（不更改受影响对象的状态）。</span><span class="sxs-lookup"><span data-stu-id="e803a-204">The job processes the objects explicitly named in the job, all dependent objects, and all objects affected by the objects being processed without changing the state of the affected objects.</span></span> <span data-ttu-id="e803a-205">例如，如果处理作业仅包含维度， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还将处理受当前已处理分区的维度处理影响的所有分区。</span><span class="sxs-lookup"><span data-stu-id="e803a-205">For example, if the processing job contains only dimensions, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] also processes all partitions affected by the dimension processing for partitions that are currently in a processed state.</span></span> <span data-ttu-id="e803a-206">如果受影响分区当前处于未处理状态，则不会对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-206">Affected partitions that are currently in an unprocessed state are not processed.</span></span> <span data-ttu-id="e803a-207">不过，由于分区依赖于维度，因此如果处理作业仅包含分区，分区处理将自动调用受影响维度的处理，即使维度当前处于未处理状态也是如此。</span><span class="sxs-lookup"><span data-stu-id="e803a-207">However, because partitions are dependent on dimensions, if the processing job contains only partitions, partition processing automatically invokes processing of affected dimensions, even when the dimension is currently in an unprocessed state.</span></span>|  
|<span data-ttu-id="e803a-208">**维度键错误**</span><span class="sxs-lookup"><span data-stu-id="e803a-208">**Dimension Key Errors**</span></span>|<span data-ttu-id="e803a-209">确定在处理过程中发生错误时 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 执行的操作。</span><span class="sxs-lookup"><span data-stu-id="e803a-209">Determines the action taken by [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] when errors occur during processing.</span></span> <span data-ttu-id="e803a-210">选择“使用默认错误配置”时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用针对要处理的每个对象设置的错误配置。</span><span class="sxs-lookup"><span data-stu-id="e803a-210">When you select Use default error configuration, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] uses the error configuration that is set for each object being processed.</span></span> <span data-ttu-id="e803a-211">如果将对象设置为使用默认的配置设置，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用为每个选项列出的默认设置。</span><span class="sxs-lookup"><span data-stu-id="e803a-211">If an object is set to use default configuration settings, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] uses the default settings that are listed for each option.</span></span> <span data-ttu-id="e803a-212">选择 "**使用自定义错误配置**" 时，可以选择以下操作的值来控制错误处理行为：</span><span class="sxs-lookup"><span data-stu-id="e803a-212">When you select **Use custom error configuration**, you can select values for the following actions to control error-handling behavior:</span></span><br /><br /> <span data-ttu-id="e803a-213">**键错误操作**。</span><span class="sxs-lookup"><span data-stu-id="e803a-213">**Key error action**.</span></span> <span data-ttu-id="e803a-214">如果记录中并不存在某个键值，则选择执行下列一项操作：</span><span class="sxs-lookup"><span data-stu-id="e803a-214">If a key value does not yet exist in a record, one of these actions is selected to occur:</span></span><br /><br /> <span data-ttu-id="e803a-215">**转换为未知**。</span><span class="sxs-lookup"><span data-stu-id="e803a-215">**Convert to unknown**.</span></span> <span data-ttu-id="e803a-216">键被解释为未知成员。</span><span class="sxs-lookup"><span data-stu-id="e803a-216">The key is interpreted as an unknown member.</span></span> <span data-ttu-id="e803a-217">这是默认设置。</span><span class="sxs-lookup"><span data-stu-id="e803a-217">This is the default setting.</span></span><br /><br /> <span data-ttu-id="e803a-218">**放弃记录**。</span><span class="sxs-lookup"><span data-stu-id="e803a-218">**Discard record**.</span></span> <span data-ttu-id="e803a-219">将放弃记录。</span><span class="sxs-lookup"><span data-stu-id="e803a-219">The record is discarded.</span></span>|  
||<span data-ttu-id="e803a-220">**处理错误限制**。</span><span class="sxs-lookup"><span data-stu-id="e803a-220">**Processing error limit**.</span></span> <span data-ttu-id="e803a-221">通过选择下列一个选项控制处理的错误数：</span><span class="sxs-lookup"><span data-stu-id="e803a-221">Controls the number of errors processed by selecting one of these options:</span></span><br /><br /> <span data-ttu-id="e803a-222">**忽略错误计数**。</span><span class="sxs-lookup"><span data-stu-id="e803a-222">**Ignore errors count**.</span></span> <span data-ttu-id="e803a-223">这将使处理继续进行，而不管错误数是多少。</span><span class="sxs-lookup"><span data-stu-id="e803a-223">This will enable processing to continue regardless of the number of errors.</span></span> <br /><span data-ttu-id="e803a-224">**出错时停止**。</span><span class="sxs-lookup"><span data-stu-id="e803a-224">**Stop on error**.</span></span> <span data-ttu-id="e803a-225">使用此选项，您可以控制其他两项设置。</span><span class="sxs-lookup"><span data-stu-id="e803a-225">With this option, you control two additional settings.</span></span> <span data-ttu-id="e803a-226">**“错误数”** 可以限制在出现特定错误数之后处理。</span><span class="sxs-lookup"><span data-stu-id="e803a-226">**Number of errors** lets you limit processing to the occurrence of a specific number of errors.</span></span> <span data-ttu-id="e803a-227">**“出错时要执行的操作”** 允许您确定达到 **“错误数”** 时的操作。</span><span class="sxs-lookup"><span data-stu-id="e803a-227">**On error action** lets you determine the action when **Number of errors** is reached.</span></span> <span data-ttu-id="e803a-228">您可以选择 **“停止处理”**，这将使处理作业失败并回滚任何更改；也可以选择 **“停止日志记录”**，这将使处理继续进行，而不记录错误。</span><span class="sxs-lookup"><span data-stu-id="e803a-228">You can select **Stop processing**, which causes the processing job to fail and roll back any changes, or **Stop logging**, which enables processing to continue without logging errors.</span></span> <span data-ttu-id="e803a-229">**“出错时停止”** 是默认设置，其中 **“错误数”** 设置为 **0** ， **“出错时要执行的操作”** 设置为 **“停止处理”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-229">**Stop on error** is the default setting with **Number of errors** set to **0** and **On error action** set to **Stop processing**.</span></span>|  
||<span data-ttu-id="e803a-230">特定错误条件。</span><span class="sxs-lookup"><span data-stu-id="e803a-230">Specific error conditions.</span></span> <span data-ttu-id="e803a-231">您可以设置下列选项来控制特定的错误处理行为：</span><span class="sxs-lookup"><span data-stu-id="e803a-231">You can set the following options to control specific error-handling behavior:</span></span><br /><br /> <span data-ttu-id="e803a-232">**找不到键**。</span><span class="sxs-lookup"><span data-stu-id="e803a-232">**Key not found**.</span></span> <span data-ttu-id="e803a-233">当键值存在于分区中，但不存在于相应的维度中时发生。</span><span class="sxs-lookup"><span data-stu-id="e803a-233">Occurs when a key value exists in a partition but does not exist in the corresponding dimension.</span></span> <span data-ttu-id="e803a-234">默认设置是 **“报告并继续”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-234">The default setting is **Report and continue**.</span></span> <span data-ttu-id="e803a-235">其他设置是 **“忽略错误”** 和 **“报告并停止”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-235">Other settings are **Ignore error** and **Report and stop**.</span></span><br /><br /> <span data-ttu-id="e803a-236">**重复键**。</span><span class="sxs-lookup"><span data-stu-id="e803a-236">**Duplicate key**.</span></span> <span data-ttu-id="e803a-237">当维度中存在多个键值时发生。</span><span class="sxs-lookup"><span data-stu-id="e803a-237">Occurs when more than one key value exists in a dimension.</span></span> <span data-ttu-id="e803a-238">默认设置是 **“忽略错误”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-238">The default setting is **Ignore error**.</span></span> <span data-ttu-id="e803a-239">其他设置是 **“报告并继续”** 和 **“报告并停止”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-239">Other settings are **Report and continue** and **Report and stop**.</span></span><br /><br /> <span data-ttu-id="e803a-240">**空键转换为未知键**。</span><span class="sxs-lookup"><span data-stu-id="e803a-240">**Null key converted to unknown**.</span></span> <span data-ttu-id="e803a-241">当键值为空值且 **“键错误操作”** 设置为 **“转换为未知”** 时发生。</span><span class="sxs-lookup"><span data-stu-id="e803a-241">Occurs when a key value is null and the **Key error action** is set to **Convert to unknown**.</span></span> <span data-ttu-id="e803a-242">默认设置是 **“忽略错误”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-242">The default setting is **Ignore error**.</span></span> <span data-ttu-id="e803a-243">其他设置是 **“报告并继续”** 和 **“报告并停止”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-243">Other settings are **Report and continue** and **Report and stop**.</span></span><br /><br /> <span data-ttu-id="e803a-244">**不允许空键**。</span><span class="sxs-lookup"><span data-stu-id="e803a-244">**Null key not allowed**.</span></span> <span data-ttu-id="e803a-245">当 **“键错误操作”** 设置为 **“放弃记录”** 时发生。</span><span class="sxs-lookup"><span data-stu-id="e803a-245">Occurs when **Key error action** is set to **Discard record**.</span></span> <span data-ttu-id="e803a-246">默认设置是 **“报告并继续”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-246">The default setting is **Report and continue**.</span></span> <span data-ttu-id="e803a-247">其他设置是 **“忽略错误”** 和 **“报告并停止”**。</span><span class="sxs-lookup"><span data-stu-id="e803a-247">Other settings are **Ignore error** and **Report and stop**.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="e803a-248">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e803a-248">See Also</span></span>  
 [<span data-ttu-id="e803a-249">多维模型对象处理</span><span class="sxs-lookup"><span data-stu-id="e803a-249">Multidimensional Model Object Processing</span></span>](processing-a-multidimensional-model-analysis-services.md)  
  
  