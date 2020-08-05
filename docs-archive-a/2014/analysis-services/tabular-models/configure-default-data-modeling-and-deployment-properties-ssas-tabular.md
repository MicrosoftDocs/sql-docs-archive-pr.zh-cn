---
title: " (SSAS 表格) 配置默认数据建模和部署属性 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deployment.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql12.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
author: minewiskan
ms.author: owend
ms.openlocfilehash: 62d3697a0308eab51002867347df63145decfa93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580418"
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a><span data-ttu-id="385d1-102">配置默认数据建模和部署属性（SSAS 表格）</span><span class="sxs-lookup"><span data-stu-id="385d1-102">Configure Default Data Modeling and Deployment Properties (SSAS Tabular)</span></span>
  <span data-ttu-id="385d1-103">本主题介绍如何配置可为在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建的每个新表格模型项目预定义的默认兼容级别、部署和工作区数据库属性设置。</span><span class="sxs-lookup"><span data-stu-id="385d1-103">This topic describes how to configure the default compatibility level, deployment and workspace database property settings, which can be pre-defined for each new tabular model project you create in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].</span></span> <span data-ttu-id="385d1-104">在创建新项目之后，根据您的特定需求，仍可以更改这些属性。</span><span class="sxs-lookup"><span data-stu-id="385d1-104">After a new project is created, these properties can still be changed depending on your particular requirements.</span></span>  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a><span data-ttu-id="385d1-105">为新模型项目配置默认的兼容级别属性</span><span class="sxs-lookup"><span data-stu-id="385d1-105">To configure the default Compatibility Level property setting for new model projects</span></span>  
  
1.  <span data-ttu-id="385d1-106">在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-106">In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], click the **Tools** menu, and then click **Options**.</span></span>  
  
2.  <span data-ttu-id="385d1-107">在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“兼容级别”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-107">In the **Options** dialog box, expand **Analysis Services Tabular Designers**, and then click **Compatibility Level**.</span></span>  
  
