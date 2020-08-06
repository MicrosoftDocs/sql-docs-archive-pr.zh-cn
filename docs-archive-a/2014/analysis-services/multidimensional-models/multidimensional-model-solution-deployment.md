---
title: 多维模型解决方案部署 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, planning
- deploying [Analysis Services]
- deploying [Analysis Services], planning
ms.assetid: 7259c201-ff54-43e8-bda5-a6d51474e0e6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 638e211f261b0a8654dfbe2d8ab937aa3dee24d3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589305"
---
# <a name="multidimensional-model-solution-deployment"></a>多维模型解决方案部署
  在完成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的开发后，可以将数据库部署到 Analysis Services 服务器。 Analysis Services 提供六个可能的部署方法，可用于将该数据库移到测试服务器或生产服务器。 此处按优势大小顺序列出这些方法：AMO 自动化、XMLA、部署向导、部署实用工具、同步向导、备份和还原。  
  
 本主题包含下列部分：  
  
 [部署方法](#bkmk_meth)  
  
 [部署注意事项](#bkmk_considerations)  
  
 [相关任务](#bkmk_rel)  
  
##  <a name="deployment-methods"></a><a name="bkmk_meth"></a>部署方法  
  
|方法|说明|链接|  
|------------|-----------------|----------|  
|**分析管理对象 (AMO) 自动化**|AMO 提供用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的完整命令集的编程接口，包括可用于解决方案部署的命令。 AMO 自动化是最灵活的解决方案部署方法，但是也需要完成一些编程工作。  使用 AMO 的一个重要优势是：可以将 SQL Server 代理用于 AMO 应用程序，以便按预设的计划运行部署。|[使用分析管理对象 (AMO) 进行开发](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)|  
|**XMLA**|使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 生成现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库的元数据的 XMLA 脚本，然后在另一台服务器中运行该脚本以重新创建初始数据库。 通过定义部署过程，然后进行整理并将其保存在 XMLA 脚本中，可以很容易在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中形成 XMLA 脚本。 将 XMLA 脚本保存到文件中以后，即可很容易地按计划运行脚本，或将脚本嵌入直接连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的应用程序中。<br /><br /> 还可以使用 SQL Server 代理按预置的计划运行 XMLA 脚本，但使用 XMLA 脚本没有 AMO 所具备的灵活性。 AMO 通过驻留完整的管理命令提供了范围更广的功能。|[使用 XMLA 部署模型解决方案](deploy-model-solutions-using-xmla.md)|  
|**部署向导**|通过部署向导，使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目生成的 XMLA 输出文件，以将项目的元数据部署到目标服务器中。 使用部署向导，可以直接从 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 文件（该文件由项目生成按输出目录创建）进行部署。<br /><br /> 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的主要优势是部署向导使用方便。 就像您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中保存 XMLA 脚本以供以后使用一样，可以保存部署向导脚本。 部署向导可以交互运行，也可以通过部署实用工具在命令提示符下运行。|[使用部署向导部署模型解决方案](deploy-model-solutions-using-the-deployment-wizard.md)|  
|**部署实用工具**|可以使用部署实用工具在命令提示符下启动 Analysis Services 部署引擎。|[使用部署实用工具部署模型解决方案](deploy-model-solutions-with-the-deployment-utility.md)|  
|**同步数据库向导**|使用同步数据库向导同步任意两个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库之间的元数据和数据。<br /><br /> 同步向导可用于将数据和元数据从源服务器复制到目标服务器。 如果目标服务器没有要部署的数据库副本，则将新数据库复制到目标服务器。 如果目标服务器已经有相同数据库的副本，则更新目标服务器上的数据库以使用源数据库的元数据和数据。|[同步 Analysis Services 数据库](synchronize-analysis-services-databases.md)|  
|**备份和还原**|备份为传输 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库提供了最简单的方式。 从 **“备份”** 对话框，可以设置配置选项，然后可以从对话框本身运行备份。 也可以创建可保存并根据需要频繁运行的脚本。<br /><br /> 与其他部署方法相比，备份和还原的使用频率较低，但它能以很小的基础结构要求快速完成部署。|[备份和还原 Analysis Services 数据库](backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="deployment-considerations"></a><a name="bkmk_considerations"></a>部署注意事项  
 在部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目前，考虑将哪些问题应用于解决方案，然后查看相关链接来了解如何解决问题：  
  
|注意事项|详细信息链接|  
|-------------------|------------------------------|  
|此解决方案需要哪些硬件和软件资源？|[Analysis Services 部署的要求和注意事项](requirements-and-considerations-for-analysis-services-deployment.md)|  
|如何部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目范围之外的相关对象（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包、报表或关系数据库架构）？||  
|如何在已部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中加载和更新数据？<br /><br /> 如何在已部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中更新元数据（如计算）？|本主题中的[部署方法](#bkmk_meth) 。|  
|是否要向用户提供通过 Internet 访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据的权限？|[在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../instances/configure-http-access-to-analysis-services-on-iis-8-0.md)|  
|是否要提供对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据的连续查询访问权限？|[Analysis Services 部署的要求和注意事项](requirements-and-considerations-for-analysis-services-deployment.md)|  
|是否要使用链接的对象或远程分区在分布式环境中部署对象？|[创建和管理本地分区 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)、[创建和管理远程分区 (Analysis Services)](create-and-manage-a-remote-partition-analysis-services.md) 和[链接度量值组](linked-measure-groups.md)。|  
|如何确保 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据的安全？|[授予对对象和操作的访问权限 (Analysis Services)](authorizing-access-to-objects-and-operations-analysis-services.md)|  
  
##  <a name="related-tasks"></a><a name="bkmk_rel"></a> 相关任务  
 [Analysis Services 部署的要求和注意事项](requirements-and-considerations-for-analysis-services-deployment.md)  
  
 [使用 XMLA 部署模型解决方案](deploy-model-solutions-using-xmla.md)  
  
 [使用部署向导部署模型解决方案](deploy-model-solutions-using-the-deployment-wizard.md)  
  
 [使用部署实用工具部署模型解决方案](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
