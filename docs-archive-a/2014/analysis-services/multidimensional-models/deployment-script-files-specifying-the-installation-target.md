---
title: 指定安装目标 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- installation targets [Analysis Services]
- Analysis Services deployments, installation targets
- Analysis Services Deployment Wizard, installation targets
- deploying [Analysis Services], installation targets
- modifying installation targets
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
author: minewiskan
ms.author: owend
ms.openlocfilehash: e830fc353898e3ec835b338e84765a0cad0de43f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587636"
---
# <a name="specifying-the-installation-target"></a>指定安装目标
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导从 .deploymenttargets 文件中读取安装目标信息 \<*project name*> 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在生成项目时创建此文件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]使用在 "属性页" 对话框的 "**部署**" 页上指定的数据库和服务器 *\<project name>* **Properties Pages**来创建 \<*project name*> .targets 文件。  
  
## <a name="modifying-the-installation-target-for-deployment"></a>修改部署的安装目标  
 在有些情况下，可能需要将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] “部署” **页上指定的项不同的数据库或** 实例。 例如，可能要在部署之前将项目部署到用于测试的服务器，再在测试完成后将其部署到生产服务器。 此外，还可能需要将已完成且经过测试的项目部署到网络负载平衡群集中的多台生产服务器，或将其部署到临时服务器和生产服务器。  
  
 若要将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目部署到其他数据库或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，可使用下列过程中介绍的方法之一，在输入文件中更改安装目标。  
  
#### <a name="to-change-the-installation-target-after-the-input-files-have-been-generated"></a>在生成了输入文件后更改安装目标  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导。 在 **“安装目标”** 页上，为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例和数据库指定新的目标。  
  
     \- 或 -  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并设置向导，使其以应答文件模式运行。 有关应答文件模式的详细信息，请参阅 [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md)。  
  
     \- 或 -  
  
-   \<*project name*>使用任意文本编辑器修改 .deploymenttargets 文件。  
  
## <a name="see-also"></a>另请参阅  
 [指定分区和角色部署选项](deployment-script-files-partition-and-role-deployment-options.md)   
 [为解决方案部署指定配置设置](deployment-script-files-solution-deployment-config-settings.md)   
 [指定处理选项](deployment-script-files-specifying-processing-options.md)  
  
  