3.  <span data-ttu-id="385d1-108">配置以下属性设置：</span><span class="sxs-lookup"><span data-stu-id="385d1-108">Configure the following property settings:</span></span>  
  
    |<span data-ttu-id="385d1-109">属性</span><span class="sxs-lookup"><span data-stu-id="385d1-109">Property</span></span>|<span data-ttu-id="385d1-110">默认设置</span><span class="sxs-lookup"><span data-stu-id="385d1-110">Default setting</span></span>|<span data-ttu-id="385d1-111">说明</span><span class="sxs-lookup"><span data-stu-id="385d1-111">Description</span></span>|  
    |--------------|---------------------|-----------------|  
    |<span data-ttu-id="385d1-112">**新项目的默认兼容级别**</span><span class="sxs-lookup"><span data-stu-id="385d1-112">**Default compatibility level for new projects**</span></span>|<span data-ttu-id="385d1-113">SQL Server 2012 (1100) </span><span class="sxs-lookup"><span data-stu-id="385d1-113">SQL Server 2012 (1100)</span></span>|<span data-ttu-id="385d1-114">此设置指定在创建新的表格模型项目时要使用的默认兼容级别。</span><span class="sxs-lookup"><span data-stu-id="385d1-114">This setting specifies the default compatibility level to use when creating a new Tabular model project.</span></span> <span data-ttu-id="385d1-115">如果要部署到未应用 SP1 的 Analysis Services 实例，则可以选择 SQL Server 2012 RTM (1100)；如果您的部署实例已应用 SP1，则可以选择 SQL Server 2012 SP1 或 SQL Server 2014。</span><span class="sxs-lookup"><span data-stu-id="385d1-115">You can choose SQL Server 2012 RTM (1100) if you will deploy to an Analysis Services instance without SP1 applied, or SQL Server 2012 SP1 if your deployment instance has SP1 applied, or SQL Server 2014.</span></span> <span data-ttu-id="385d1-116">有关详细信息，请参阅[&#40;SSAS 表格 SP1&#41;兼容级别](compatibility-level-for-tabular-models-in-analysis-services.md)。</span><span class="sxs-lookup"><span data-stu-id="385d1-116">For more information, see [Compatibility Level &#40;SSAS Tabular SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md).</span></span>|  
    |<span data-ttu-id="385d1-117">**兼容级别选项**</span><span class="sxs-lookup"><span data-stu-id="385d1-117">**Compatibility level options**</span></span>|<span data-ttu-id="385d1-118">全选中</span><span class="sxs-lookup"><span data-stu-id="385d1-118">All checked</span></span>|<span data-ttu-id="385d1-119">为新的表格模型项目和在部署到其他 Analysis Services 实例时指定兼容级别选项。</span><span class="sxs-lookup"><span data-stu-id="385d1-119">Specifies compatibility level options for new Tabular model projects and when deploying to another Analysis Services instance.</span></span>|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a><span data-ttu-id="385d1-120">为新模型项目配置默认的部署服务器属性设置</span><span class="sxs-lookup"><span data-stu-id="385d1-120">To configure the default deployment server property setting for new model projects</span></span>  
  
1.  <span data-ttu-id="385d1-121">在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-121">In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], click the **Tools** menu, and then click **Options**.</span></span>  
  
2.  <span data-ttu-id="385d1-122">在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“部署”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-122">In the **Options** dialog box, expand **Analysis Services Tabular Designers**, and then click **Deployment**.</span></span>  
  
3.  <span data-ttu-id="385d1-123">配置以下属性设置：</span><span class="sxs-lookup"><span data-stu-id="385d1-123">Configure the following property settings:</span></span>  
  
    |<span data-ttu-id="385d1-124">属性</span><span class="sxs-lookup"><span data-stu-id="385d1-124">Property</span></span>|<span data-ttu-id="385d1-125">默认设置</span><span class="sxs-lookup"><span data-stu-id="385d1-125">Default setting</span></span>|<span data-ttu-id="385d1-126">说明</span><span class="sxs-lookup"><span data-stu-id="385d1-126">Description</span></span>|  
    |--------------|---------------------|-----------------|  
    |<span data-ttu-id="385d1-127">**默认部署服务器**</span><span class="sxs-lookup"><span data-stu-id="385d1-127">**Default deployment server**</span></span>|<span data-ttu-id="385d1-128">localhost</span><span class="sxs-lookup"><span data-stu-id="385d1-128">localhost</span></span>|<span data-ttu-id="385d1-129">此设置指定在部署模型时要使用的默认服务器。</span><span class="sxs-lookup"><span data-stu-id="385d1-129">This setting specifies the default server to use when deploying a model.</span></span> <span data-ttu-id="385d1-130">您可以单击向下箭头以浏览您可以使用的本地网络 Analysis Services 服务器，也可以键入远程服务器的名称。</span><span class="sxs-lookup"><span data-stu-id="385d1-130">You can click the down arrow to browse for local network Analysis Services servers you can use or you can type the name of a remote server.</span></span>|  
  
    > [!NOTE]  
    >  <span data-ttu-id="385d1-131">更改默认的部署服务器属性设置将不会影响在更改之前创建的现有项目。</span><span class="sxs-lookup"><span data-stu-id="385d1-131">Changes to the Default deployment Server property setting will not affect existing projects created prior to the change.</span></span>  
  
###  <a name="to-configure-the-default-workspace-database-property-settings-for-new-model-projects"></a><a name="bkmk_conf_default"></a><span data-ttu-id="385d1-132">为新模型项目配置默认的工作区数据库属性设置</span><span class="sxs-lookup"><span data-stu-id="385d1-132">To configure the default Workspace Database property settings for new model projects</span></span>  
  
1.  <span data-ttu-id="385d1-133">在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-133">In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], click the **Tools** menu, and then click **Options**.</span></span>  
  
2.  <span data-ttu-id="385d1-134">在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“工作区数据库”**。</span><span class="sxs-lookup"><span data-stu-id="385d1-134">In the **Options** dialog box, expand **Analysis Services Tabular Designers**, and then click **Workspace Database**.</span></span>  
  
3.  <span data-ttu-id="385d1-135">配置以下属性设置：</span><span class="sxs-lookup"><span data-stu-id="385d1-135">Configure the following property settings:</span></span>  
  
    |<span data-ttu-id="385d1-136">属性</span><span class="sxs-lookup"><span data-stu-id="385d1-136">Property</span></span>|<span data-ttu-id="385d1-137">默认设置</span><span class="sxs-lookup"><span data-stu-id="385d1-137">Default setting</span></span>|<span data-ttu-id="385d1-138">说明</span><span class="sxs-lookup"><span data-stu-id="385d1-138">Description</span></span>|  
    |--------------|---------------------|-----------------|  
    |<span data-ttu-id="385d1-139">**默认工作区服务器**</span><span class="sxs-lookup"><span data-stu-id="385d1-139">**Default workspace server**</span></span>|<span data-ttu-id="385d1-140">**localhost**</span><span class="sxs-lookup"><span data-stu-id="385d1-140">**localhost**</span></span>|<span data-ttu-id="385d1-141">此属性指定在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创作模型时将用于承载工作区数据库的默认服务器。</span><span class="sxs-lookup"><span data-stu-id="385d1-141">This property specifies the default server that will be used to host the workspace database while the model is being authored in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].</span></span> <span data-ttu-id="385d1-142">在本地计算机上运行的 Analysis Services 的所有可用实例都将包括在列表框中。</span><span class="sxs-lookup"><span data-stu-id="385d1-142">All available instances of Analysis Services running on the local computer are included in the listbox.</span></span><br /><br /> <span data-ttu-id="385d1-143">注意：建议你始终将本地 Analysis Services 服务器指定为工作区服务器。</span><span class="sxs-lookup"><span data-stu-id="385d1-143">Note: It is recommended that you always specify a local Analysis Services server as the workspace server.</span></span> <span data-ttu-id="385d1-144">对于远程服务器上的工作区数据库，不支持从 PowerPivot 导入数据，数据不能在本地备份，并且在查询过程中用户界面可能会遇到滞后的情况。</span><span class="sxs-lookup"><span data-stu-id="385d1-144">For workspace databases on a remote server, importing data from PowerPivot is not supported, data cannot be backed up locally, and the user interface may experience latency during queries.</span></span>|  
    |<span data-ttu-id="385d1-145">**在关闭模型后工作区数据库保留**</span><span class="sxs-lookup"><span data-stu-id="385d1-145">**Workspace database retention after the model is closed**</span></span>|<span data-ttu-id="385d1-146">**在磁盘上保留工作区数据库，但从内存中卸载**</span><span class="sxs-lookup"><span data-stu-id="385d1-146">**Keep workspace databases on disk, but unload from memory**</span></span>|<span data-ttu-id="385d1-147">指定在关闭某一模型后将如何保留工作区数据库。</span><span class="sxs-lookup"><span data-stu-id="385d1-147">Specifies how a workspace database is retained after a model is closed.</span></span> <span data-ttu-id="385d1-148">工作区数据库将包括模型元数据、导入到模型中的数据以及模拟凭据（已加密）。</span><span class="sxs-lookup"><span data-stu-id="385d1-148">A workspace database includes model metadata, the data imported into a model, and impersonation credentials (encrypted).</span></span> <span data-ttu-id="385d1-149">在某些情况下，工作区数据库可能会非常大并且占用大量内存。</span><span class="sxs-lookup"><span data-stu-id="385d1-149">In some cases, the workspace database can be very large and consume a significant amount of memory.</span></span> <span data-ttu-id="385d1-150">默认情况下，工作区数据库将从内存中删除。</span><span class="sxs-lookup"><span data-stu-id="385d1-150">By default, workspace databases are removed from memory.</span></span> <span data-ttu-id="385d1-151">在更改此设置时，一定要考虑您的可用内存资源以及计划处理该模型的频繁程度。</span><span class="sxs-lookup"><span data-stu-id="385d1-151">When changing this setting, it is important to consider your available memory resources as well as how often you plan to work on the model.</span></span> <span data-ttu-id="385d1-152">此属性设置具有以下选项：</span><span class="sxs-lookup"><span data-stu-id="385d1-152">This property setting has the following options:</span></span><br /><br /> <span data-ttu-id="385d1-153">**在内存中保留工作区** - 指定在关闭模型后将工作区保留在内存中。</span><span class="sxs-lookup"><span data-stu-id="385d1-153">**Keep workspaces in memory** - Specifies to keep workspaces in memory after a model is closed.</span></span> <span data-ttu-id="385d1-154">此选项将会占用较多内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用较少的资源并且工作区将更快加载。</span><span class="sxs-lookup"><span data-stu-id="385d1-154">This option will consume more memory; however, when opening a model in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], fewer resources are consumed and the workspace will load faster.</span></span><br /><br /> <span data-ttu-id="385d1-155">**在磁盘上保留工作区数据库，但从内存中卸载** - 指定将工作区数据库保留在磁盘上，但在关闭模型后将不再保留在内存中。</span><span class="sxs-lookup"><span data-stu-id="385d1-155">**Keep workspace databases on disk, but unload from memory** - Specifies to keep the workspace database on disk, but no longer in memory after a model is closed.</span></span> <span data-ttu-id="385d1-156">此选项将会占用较少内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区保留在内存中相比，模型的加载速度将更慢。</span><span class="sxs-lookup"><span data-stu-id="385d1-156">This option will consume less memory; however, when opening a model in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], additional resources are consumed and the model will load more slowly than if the workspace database is kept in memory.</span></span> <span data-ttu-id="385d1-157">在内存中资源受到限制或在处理远程工作区数据库时，将使用此选项。</span><span class="sxs-lookup"><span data-stu-id="385d1-157">Use this option when in-memory resources are limited or when working on a remote workspace database.</span></span><br /><br /> <span data-ttu-id="385d1-158">**删除工作区** - 指定从内存中删除工作区数据库，在关闭模型后不将工作区数据库保留在磁盘上。</span><span class="sxs-lookup"><span data-stu-id="385d1-158">**Delete workspace** - Specifies to delete workspace database from memory and not keep workspace database on disk after the model is closed.</span></span> <span data-ttu-id="385d1-159">此选项将会占用较少内存和存储空间；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区数据库保留在内存中或磁盘上相比，模型的加载速度将更慢。</span><span class="sxs-lookup"><span data-stu-id="385d1-159">This option will consume less memory and storage space; however, when opening a model in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], additional resources are consumed and the model will load more slowly than if the workspace database is kept in memory or on-disk.</span></span> <span data-ttu-id="385d1-160">只有在偶尔处理模型时，才使用此选项。</span><span class="sxs-lookup"><span data-stu-id="385d1-160">Use this option when only occasionally working on models.</span></span>|  
    |<span data-ttu-id="385d1-161">**数据备份**</span><span class="sxs-lookup"><span data-stu-id="385d1-161">**Data backup**</span></span>|<span data-ttu-id="385d1-162">**在磁盘上保留数据的备份**</span><span class="sxs-lookup"><span data-stu-id="385d1-162">**Keep backup of data on disk**</span></span>|<span data-ttu-id="385d1-163">指定模型数据的备份是否将保留在备份文件中。</span><span class="sxs-lookup"><span data-stu-id="385d1-163">Specifies whether or not a backup of the model data is kept in a backup file.</span></span> <span data-ttu-id="385d1-164">此属性设置具有以下选项：</span><span class="sxs-lookup"><span data-stu-id="385d1-164">This property setting has the following options:</span></span><br /><br /> <span data-ttu-id="385d1-165">**在磁盘上保留数据的备份** - 指定将模型数据的备份保留在磁盘上。</span><span class="sxs-lookup"><span data-stu-id="385d1-165">**Keep backup of data on disk** - Specifies to keep a backup of model data on disk.</span></span> <span data-ttu-id="385d1-166">在保存模型时，数据也将保存到备份 (ABF) 文件中。</span><span class="sxs-lookup"><span data-stu-id="385d1-166">When the model is saved, the data will also be saved to the backup (ABF) file.</span></span> <span data-ttu-id="385d1-167">选择此选项可能导致保存和加载模型的速度变慢</span><span class="sxs-lookup"><span data-stu-id="385d1-167">Selecting this option can cause slower model save and load times</span></span><br /><br /> <span data-ttu-id="385d1-168">**不在磁盘上保留数据的备份** - 指定不将模型数据的备份保留在磁盘上。</span><span class="sxs-lookup"><span data-stu-id="385d1-168">**Do not keep backup of databack on disk** - Specifies to not keep a backup of model data on disk.</span></span> <span data-ttu-id="385d1-169">此选项将保存时间和模型加载时间降至最低。</span><span class="sxs-lookup"><span data-stu-id="385d1-169">This option will minimize save and model loading time.</span></span>|  
  
