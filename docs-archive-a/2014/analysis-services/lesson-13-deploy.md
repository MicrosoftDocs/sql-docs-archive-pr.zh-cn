---
title: 第14课：部署 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
ms.openlocfilehash: c1a55960a0c33a386d978f3c15e489ed7bd861ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577028"
---
# <a name="lesson-14-deploy"></a>第 14 课：部署
  在本课中，您将配置部署属性；同时指定在表格模式下运行的 Analysis Services 的部署服务器实例以及为您要部署的模型指定名称。 然后，将模型部署到该实例。 部署此模型之后，用户可以使用报表客户端应用程序连接到该模型。 若要了解详细信息，请参阅[表格模型解决方案部署（SSAS 表格）](tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
 学完本课的估计时间： **5 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，应该已完成上一课： [第 13 课：在 Excel 中分析](lesson-12-analyze-in-excel.md)。  
  
## <a name="deploy-the-model"></a>部署模型  
  
#### <a name="to-configure-deployment-properties"></a>配置部署属性  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“解决方案资源管理器”**** 中，右键单击“Adventure Works Internet Sales Tabular Model”**** 项目，然后在上下文菜单中单击“属性”****。  
  
2.  在“AW Internet Sales Tabular Model 属性页”**** 对话框中，在“部署服务器”**** 下的“服务器”**** 属性中，键入在表格模式下运行的 Analysis Services 实例的名称。 这将是您的模型将被部署到的实例。  
  
    > [!IMPORTANT]  
    >  您必须对远程 Analysis Services 实例具有管理员权限，才能将模型部署到该实例。  
  
3.  验证 "**查询模式**" 属性是否设置为 **"内存中**"。  
  
    > [!NOTE]  
    >  在 DirectQuery 模式下，不支持使用本教程创建的模型。  
  
4.  在 "**数据库**" 属性中，键入 `Adventure Works Internet Sales Model` 。  
  
5.  在 "**多维数据集**名称" 属性中，键入 `Adventure Works Internet Sales Model` 。  
  
6.  验证你的选择，并单击“确定”。****  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>部署 Adventure Works Internet Sales 表格模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“生成”**** 菜单，然后单击“部署 AW Internet Sales Tabular Model”****。  
  
     “部署”对话框将出现，并且显示模型中包括的元数据和每个表的部署状态。  
  
## <a name="conclusion"></a>结论  
 恭喜！ 您已完成了创作和部署第一个 Analysis Services 表格模型的过程。 本教程已帮助指导您完成了创建表格模型的最常见任务。 既然已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 来管理此模型、创建进程脚本和备份计划。 用户可以使用报表客户端应用程序（如 Microsoft Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]）连接到此模型。  
  
## <a name="additional-resources"></a>其他资源  
 若要了解有关支持 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的表格模型属性的详细信息，请参阅 [Power View 报表属性（SSAS 表格）](tabular-models/properties-ssas-tabular.md)。  
  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式 &#40;SSAS 表格&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;配置默认数据建模和部署属性](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [表格模型数据库（SSAS 表格）](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
