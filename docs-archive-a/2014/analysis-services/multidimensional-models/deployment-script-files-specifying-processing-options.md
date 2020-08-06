---
title: 指定处理选项 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9690aaa7e1d3b3870eb6ab01630b98027263655f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687284"
---
# <a name="specifying-processing-options"></a>指定处理选项
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导从 d 文件中读取处理选项 \<*project name*> 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在生成项目时创建此文件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用在 "属性页" 对话框的 "**部署**" 页上指定的处理选项 *\<project name>* **Properties Pages**来创建 \<*project name*> d 文件。  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>检查部署的处理选项  
 D 文件中存储的配置设置如下所示 \<*project name*> ：  
  
-   **处理方法** 此设置将控制在部署后是否处理部署的对象以及将执行的处理的类型。 有以下三个处理选项：  
  
    -   默认处理（默认值）  
  
    -   完全处理  
  
    -   无  
  
-   **写回表选项** 如果在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中启用了写回，则此设置可定义处理写回的方式。 有以下三个写回表选项：  
  
    -   默认情况下，如果存在写回表，则使用该表。 如果写回表不存在，则将创建一个新的写回表。  
  
    -   如果写回表已经存在，则部署失败。 如果写回表不存在，则将创建一个新的写回表。  
  
    -   不管写回表是否已存在，都将创建新的写回表。 在这种情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导将删除任何现有的表，并用新的写回表来替换现有的表。  
  
-   **事务性部署** 此设置控制元数据更改和进程命令的部署是在单个事务中进行还是在多个单独的事务中进行。  
  
    -   如果此选项为 `True`（默认值），则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在单个事务中部署所有元数据更改和所有进程命令。  
  
    -   如果此选项为 `False`，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在单个事务中部署元数据更改，并在其自己的事务中部署每个处理命令。  
  
## <a name="modifying-the-processing-options-for-deployment"></a>修改部署的处理选项  
 但是，你可能需要 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用与 d 文件中存储的选项不同的处理选项来部署项目 \<*project name*> 。 例如，您也可能要完全处理所有对象，使用默认处理选项进行处理，也可不进行任何处理。 如果多维数据集或维度启用了写操作，则可以指定是使用新的写回表还是现有的写回表。  
  
 若要修改部署过程中使用的处理选项，可以编辑和重新生成项目，也可以通过使用下列步骤中介绍的方法之一来更改输入文件中的处理选项。  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>在生成输入文件后更改处理选项  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导。 在 **“处理选项”** 页上，为要部署的项目指定处理选项。  
  
     - 或 -  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并设置向导，使其以应答文件模式运行。 有关应答文件模式的详细信息，请参阅 [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md)。  
  
     - 或 -  
  
-   \<*project name*>使用任意文本编辑器修改 d 文件。  
  
## <a name="see-also"></a>另请参阅  
 [指定安装目标](deployment-script-files-specifying-the-installation-target.md)   
 [指定分区和角色部署选项](deployment-script-files-partition-and-role-deployment-options.md)   
 [为解决方案部署指定配置设置](deployment-script-files-solution-deployment-config-settings.md)  
  
  
