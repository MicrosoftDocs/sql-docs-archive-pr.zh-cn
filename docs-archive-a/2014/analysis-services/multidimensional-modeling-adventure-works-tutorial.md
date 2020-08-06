---
title: " (艾德 Works 教程) 的多维建模Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tutorials [Analysis Services]
- Analysis Services, tutorials
ms.assetid: db55e226-601a-4026-8651-573195555a59
author: minewiskan
ms.author: owend
ms.openlocfilehash: cd2e8f856d36cab045e6cbc4d34f7cfeffac3c3c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588731"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>多维建模（Adventure Works 教程）
  欢迎使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教程。 本教程通过在所有示例中使用虚构公司 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ，说明如何使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 开发和部署 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 项目。  
  
## <a name="what-you-will-learn"></a>学习内容  
 在本教程中，您将了解以下内容：  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]项目中定义数据源、数据源视图、维度、属性、属性关系、层次结构和多维数据集。  
  
-   如何通过将 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例来查看多维数据集和维度数据，以及如何在随后处理已部署的对象以使用基础数据源中的数据来填充对象。  
  
-   如何在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目中修改度量值、维度、层次结构、属性和度量值组，以及如何将增量更改部署到开发服务器上的已部署多维数据集。  
  
-   如何定义多维数据集内的计算、关键绩效指标 (KPI)、操作、透视、翻译和安全角色。  
  
 在此教程中随附应用场景说明，以便您可以更好地理解这些课程的上下文。 有关详细信息，请参阅 [Analysis Services Tutorial Scenario](analysis-services-tutorial-scenario.md)。  
  
## <a name="prerequisites"></a>先决条件  
 要完成本教程的所有课程，您将需要示例数据、示例项目文件以及软件。 有关如何查找和安装本教程的必备组件的说明，请参阅 [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](install-sample-data-and-projects.md)。  
  
 此外，必须具有下列权限才能成功完成本教程：  
  
-   您必须是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 计算机上本地管理员组的成员或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例中的服务器管理角色的成员。  
  
-   您在 **AdventureWorksDW2012** 示例数据库中必须具有读取权限。 此示例数据库对于 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本有效。  
  
## <a name="lessons"></a>课程  
 本教程包括以下几课。  
  
|课程|估计完成时间|  
|------------|--------------------------------|  
|[第 1 课：在 Analysis Services 项目中定义数据源视图](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 分钟|  
|[第 2 课：定义和部署多维数据集](lesson-2-defining-and-deploying-a-cube.md)|30 分钟|  
|[第 3 课：修改度量值、属性和层次结构](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 分钟|  
|[第 4 课：定义高级属性和维度属性](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 分钟|  
|[第 5 课：定义维度和度量值组之间的关系](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 分钟|  
|[第 6 课：定义计算](lesson-6-defining-calculations.md)|45 分钟|  
|[第 7 课：定义关键绩效指标 (KPI)](lesson-7-defining-key-performance-indicators-kpis.md)|30 分钟|  
|[第 8 课：定义操作](lesson-8-defining-actions.md)|30 分钟|  
|[第 9 课：定义透视和翻译](lesson-9-defining-perspectives-and-translations.md)|30 分钟|  
|[第 10 课：定义管理角色](lesson-10-defining-administrative-roles.md)|15 分钟|  
  
> [!NOTE]  
>  您将在本教程中创建的多维数据集数据库是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维模型项目的简化版本，此项目是可在 codeplex 站点上下载的 Adventure Works 示例数据库的一部分。 简化了艾德公司数据库的教程版本，使你能够更好地专注于要立即改进的特定技能。 在完成该教程后，请考虑自己探索该多维模型项目，以便进一步理解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维建模。  
  
## <a name="next-step"></a>下一步  
 要开始学习本教程，请转到第一课： [Lesson 1: Defining a Data Source View within an Analysis Services Project](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)。  
  
  
