---
title: SQL Server Office 数据挖掘外接程序 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c9021a19-2c19-4f0a-a293-5f7e0ac2524c
author: minewiskan
ms.author: owend
ms.openlocfilehash: b64d0c8728e4752d0d5831562d43646e29f7d723
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577075"
---
# <a name="sql-server-data-mining-add-ins-for-office"></a>SQL Server Office 数据挖掘外接程序
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Office 数据挖掘外接程序是用于预测分析的一组轻型工具，允许您使用 Excel 中的数据生成分析模型来用于预测、建议或浏览。  
  
 该外接程序中的向导和数据管理工具为以下这些常用的数据挖掘任务提供了分步说明：  
  
-   **建模前组织和清理你的数据。** 使用在 Excel 或任何 Excel 数据源中存储的数据。 可创建并保存连接以重用数据源、重复进行试验或将模型重新定型。  
  
-   **探查、抽样和准备。** 许多经验丰富的数据挖掘人员都说，一个数据挖掘项目中有百分之 70-90 的时间用在数据准备上。 该外接程序通过在 Excel 中提供可视化效果和帮助您完成以下这些常用任务的向导，可使此任务更快完成：  
  
    -   探查数据并了解其分布和特征。  
  
    -   通过随机抽样或过度抽样创建定型集和测试集。  
  
    -   找到离散值并删除或替换它们。  
  
    -   重新标记数据以提高分析质量。  
  
-   **通过监督的学习或无人监督的学习分析模式。** 单击用户友好的向导以便执行某些最常见数据挖掘任务，包括聚类分析、市场篮分析和预测。  
  
     该外接程序中包括的众所周知的计算机学习算法为 Naïve Bayes、逻辑回归、聚类分析、时序和神经网络。  
  
     如果您不熟悉数据挖掘，则可以使用 **“查询”** 向导帮助生成预测查询。  
  
     高级用户可通过拖放“高级查询编辑器”生成自定义 DMX 查询，或使用 Excel VBA 自动进行预测。****  
  
-   **记载和管理。** 创建了数据集并生成了一些模型后，通过生成数据和模型参数的统计摘要来记录您的工作和见解。  
  
-   **浏览和展现。** 数据挖掘不是可完全自动进行的活动-需要探索并理解结果才能采取有意义的操作。 该外接程序帮助您探索各种内容，其中在 Excel、Visio 模板中提供交互式查看器，使您可自定义模型关系图，还可将图表和表导出到 Excel 供进一步筛选或修改。  
  
-   **部署和集成。** 创建有用的模型后，通过使用管理工具将模型从试验服务器导出到另一个实例，使模型进入生产环境中 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  
  
     您还可以将模型保留在服务器上创建它时的位置，但使用 Integration Services 或 DMX 脚本刷新定型数据并运行预测。  
  
     高级用户一定会感激 **“跟踪”** 功能，通过该功能，可看到发送到服务器的 XMLA 和 DMX 语句。  
  
## <a name="getting-started"></a>入门  
 若要了解这些工具和进行设置，请参阅以下这些主题：  
  
-   [Excel 数据挖掘客户端 &#40;SQL Server 数据挖掘外接程序&#41;](../data-mining-client-for-excel-sql-server-data-mining-add-ins.md)  
  
-   [Excel 表分析工具](../table-analysis-tools-for-excel.md)  
  
-   [Visio 数据挖掘形状](../data-mining-shapes-for-visio.md)  
  
-   [连接到数据挖掘服务器](../connect-to-a-data-mining-server.md)  
  
## <a name="support-and-requirements"></a>支持和要求  
 可免费下载 SQL Server Office 数据挖掘外接程序。 必须已安装以下某个 Office 版本才能使用这些工具：  
  
-   Office 2010（32 位或 64 位版）  
  
-   Office 2013（32 位或 64 位版）  
  
> [!WARNING]  
>  请确保下载与您的 Excel 版本匹配的外接程序版本。  
  
 数据挖掘外接程序要求与以下 SQL Server Analysis Services 版本之一的连接：  
  
-   Enterprise  
  
-   商业智能  
  
-   Standard  
  
 根据所连接的 SQL Server Analysis Services 版本，某些高级算法可能不可用。 有关信息，请参阅[SQL Server 2014 的各个版本支持的功能](https://msdn.microsoft.com/library/cc645993.aspx)。  
  
 有关安装的其他帮助，请参阅下载中心上的此页：[https://www.microsoft.com/download/details.aspx?id=29061](https://www.microsoft.com/download/details.aspx?id=29061)  
  
  
