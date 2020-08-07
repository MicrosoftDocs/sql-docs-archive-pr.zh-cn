---
title: 部署 Analysis Services 项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5d98bab3-3577-4143-b737-5196444a36ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: 031c25b8a7e777cacb3be215b733119ff783db3f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577016"
---
# <a name="deploying-an-analysis-services-project"></a>部署 Analysis Services 项目
  若要查看位于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集中的对象的多维数据集和维度数据，必须将该项目部署到指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中，然后再处理该多维数据集及其维度。 ** 部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目将在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中创建定义的对象。 处理**[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中的对象会将基础数据源中的数据复制到多维数据集对象中。 有关详细信息，请参阅 [部署 Analysis Services 项目 (SSDT)](multidimensional-models/deploy-analysis-services-projects-ssdt.md) 和 [配置 Analysis Services 项目属性 (SSDT)](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
 在开发过程中的这个阶段通常将此多维数据集部署到开发服务器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中。 完成业务智能项目的开发时，通常会使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 开发向导将项目从开发服务器部署到生产服务器。 有关详细信息，请参阅 [多维模型解决方案部署](multidimensional-models/multidimensional-model-solution-deployment.md) 和 [使用部署向导部署模型解决方案](multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)。  
  
 在以下任务中，您将查看 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目的部署属性，然后将该项目部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的本地实例中。  
  
### <a name="to-deploy-the-analysis-services-project"></a>部署 Analysis Services 项目  
  
1.  在解决方案资源管理器中，右键单击“Analysis Services 教程”**** 项目，然后单击“属性”****。  
  
     将出现“Analysis Services 教程属性页”**** 对话框，并显示活动（开发）配置的属性。 可以定义多个配置，每个配置可以具有不同的属性。 例如，开发人员可能需要将同一项目配置为部署到不同的开发计算机，并具有不同的部署属性，如数据库名称或处理属性。 注意“输出路径”**** 属性的值。 该属性指定生成项目时保存项目的 XMLA 部署脚本的位置。 这些脚本用于将该项目中的对象部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例。  
  
2.  在左窗格的“配置属性”**** 节点中，单击“部署”****。  
  
     查看项目的部署属性。 默认情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目模板将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目配置为将所有项目增量部署到本地计算机上的默认 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例，以创建一个与此项目同名的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库，并在部署后使用默认处理选项处理这些对象。 有关详细信息，请参阅 [配置 Analysis Services 项目属性 (SSDT)](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
    > [!NOTE]  
    >  如果要将项目部署到本地计算机上的命名实例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或远程服务器上的实例，请将**服务器**属性更改为相应的实例名称，例如 \<*ServerName**> \\ < **InstanceName**> *。  
  
3.  单击“确定”。  
  
4.  在解决方案资源管理器中，右键单击“Analysis Services 教程”**** 项目，然后单击“部署”****。 您可能需要等待。  
  
    > [!NOTE]  
    >  如果您在部署过程中出现错误，则使用 SQL Server Management Studio 检查数据库权限。 您为数据源连接指定的帐户必须在 SQL Server 实例上具有登录名。 双击该登录名可以查看“用户映射”属性。 该帐户必须对 **AdventureWorksDW2012** 数据库具有 db_datareader 权限。  
  
     [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 将生成 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程项目，然后使用部署脚本将其部署到指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中。 部署进度显示在两个窗口中： "**输出**" 窗口和 "**部署进度-Analysis Services 教程**" 窗口。  
  
     打开“输出”窗口，如果需要，可通过单击“视图”**** 菜单上的“输出”**** 实现。 “输出”**** 窗口显示部署的整体进度。 "**部署进度-Analysis Services 教程**" 窗口显示部署过程中执行的每个步骤的详细信息。 有关详细信息，请参阅[生成 Analysis Services 项目 (SSDT)](multidimensional-models/build-analysis-services-projects-ssdt.md)和[部署 Analysis Services 项目 (SSDT)](multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
5.  查看 "**输出**" 窗口和 "**部署进度-Analysis Services 教程**" 窗口的内容，验证是否已生成、部署和处理了多维数据集，并且没有出现错误。  
  
6.  若要隐藏“部署进度 - Analysis Services 教程”**** 窗口，请单击窗口的工具栏上的“自动隐藏”**** 图标（看起来像图钉）。  
  
7.  若要隐藏“输出”**** 窗口，请单击窗口的工具栏上的“自动隐藏”**** 图标。  
  
 您已经将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 多维数据集成功部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的本地实例，并已对部署的多维数据集进行了处理。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [浏览多维数据集](lesson-2-6-browsing-the-cube.md)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSDT 部署 Analysis Services 项目&#41;](multidimensional-models/deploy-analysis-services-projects-ssdt.md)   
 [配置 Analysis Services 项目属性 (SSDT)](multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
