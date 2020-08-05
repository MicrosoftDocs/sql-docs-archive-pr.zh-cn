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
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>配置默认数据建模和部署属性（SSAS 表格）
  本主题介绍如何配置可为在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创建的每个新表格模型项目预定义的默认兼容级别、部署和工作区数据库属性设置。 在创建新项目之后，根据您的特定需求，仍可以更改这些属性。  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>为新模型项目配置默认的兼容级别属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。  
  
2.  在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“兼容级别”**。  
  
3.  配置以下属性设置：  
  
    |属性|默认设置|说明|  
    |--------------|---------------------|-----------------|  
    |**新项目的默认兼容级别**|SQL Server 2012 (1100) |此设置指定在创建新的表格模型项目时要使用的默认兼容级别。 如果要部署到未应用 SP1 的 Analysis Services 实例，则可以选择 SQL Server 2012 RTM (1100)；如果您的部署实例已应用 SP1，则可以选择 SQL Server 2012 SP1 或 SQL Server 2014。 有关详细信息，请参阅[&#40;SSAS 表格 SP1&#41;兼容级别](compatibility-level-for-tabular-models-in-analysis-services.md)。|  
    |**兼容级别选项**|全选中|为新的表格模型项目和在部署到其他 Analysis Services 实例时指定兼容级别选项。|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>为新模型项目配置默认的部署服务器属性设置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。  
  
2.  在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“部署”**。  
  
3.  配置以下属性设置：  
  
    |属性|默认设置|说明|  
    |--------------|---------------------|-----------------|  
    |**默认部署服务器**|localhost|此设置指定在部署模型时要使用的默认服务器。 您可以单击向下箭头以浏览您可以使用的本地网络 Analysis Services 服务器，也可以键入远程服务器的名称。|  
  
    > [!NOTE]  
    >  更改默认的部署服务器属性设置将不会影响在更改之前创建的现有项目。  
  
###  <a name="to-configure-the-default-workspace-database-property-settings-for-new-model-projects"></a><a name="bkmk_conf_default"></a>为新模型项目配置默认的工作区数据库属性设置  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“工具”** 菜单，然后单击 **“选项”**。  
  
2.  在 **“选项”** 对话框中，展开 **“Analysis Services 表格设计器”**，然后单击 **“工作区数据库”**。  
  
3.  配置以下属性设置：  
  
    |属性|默认设置|说明|  
    |--------------|---------------------|-----------------|  
    |**默认工作区服务器**|**localhost**|此属性指定在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中创作模型时将用于承载工作区数据库的默认服务器。 在本地计算机上运行的 Analysis Services 的所有可用实例都将包括在列表框中。<br /><br /> 注意：建议你始终将本地 Analysis Services 服务器指定为工作区服务器。 对于远程服务器上的工作区数据库，不支持从 PowerPivot 导入数据，数据不能在本地备份，并且在查询过程中用户界面可能会遇到滞后的情况。|  
    |**在关闭模型后工作区数据库保留**|**在磁盘上保留工作区数据库，但从内存中卸载**|指定在关闭某一模型后将如何保留工作区数据库。 工作区数据库将包括模型元数据、导入到模型中的数据以及模拟凭据（已加密）。 在某些情况下，工作区数据库可能会非常大并且占用大量内存。 默认情况下，工作区数据库将从内存中删除。 在更改此设置时，一定要考虑您的可用内存资源以及计划处理该模型的频繁程度。 此属性设置具有以下选项：<br /><br /> **在内存中保留工作区** - 指定在关闭模型后将工作区保留在内存中。 此选项将会占用较多内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用较少的资源并且工作区将更快加载。<br /><br /> **在磁盘上保留工作区数据库，但从内存中卸载** - 指定将工作区数据库保留在磁盘上，但在关闭模型后将不再保留在内存中。 此选项将会占用较少内存；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区保留在内存中相比，模型的加载速度将更慢。 在内存中资源受到限制或在处理远程工作区数据库时，将使用此选项。<br /><br /> **删除工作区** - 指定从内存中删除工作区数据库，在关闭模型后不将工作区数据库保留在磁盘上。 此选项将会占用较少内存和存储空间；但在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中打开某一模型时，将会占用附加的资源，并且与工作区数据库保留在内存中或磁盘上相比，模型的加载速度将更慢。 只有在偶尔处理模型时，才使用此选项。|  
    |**数据备份**|**在磁盘上保留数据的备份**|指定模型数据的备份是否将保留在备份文件中。 此属性设置具有以下选项：<br /><br /> **在磁盘上保留数据的备份** - 指定将模型数据的备份保留在磁盘上。 在保存模型时，数据也将保存到备份 (ABF) 文件中。 选择此选项可能导致保存和加载模型的速度变慢<br /><br /> **不在磁盘上保留数据的备份** - 指定不将模型数据的备份保留在磁盘上。 此选项将保存时间和模型加载时间降至最低。|  
  
> [!NOTE]  
>  更改默认的模型属性将不会影响更改之前创建的现有模型。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的项目属性](properties-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;的模型属性](model-properties-ssas-tabular.md)   
 [SSAS 表格 SP1&#41;兼容级别 &#40;](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
