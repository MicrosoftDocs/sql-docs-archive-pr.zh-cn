---
title: " (SSAS 表格) 导入数据 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6617b2a2-9f69-433e-89e0-4c5dc92982cf
author: minewiskan
ms.author: owend
ms.openlocfilehash: ef6097d7c85af36f01fe2442b1032751301891a1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590975"
---
# <a name="import-data-ssas-tabular"></a>导入数据（SSAS 表格）
  可以从各种源将数据导入表格模型中。 本节中的主题说明如何使用数据导入向导连接并选择要导入模型项目的数据。  
  
> [!IMPORTANT]  
>  如果模型中的任一表包含大量行，请考虑在模型创作期间仅导入一部分数据。 通过导入一部分数据，可减少处理时间和消耗的工作区数据库服务器资源。  
  
 使用表导入向导，可以从以下数据源导入数据：  
  
|**数据源**|**说明**|  
|---------------------|---------------------|  
|**关系数据库**|关系数据源包括：<br /><br /> Microsoft SQL Server<br /><br /> Microsoft SQL Azure<br /><br /> Microsoft SQL Server Parallel Data Warehouse<br /><br /> Microsoft Access<br /><br /> Oracle<br /><br /> Teradata<br /><br /> Sybase<br /><br /> Informix<br /><br /> IBM DB2<br /><br /> OLEDB/ODBC|  
|**多维源**|Microsoft SQL Server Analysis Services 多维数据集|  
|**数据馈送**|数据馈送包括：<br /><br /> Microsoft Reporting Services 报表<br /><br /> Azure DataMarket 数据集<br /><br /> 来自公共或公司提供程序的 Atom 馈送|  
|**文本文件**|文本文件包括：<br /><br /> Excel 文件 (.xlsx)<br /><br /> 文本文件 (.txt)|  
  
 除了使用表导入向导导入数据外，还可以将从剪贴板复制的数据粘贴到表中。 粘贴的数据的行为不同于已从其他数据源导入的数据的行为。 表中粘贴的数据没有“连接名称”或“源数据”属性。 粘贴的数据在 Model.bim 文件中保持不变。 保存项目或 Model.bim 文件时，也保存粘贴的数据。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|主题|说明|  
|-----------|-----------------|  
|[从关系数据源导入 &#40;SSAS 表格&#41;](import-from-a-relational-data-source-ssas-tabular.md)|说明如何从关系数据源（如 Microsoft SQL Server、Oracle 或 Teradata 数据库）导入数据。|  
|[从多维数据源导入 &#40;SSAS 表格&#41;](import-from-a-multidimensional-data-source-ssas-tabular.md)|说明如何从多维 SQL Server Analysis Services 多维数据集导入数据。|  
|[从数据馈送导入 &#40;SSAS 表格&#41;](import-from-a-data-feed-ssas-tabular.md)|说明如何从数据馈送（如 Microsoft Reporting Services 报表或 Azure DataMarket 数据集）导入数据。|  
|[从文本文件导入 &#40;SSAS 表格&#41;](import-from-a-text-file-ssas-tabular.md)|说明如何从 Microsoft Excel 工作簿或文本文件中导入数据。|  
|[复制并粘贴数据（SSAS 表格）](copy-and-paste-data-ssas-tabular.md)|说明如何使用“粘贴”和“追加粘贴”将数据添加到模型设计器中的现有表。|  
  
  