> [!NOTE]  
>  <span data-ttu-id="385d1-170">更改默认的模型属性将不会影响更改之前创建的现有模型。</span><span class="sxs-lookup"><span data-stu-id="385d1-170">Changes to default model properties will not affect properties for existing models created prior to the change.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="385d1-171">另请参阅</span><span class="sxs-lookup"><span data-stu-id="385d1-171">See Also</span></span>  
 <span data-ttu-id="385d1-172">[&#40;SSAS 表格&#41;的项目属性](properties-ssas-tabular.md) </span><span class="sxs-lookup"><span data-stu-id="385d1-172">[Project Properties &#40;SSAS Tabular&#41;](properties-ssas-tabular.md) </span></span>  
 <span data-ttu-id="385d1-173">[&#40;SSAS 表格&#41;的模型属性](model-properties-ssas-tabular.md) </span><span class="sxs-lookup"><span data-stu-id="385d1-173">[Model Properties &#40;SSAS Tabular&#41;](model-properties-ssas-tabular.md) </span></span>  
 [<span data-ttu-id="385d1-174">SSAS 表格 SP1&#41;兼容级别 &#40;</span><span class="sxs-lookup"><span data-stu-id="385d1-174">Compatibility Level &#40;SSAS Tabular SP1&#41;</span></span>](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  