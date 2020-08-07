---
title: Excel 数据挖掘客户端 (SQL Server 数据挖掘外接程序) |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
author: minewiskan
ms.author: owend
ms.openlocfilehash: d82d7dc4192fedef5e37ac054531b33fc2d1823d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588778"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>Excel 数据挖掘客户端（SQL Server 数据挖掘外接程序）
  Excel 数据挖掘客户端是一组工具，通过这些工具，可执行常用的数据挖掘任务，包括从数据清理到建模和预测查询。 可使用 Excel 表或范围中的数据，也可访问外部数据源。  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [处理数据](#bkmk_Data)  
  
     将数据加载到 Excel，清理数据，检查是否存在离群值，然后创建统计摘要。 还可执行不同类型的抽样、分析数据和使用外部数据测试模型。 数据挖掘客户端是准备数据以供分析的最简单方法，不需要复杂的脚本或 ETL 进程。  
  
-   [生成模型和分析](#bkmk_Model)  
  
     这些工具针对已知的、经过了实践检验的数据挖掘算法提供向导界面，这些算法包括聚类分析（K-means 和 EM）、关联分析、时序分析和决策树。 通过每个向导的高级建模选项，可选择不同的算法（如 Naïve Bayes 或神经网络）和自定义聚类种子或初始抽样大小等行为。  
  
     所有数据挖掘算法均托管在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中，从而提高建立复杂模型的能力。  
  
-   [测试、查询和验证模型](#bkmk_Validate)  
  
     数据挖掘客户端提供用于测试模型的行业标准工具，包括提升图和交叉验证。 所提供的向导使检验数据集的有效性及其准确性变得轻而易举。 查询向导生成查询以使用模型进行预测和评分。  
  
-   [查看模型](#bkmk_ViewModels)  
  
     大多数工具生成的图表都可直接保存到 Excel。 使用[Excel 中的 "浏览模型" &#40;SQL Server 数据挖掘外接程序 "&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)工具浏览模型。  
  
-   [管理、记录和部署](#bkmk_UsageMgmt)  
  
     Excel 数据挖掘客户端与服务器之间保持一个活动连接，这样，您可以将数据挖掘模型保存到服务器以便用于进一步的测试，或者部署到生产服务器以便获得更高的可伸缩性。  
  
##  <a name="work-with-data"></a><a name="bkmk_Data"></a>处理数据  
 "**数据准备**" 组包含以下向导，可帮助您查看和清理数据，以便为数据挖掘任务做好准备。 大多数向导还允许您将数据划分为定型集和测试集。  
  
 [浏览数据挖掘外接 &#40;SQL Server 数据&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 为生成和存储模型，外接程序支持以下数据连接：  
  
-   与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器的连接，用于存储和处理模型。  
  
-   与外部数据源的可选连接。 您可以使用可定义为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源的任何数据类型生成您的模型，或者只使用 Excel 中已有的数据。  
  
 [浏览数据挖掘外接 &#40;SQL Server 数据&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 "**浏览数据**" 向导可帮助您了解数据表中数据的类型和数量，方法是将所选列的分布和值绘制一次。  
  
 [&#40;SQL Server 数据挖掘外接程序的示例数据&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 为模型的定型和测试创建正确类型的数据是数据挖掘的一个重要部分，但如果没有适当的工具，将非常单调乏味。 使用 "**示例数据**" 向导可以轻松地将用于模型的数据分为两组，一组用于生成模型，另一组用于测试模型。 您可以使用随机抽样或过度抽样。  
  
 [用于 Excel&#41;的预测计算器 &#40;表分析工具](prediction-calculator-table-analysis-tools-for-excel.md)  
 "**删除离群**值" 向导提供了几个工具用于标识和适当处理离群值。 该向导显示值的分布以及离群值与其他数据的关系，并且允许您决定是删除还是更改离群值。  
  
 [用于 Excel&#41;的预测计算器 &#40;表分析工具](prediction-calculator-table-analysis-tools-for-excel.md)  
 重新**标记**向导帮助您为数据创建新标签，以使其更易于理解分析结果。 例如，您可以使用更具说明性的名称或从列表中选择代表值，来重新命名数据区域。  
  
##  <a name="build-models-and-analyze"></a><a name="bkmk_Model"></a>生成模型并进行分析  
 通过工具栏的 "**数据建模**" 部分的选项，您可以从数据中派生模式;根据属性对数据行进行分组，或浏览关联。 此工具功能区中的向导基于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中强大的数据挖掘算法。 与 Excel 表分析工具中的类似工具不同，使用这些向导可以自定义算法的行为并使用多种数据源。  
  
 [用于 Excel 的数据挖掘外接程序 &#40;分类向导&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
 **分类**向导可帮助您基于 excel 表、excel 区域或外部数据源中的现有数据生成分类模型。 分类模型提取数据中表示相似性的模式，并帮助您基于值的分组进行预测。 例如，分类模型可用于根据收入或消费模式来预测风险。  
  
 **分类**向导支持使用以下 Microsoft 数据挖掘算法：决策树算法、逻辑回归、简单 Bayes、神经网络。  
  
 [估计向导 &#40;Excel 数据挖掘外接程序&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 **估计**向导帮助您创建估计模型。 估计模型从数据中提取数据模式，并且使用这些模式来预测数字结果，例如货币、销售金额、日期或时间。  
  
 **估计**向导使用以下 Microsoft 数据挖掘算法：决策树、线性回归、逻辑回归和神经网络。  
  
 [分析&#41;Excel &#40;表分析工具的关键影响因素](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 聚类分析向导帮助您生成聚类分析模型。 聚类分析模型检测各组具有相似特征的行。 此向导对于检测各种类型数据中的模式非常有用。  
  
 **群集**向导使用 Microsoft 聚类分析算法，包括 K 平均值和 EM。  
  
 [用于 Excel 的数据挖掘客户端的关联向导 &#40;&#41;](associate-wizard-data-mining-client-for-excel.md)  
 "**关联**" 向导帮助您使用 Microsoft 关联规则算法创建数据挖掘模型，该算法可检测经常发生的共存项或事件。 此类关联模型对于提出建议尤为有用。  
  
 **关联**向导使用 Microsoft 关联规则算法。  
  
 [预测向导 &#40;Excel 数据挖掘外接程序&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
 **预测**向导有助于您预测时序中的值。 通常，您在预测中使用的数据包含某种类型的时序（可以是日期戳或某个序列 ID），并且您使用该时序来派生模式以便用于预测将来值。  
  
 **预测**向导使用 Microsoft 时序算法。  
  
 [&#40;Excel 数据挖掘外接程序的高级建模&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
 是否已熟悉数据挖掘？ 您可以使用**高级**数据建模选项来创建自定义数据结构，并使用其他工具和向导中未包含的自定义项来生成模型。  
  
##  <a name="test-query-and-validate-models"></a><a name="bkmk_Validate"></a>测试、查询和验证模型  
 使用 "**准确性和验证**" 工具栏上的向导可以使用行业标准测试来验证模型的准确性，并评估用于创建模型的数据集的可用性。  
  
 [分析&#41;Excel &#40;表分析工具的关键影响因素](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 通过生成提升图或散点图来评估数据挖掘模型的性能。  
  
 [SQL Server 数据挖掘外接程序的分类矩阵 &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 通过创建基于模型的精确预测和不精确预测的汇总图表，帮助您评估分类模型的性能。  
  
 [SQL Server 数据挖掘外接程序的利润图 &#40;&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 通过将预测的准确性与基于预测所采取行动的成本和效益进行绘图，帮助您了解数据挖掘模型的影响。  
  
 [SQL Server 数据挖掘外接程序的交叉验证 &#40;&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 用于创建报表，汇总模型在数据集的多个子集间的准确性，以此确定模型的稳定程度。  
  
 您还可以将 Excel 表中的数据作为针对存储在服务器上的挖掘模型进行的预测查询的输入。  
  
 [查询 &#40;SQL Server 数据挖掘外接程序&#41;](query-sql-server-data-mining-add-ins.md)  
 **查询**向导可帮助您针对现有数据挖掘模型创建预测。  
  
 [高级数据挖掘查询编辑器](advanced-data-mining-query-editor.md)  
 对于高级用户，此工具提供针对 DMX 的拖放界面。 您可以轻松地创建预测查询或新模型，而不必担心语法。  
  
##  <a name="view-models"></a><a name="bkmk_ViewModels"></a>查看模型  
 所创建的模型将自动打开以供浏览。 但是，也可在服务器上浏览模型并生成新的可视化效果。 使用[Visio 形状](viewing-data-mining-models-in-visio-data-mining-add-ins.md)将模型图导出到可自定义的画布。  
  
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 使用对各种模型类型自定义的交互式图形查看您已创建的模型。  
  
 [记录挖掘模型 &#40;Excel 数据挖掘外接程序&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 此向导将创建提供有关模型的数据集和元数据的统计摘要的报表，以便帮助进行调查和解释。  
  
##  <a name="manage-document-and-deploy"></a><a name="bkmk_UsageMgmt"></a>管理、记录和部署  
 这些工具帮助您连接到某一数据挖掘服务器，管理和导出模型，以及监视数据挖掘活动。  
  
 [管理 &#40;SQL Server 数据挖掘外接程序的模型&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 如果具有所需的权限，您可以在不离开 Excel 的情况下删除、修改、重命名或处理现有挖掘模型和结构。  
  
 [&#40;Excel&#41;的数据挖掘客户端跟踪](trace-data-mining-client-for-excel.md)  
 单击 "**跟踪**" 可查看 Excel 客户端与服务器之间的交互的持续捕获 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 所有活动都作为 DMX 或 XMLA 语句存储，这样便于排除数据挖掘会话中的故障，也便于保存信息以备日后使用。  
  
 [连接到数据挖掘服务器](connect-to-a-data-mining-server.md)  
 若要将 Excel 用作数据挖掘客户端，您必须与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例建立连接。 通过该连接可以访问 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎。 如果有相应权限，您还可以通过该连接存储已发现的所有模式，并修改现有数据挖掘对象。  
  
 "**连接**" 工具栏提供了用于管理与实例的连接的向导 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 为了使用数据挖掘工具和算法，必须定义与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接。 您可以在安装外接程序时创建连接，也可以在以后添加连接。  
  
 **入门**  
 单击 "**入门**" 按钮启动配置向导，该向导将引导您完成创建实例连接的过程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，并获取执行数据挖掘所需的权限。  
  
 **帮助**  
 "**帮助**" 下拉菜单提供了指向联机帮助、网站和配置向导的链接，可帮助您完成设置和启动数据挖掘。  
  
 该“帮助”页还链接到在线资源，包括用于外接程序的帮助，以及附加的视频、演示和示例。  
  
## <a name="see-also"></a>另请参阅  
 [用于 Excel 的表分析工具](table-analysis-tools-for-excel.md)   
 [解决 Visio 数据挖掘关系图 &#40;SQL Server 数据挖掘外接程序&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
