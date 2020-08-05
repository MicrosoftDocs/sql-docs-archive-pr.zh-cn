---
title: 为解决方案部署指定配置设置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
author: minewiskan
ms.author: owend
ms.openlocfilehash: 83b08ce2b6296a5098c1b21a3afa443668c481a1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580944"
---
# <a name="specifying-configuration-settings-for-solution-deployment"></a><span data-ttu-id="73f06-102">为解决方案部署指定配置设置</span><span class="sxs-lookup"><span data-stu-id="73f06-102">Specifying Configuration Settings for Solution Deployment</span></span>
  <span data-ttu-id="73f06-103">[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导将从 .configsettings 文件中读取您在部署脚本中使用的分区和角色部署选项 \<*project name*> 。</span><span class="sxs-lookup"><span data-stu-id="73f06-103">The [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Wizard reads the partition and role deployment options that you use in the deployment script from the \<*project name*>.configsettings file.</span></span> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<span data-ttu-id="73f06-104">在生成项目时创建此文件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="73f06-104">creates this file when you build the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project.</span></span> [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<span data-ttu-id="73f06-105">使用当前项目的配置设置创建 \<*project name*> .configsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="73f06-105">uses the configuration settings of the current project to create the \<*project name*>.configsettings file.</span></span>  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a><span data-ttu-id="73f06-106">检查部署的配置设置</span><span class="sxs-lookup"><span data-stu-id="73f06-106">Reviewing the Configuration Settings for Deployment</span></span>  
 <span data-ttu-id="73f06-107">以下是存储在 .configsettings 文件中的配置设置 \<*project name*> ：</span><span class="sxs-lookup"><span data-stu-id="73f06-107">The following are the configuration settings stored in the \<*project name*>.configsettings file:</span></span>  
  
-   <span data-ttu-id="73f06-108">**数据源连接字符串** 这些是基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中指定值的每个数据源的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="73f06-108">**Data Source Connection Strings** These are the connection strings for each data source based on the values specified in the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project.</span></span> <span data-ttu-id="73f06-109">总是先删除连接字符串中的用户 ID 和密码，然后再在此文件中存储字符串的其余部分。</span><span class="sxs-lookup"><span data-stu-id="73f06-109">The user id and password are always removed from the connection string before the remainder of the string is stored in this file.</span></span> <span data-ttu-id="73f06-110">但是，如果部署向导直接对 Analysis Services 实例进行部署，则可以在向导中添加相应的用户 ID 和密码信息，以便成功地处理部署数据库。</span><span class="sxs-lookup"><span data-stu-id="73f06-110">However, if the Deployment Wizard is deploying directly to an Analysis Services instance, you can add the appropriate user id and password information within the wizard to enable a successful processing of the deployment database.</span></span> <span data-ttu-id="73f06-111">如果部署向导保存了此连接信息，则部署脚本中不存储此信息。</span><span class="sxs-lookup"><span data-stu-id="73f06-111">This connection information will not be stored in the deployment script itself if one is saved by the Deployment Wizard.</span></span>  
  
-   <span data-ttu-id="73f06-112">**模拟帐户** 此设置指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在每个数据源中运行语句时所用的用户名。</span><span class="sxs-lookup"><span data-stu-id="73f06-112">**Impersonation Accounts** This setting specifies the user name that [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] uses to run statements in each data source.</span></span> <span data-ttu-id="73f06-113">如果未指定模拟帐户， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用其登录帐户来运行语句。</span><span class="sxs-lookup"><span data-stu-id="73f06-113">If no impersonation account is specified, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] uses its logon account to run statements.</span></span> <span data-ttu-id="73f06-114">如果直接在数据源中向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登录帐户授予权限，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中所有数据库的所有数据库管理员均可通过该登录帐户访问数据源。</span><span class="sxs-lookup"><span data-stu-id="73f06-114">If the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] logon account is granted permissions directly in the data source, all database administrators in all databases in the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance have access to the data source through the logon account.</span></span> <span data-ttu-id="73f06-115">如果指定用户帐户和密码，则总是先删除此信息，然后再在此文件中存储模拟信息。</span><span class="sxs-lookup"><span data-stu-id="73f06-115">If a user account and password is specified, this information is always removed before the impersonation information is stored in this file.</span></span> <span data-ttu-id="73f06-116">但是，如果部署向导直接对 Analysis Services 实例进行部署，则可以在向导中添加相应的用户 ID 和密码信息，以便成功地处理部署数据库。</span><span class="sxs-lookup"><span data-stu-id="73f06-116">However, if the Deployment Wizard is deploying directly to an Analysis Services instance, you can add the appropriate user id and password information within the wizard to enable a successful processing of the deployment database.</span></span> <span data-ttu-id="73f06-117">如果部署向导保存了此模拟信息，则部署脚本中不存储此信息。</span><span class="sxs-lookup"><span data-stu-id="73f06-117">This impersonation information will not be stored in the deployment script itself if one is saved by the Deployment Wizard.</span></span>  
  
-   <span data-ttu-id="73f06-118">**键错误日志文件** 此设置为数据库中的每个多维数据集、度量值组、分区和维度指定键错误日志文件的文件名和路径。</span><span class="sxs-lookup"><span data-stu-id="73f06-118">**Key Error Log Files** This setting specifies the file name and path of the key error log file for each cube, measure group, partition, and dimension in the database.</span></span>  
  
-   <span data-ttu-id="73f06-119">**存储位置** 此设置为数据库中的每个多维数据集、度量值组和分区指定存储位置。</span><span class="sxs-lookup"><span data-stu-id="73f06-119">**Storage Locations** This setting specifies the storage location for each cube, measure group, and partition in the database.</span></span> <span data-ttu-id="73f06-120">如果没有为对象提供任何值，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导使用该对象的默认位置。</span><span class="sxs-lookup"><span data-stu-id="73f06-120">If no value is provided for an object, the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Wizard uses the default location for the object.</span></span> <span data-ttu-id="73f06-121">例如，分区使用度量值组的位置，度量值组使用多维数据集的位置，而多维数据集使用对象在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的默认位置。</span><span class="sxs-lookup"><span data-stu-id="73f06-121">For example, partitions use the location for the measure group, measure groups use the location for the cube, and cubes use the default location for objects on the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instance.</span></span> <span data-ttu-id="73f06-122">存储位置可以是本地路径，也可以是通用命名约定 (UNC) 路径。</span><span class="sxs-lookup"><span data-stu-id="73f06-122">The storage location can be a local or a Universal Naming Convention (UNC) path.</span></span>  
  
-   <span data-ttu-id="73f06-123">**报表服务器** 此设置为数据库的每个多维数据集中定义的每个报表操作指定报表服务器和文件夹位置。</span><span class="sxs-lookup"><span data-stu-id="73f06-123">**Report Server** This setting specifies the report server and folder location for each report action defined in each cube in the database.</span></span>  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a><span data-ttu-id="73f06-124">修改部署的配置设置</span><span class="sxs-lookup"><span data-stu-id="73f06-124">Modifying the Configuration Settings for Deployment</span></span>  
 <span data-ttu-id="73f06-125">在某些情况下，可能需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用不同于 .configsettings 文件中存储的配置设置来部署项目 \<*project name*> 。</span><span class="sxs-lookup"><span data-stu-id="73f06-125">In some cases, you may need to deploy the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project using different configuration settings than those stored in the \<*project name*>.configsettings file.</span></span> <span data-ttu-id="73f06-126">例如，最好更改一个或多个数据源的连接字符串，或需要为特定的分区或度量值组指定存储位置。</span><span class="sxs-lookup"><span data-stu-id="73f06-126">For example, you may want to change the connection string to one or more data sources, or specify storage locations for specific partitions or measure groups.</span></span>  
  
 <span data-ttu-id="73f06-127">若要在项目中修改分区和角色的部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，必须在 .configsettings 文件中更改此信息 \<*project name*> ，如以下过程中所述。</span><span class="sxs-lookup"><span data-stu-id="73f06-127">To modify the deployment of partitions and roles in an [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] project, you must change this information within the \<*project name*>.configsettings file, as described in the procedure below.</span></span> <span data-ttu-id="73f06-128">不能在项目中更改分区和角色设置，因为中的 " *\<project name>* **属性页**" 对话框 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 不会显示这些选项。</span><span class="sxs-lookup"><span data-stu-id="73f06-128">You cannot change the partition and roles settings within the project because the *\<project name>* **Properties Pages** dialog box in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] does not display these options.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="73f06-129">配置设置可应用于所有对象，也可仅应用于新创建的对象。</span><span class="sxs-lookup"><span data-stu-id="73f06-129">Configuration settings can apply to all objects or only to newly created objects.</span></span> <span data-ttu-id="73f06-130">仅当要将其他对象部署到以前部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中，并且不希望覆盖现有对象时，才将配置设置应用于新创建的对象。</span><span class="sxs-lookup"><span data-stu-id="73f06-130">Apply configuration settings to newly created objects only when you are deploying additional objects to a previously deployed [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database and do not want to overwrite existing objects.</span></span> <span data-ttu-id="73f06-131">若要指定是将配置设置应用于所有对象，还是仅应用于新创建的设置，请在 d 文件中设置此选项 \<*project name*> 。</span><span class="sxs-lookup"><span data-stu-id="73f06-131">To specify whether configuration settings apply to all objects or only to newly created ones, set this option in the \<*project name*>.deploymentoptions file.</span></span> <span data-ttu-id="73f06-132">有关详细信息，请参阅 [指定分区和角色部署选项](deployment-script-files-partition-and-role-deployment-options.md)。</span><span class="sxs-lookup"><span data-stu-id="73f06-132">For more information, see [Specifying Partition and Role Deployment Options](deployment-script-files-partition-and-role-deployment-options.md).</span></span>  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a><span data-ttu-id="73f06-133">在生成输入文件后更改配置设置</span><span class="sxs-lookup"><span data-stu-id="73f06-133">To change configuration settings after the input files have been generated</span></span>  
  
-   <span data-ttu-id="73f06-134">以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，然后在 **“配置设置”** 页上，为要部署的对象指定配置设置。</span><span class="sxs-lookup"><span data-stu-id="73f06-134">Run the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Wizard interactively, and on the **Configuration Settings** page, specify the configuration setting for the objects being deployed.</span></span>  
  
     <span data-ttu-id="73f06-135">- 或 -</span><span class="sxs-lookup"><span data-stu-id="73f06-135">-or-</span></span>  
  
-   <span data-ttu-id="73f06-136">在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并设置向导，使其以应答文件模式运行。</span><span class="sxs-lookup"><span data-stu-id="73f06-136">Run the [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Deployment Wizard at the command prompt and set the wizard to run in answer file mode.</span></span> <span data-ttu-id="73f06-137">有关应答文件模式的详细信息，请参阅 [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md)。</span><span class="sxs-lookup"><span data-stu-id="73f06-137">For more information about answer file mode, see [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md).</span></span>  
  
     <span data-ttu-id="73f06-138">- 或 -</span><span class="sxs-lookup"><span data-stu-id="73f06-138">-or-</span></span>  
  
-   <span data-ttu-id="73f06-139">\<*project name*>使用任意文本编辑器修改 .configsettings 文件。</span><span class="sxs-lookup"><span data-stu-id="73f06-139">Modify the \<*project name*>.configsettings file by using any text editor.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="73f06-140">另请参阅</span><span class="sxs-lookup"><span data-stu-id="73f06-140">See Also</span></span>  
 <span data-ttu-id="73f06-141">[指定安装目标](deployment-script-files-specifying-the-installation-target.md) </span><span class="sxs-lookup"><span data-stu-id="73f06-141">[Specifying the Installation Target](deployment-script-files-specifying-the-installation-target.md) </span></span>  
 <span data-ttu-id="73f06-142">[指定分区和角色部署选项](deployment-script-files-partition-and-role-deployment-options.md) </span><span class="sxs-lookup"><span data-stu-id="73f06-142">[Specifying Partition and Role Deployment Options](deployment-script-files-partition-and-role-deployment-options.md) </span></span>  
 [<span data-ttu-id="73f06-143">指定处理选项</span><span class="sxs-lookup"><span data-stu-id="73f06-143">Specifying Processing Options</span></span>](deployment-script-files-specifying-processing-options.md)  
  
  