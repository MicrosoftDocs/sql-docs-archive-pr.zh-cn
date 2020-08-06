---
title: " (中级数据挖掘教程) 创建解决方案和数据源 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 48009fae653c4c1a231380e8d286363168ae28d6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579444"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>创建解决方案和数据源（数据挖掘中级教程）
  若要使用数据挖掘，必须首先在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用 **“Analysis Services 多维和数据挖掘项目”** 模板创建一个项目。 打开该模板时，它将在设计器中加载您进行数据挖掘时可能需要的所有架构：数据源、挖掘结构和挖掘模型，甚至多维数据集（如果您的挖掘结构使用多维数据）。  
  
 创建项目时，在部署解决方案之前，解决方案将存储为本地文件。 部署解决方案时， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会查找在项目属性中指定的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器，并使用与项目相同的名称创建新的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。 默认情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用新项目的“localhost” **** 实例。 如果您使用的是命名实例，或者您如果为默认实例指定了其他名称，则必须将项目的部署数据库属性更改为要创建数据挖掘对象的位置。  
  
 有关项目的详细信息 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，请参阅[创建 Analysis Services 项目 &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt)。  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>为本教程创建新的 Analysis Services 项目  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。  
  
3.  从 **“已安装的模板”** 窗格中选择 **“Analysis Services 多维和数据挖掘项目”** 。  
  
4.  在“名称” **** 框中，将新项目命名为 **DM Intermediate**。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>更改存储数据挖掘对象的实例（可选）  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“项目”** 菜单中的 **“属性”**。  
  
2.  在“属性页” **** 窗格的左侧，单击“部署” ****。  
  
3.  验证 **“服务器”** 名称是否为 **localhost**。 如果使用的是其他实例，请键入该实例的名称。 如果使用的是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的命名实例，请键入计算机名称和实例名称。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>更改项目的部署属性（可选）  
  
1.  在解决方案资源管理器中，右键单击该项目，然后选择 **“属性”**。  
  
     - 或 -  
  
     在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，选择 **“项目”** 菜单中的 **“属性”**。  
  
2.  在“属性页” **** 窗格的左侧，单击“部署” ****。  
  
     在 **“选项”** 窗格中选择 **“部署模式”**，将选项设置为 **“全部部署”** 以覆盖对象，或者设置为 **“仅部署更改”** 以更新对象或添加对象。  
  
## <a name="creating-a-data-source"></a>创建数据源  
 在数据挖掘基础教程中，您创建了一个用于存储 *数据库连接信息的“数据源”*[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 。 在本解决方案中按照相同的步骤创建 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 数据源。  
  
#### <a name="to-create-a-data-source"></a>创建数据源  
  
-   [创建数据源 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 一个数据源可以支持多个数据源视图，每个数据源视图可以有多个表。 但是，由于数据源和数据源视图 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 与您创建的数据挖掘模型一起部署到您的数据库中，因此，最好只在每个数据源视图中包括每个数据挖掘模型或模型组所需的表。  
  
 在下一课中，您将添加数据源视图以便支持每个新方案。 只有市场篮以及顺序分析和聚类分析课程使用相同的数据源视图；别的每个方案使用不同的数据源视图，因此各课程彼此是独立的，可以单独完成。  
  
|方案|包括在数据源视图中的数据|  
|--------------|-------------------------------------------|  
|[第2课： &#40;中级数据挖掘教程构建预测方案&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|不同区域的自行车型号的每月销售报表，收集为单一视图形式。|  
|[第 3 课：生成市场篮方案（数据挖掘中级教程）](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|一个包含客户订单列表的表，和一个显示每个客户的单独购买情况的嵌套表。|  
|[第4课：生成顺序分析和聚类分析方案 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|用于市场篮分析的相同数据，添加了显示产品购买订单的标识符。|  
|[第 5 课：生成神经网络模型和逻辑回归模型（数据挖掘中级教程）](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|包含来自呼叫中心的一些初步性能跟踪数据的单一表。|  
  
## <a name="next-lesson"></a>下一课  
 [第2课： &#40;中级数据挖掘教程构建预测方案&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘项目](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [多维模型中的数据源视图](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
