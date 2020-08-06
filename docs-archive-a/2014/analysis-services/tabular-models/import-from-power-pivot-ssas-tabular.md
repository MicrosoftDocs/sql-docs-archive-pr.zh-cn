---
title: 从 PowerPivot (SSAS 表格) 导入 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
author: minewiskan
ms.author: owend
ms.openlocfilehash: 581259d79e5d84bd558ca3f13519fbf4dc0ba52f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687219"
---
# <a name="import-from-powerpivot-ssas-tabular"></a>从 PowerPivot 导入（SSAS 表格）
  本主题介绍如何通过使用中的 "从 PowerPivot 导入" 项目模板从 PowerPivot 工作簿导入元数据和数据，从而创建新的表格模型项目 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 。  
  
## <a name="create-a-new-tabular-model-from-a-powerpivot-for-excel-file"></a>从 PowerPivot for Excel 文件创建新的表格模型  
 在通过从 PowerPivot 工作簿中导入来创建新的表格模型项目时，将使用定义工作簿结构的元数据来创建和定义 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中的表格模型项目的结构。 表、列、度量值和关系之类的对象将与它们处于 PowerPivot 工作簿中一样保留并出现在表格模型项目中。 不对 .xlsx 工作簿文件进行任何更改。  
  
> [!NOTE]  
>  表格模型不支持链接表。 在从包含链接表的 PowerPivot 工作簿中导入时，链接表数据将作为复制\粘贴的数据处理并且存储于 Model.bim 文件中。 在查看复制\粘贴的表的属性时，“源数据”**** 属性将被禁用，并且“表”**** 菜单上的“表属性”**** 对话框将被禁用。  
>   
>  对于可添加到在模型中嵌入的数据中的行数，有最多 10,000 行的限制。 如果从 PowerPivot 导入模型并看到错误 "数据已被截断。 粘贴的表不能包含超过10000行 "您应该通过将嵌入的数据移到另一个数据源（如 SQL Server 中的表），然后重新导入来修改 PowerPivot 模型。  
  
 有一些特别注意事项，这取决于工作区数据库是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 所处的计算机（本地）上的 Analysis Services 实例中还是在远程 Analysis Services 实例中。  
  
 如果工作区数据库在本地 Analysis Services 实例中，则可以从 PowerPivot 工作簿导入元数据和数据。 从工作簿复制元数据并使用该元数据创建表格模型项目。 然后，从工作簿复制数据并将其存储到项目的工作区数据库中 (除了复制/粘贴数据，) 存储在 model.bim 文件中。  
  
 如果工作区数据库在远程 Analysis Services 实例中，则无法从 PowerPivot for Excel 工作簿导入数据。 您仍可以导入工作薄元数据；不过，这将导致脚本在远程 Analysis Services 实例中运行。 您应只从受信任的 PowerPivot 工作薄导入元数据。 必须从数据源连接所定义的源中导入数据。 必须将 PowerPivot 工作簿中的复制/粘贴的数据和链接表数据复制并粘贴到表格模型项目中。  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-powerpivot-for-excel-file"></a>从 PowerPivot for Excel 文件创建新的表格模型项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在 "**新建项目**" 对话框中的 "**已安装的模板**" 下，单击 "**商业智能**"，然后单击 "**从 PowerPivot 导入**"。  
  
3.  在 "**名称**" 中，键入项目的名称，然后指定位置和解决方案名称，然后单击 **"确定"**。  
  
4.  在 **“打开”** 对话框中，选择包含您要导入的模型元数据和数据的 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 文件，然后单击 **“打开”**。  
  
## <a name="see-also"></a>另请参阅  
 [工作区数据库 &#40;SSAS 表格&#41;](workspace-database-ssas-tabular.md)   
 [复制并粘贴数据（SSAS 表格）](../copy-and-paste-data-ssas-tabular.md)  
  
  
