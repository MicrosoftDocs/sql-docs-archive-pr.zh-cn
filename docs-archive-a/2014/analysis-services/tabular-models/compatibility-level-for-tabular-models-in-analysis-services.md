---
title: " (SSAS 表格 SP1) 的兼容级别 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2853cd5509b66dbfaadd78c578b9676399e81977
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693504"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>兼容级别（SSAS 表格 SP1）
  您可以在创建新的表格模型项目时、升级现有表格模型项目时、升级现有的已部署表格模型数据库时或者在导入 PowerPivot 工作簿时指定*兼容性级别*。  
  
## <a name="compatibility-level"></a>兼容级别  
 通常，应该先在开发和测试计算机上安装新版本和 Service Pack，然后再在生产计算机上安装。 在此类情况下，了解如何为新的表格模型项目以及已部署到生产环境中的表格模型项目设置兼容级别十分重要。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services 实例支持以下兼容级别（数据库版本）：  
  
-   SQL Server 2012 (1100)   
  
-   SQL Server 2012 SP1 (1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>在创建新的表格模型项目时设置兼容级别  
 在 SQL Server Data Tools (SSDT) 中创建新的表格模型项目时，可以在 "**新建表格项目选项**" 对话框中指定兼容级别。 您可以在创建要部署到 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本的 Analysis Services 实例还是 SQL Server 2012 Analysis Services 实例（不含 Service Pack 1）的新项目之间进行选择。  
  
 您还可以通过选择 **“不再显示此消息”** 选项指定默认的兼容级别。 所有后续项目都将使用您指定的兼容级别。 您可以通过 SSDT 在“选项”中更改默认兼容级别。  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>将现有的表格模型项目升级到 1103 兼容级别  
 您可以 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 使用 "模型**属性**" 窗口中的 "**兼容级别**" 属性升级在 SSDT 中创建的表格模型项目，然后再将或更高版本安装为与数据库版本1103兼容。 为了升级表格模型项目，安装 SSDT 的计算机必须安装了 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本，并且工作区数据库所在的 Analysis Services 实例必须也安装了[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本。 不能降级到更早的版本。  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>将已部署的表格模型数据库升级到 1103 兼容级别  
 您可以使用 "**数据库属性**" 中的 "**兼容级别**" 属性，将现有的已部署表格模型数据库升级到 SQL Server Management Studio (SSMS) 中兼容的数据库版本1103。 为了进行升级，安装 SQL Server Analysis Services 实例的计算机必须安装 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 或更高版本。 不能将已部署的表格模型数据库降级到更早的版本。  
  
### <a name="import-from-powerpivot"></a>从 PowerPivot 导入  
 在通过从 PowerPivot 导入来创建新的表格模型项目时，您可以指定是要将兼容级别升级到默认兼容级别（如果以前已在 SSDT 中配置），还是将该兼容级别保留为已在 PowerPivot 工作簿中指定的兼容级别。  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>检查 SSMS 中表格模型数据库的兼容级别  
 您可以通过查看 "**兼容级别**" 属性，在 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] **数据库属性**) 中的 " (新建" 来检查 SSMS 中表格模型数据库的兼容级别。  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>检查 SSMS 中 Analysis Services 实例支持的兼容级别  
 你可以通过查看 "**信息**" 页上的 "**支持的兼容级别**" 属性来检查 SSMS 中支持的兼容性级别， ([!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] Analysis Services "**属性**") 中的 "新建"。 支持的兼容级别 1103 指示安装了 SQL Server SP1 或更高版本。 不能更改支持的兼容级别。  
  
  
