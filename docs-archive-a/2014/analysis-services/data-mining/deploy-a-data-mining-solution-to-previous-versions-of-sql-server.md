---
title: 将数据挖掘解决方案部署到以前版本的 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [Analysis Services]
- holdout [data mining]
- deploy [Analysis Services]
- time series [Analysis Services]
- deploying [Analysis Services - data mining]
- synchronization [Analysis Services]
- deployment [Analysis Services]
ms.assetid: 2715c245-f206-43af-8bf5-e6bd2585477a
author: minewiskan
ms.author: owend
ms.openlocfilehash: f09a37c078cf58f24db9a08e3ddcb68cb2638717
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589965"
---
# <a name="deploy-a-data-mining-solution-to-previous-versions-of-sql-server"></a>将数据挖掘解决方案部署到以前版本的 SQL Server
  尝试将在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 实例中创建的数据挖掘模型或数据挖掘结构部署到使用 SQL Server 2005 Analysis Services 的数据库，或者将在 SQL Server 2005 中创建的模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例中时，有可能会遇到兼容性问题。本节将讲述这些已知的兼容性问题。  
  
 不支持部署到 SQL Server 2000 Analysis Services 实例。  
  
 [部署时序模型](#bkmk_TimeSeries)  
  
 [部署具有维持的模型](#bkmk_Holdout)  
  
 [部署具有筛选器的模型](#bkmk_Filter)  
  
 [从数据库备份还原](#bkmk_Backup)  
  
 [使用数据库同步](#bkmk_Synch)  
  
##  <a name="deploying-times-series-models"></a><a name="bkmk_TimeSeries"></a>部署时序模型  
 SQL Server 2008 中新增了一个辅助补充算法 ARIMA，从而增强了原有的 Microsoft 时序算法。 有关时序算法方面的更改的详细信息，请参阅 [Microsoft 时序算法](microsoft-time-series-algorithm.md)。  
  
 因此，使用新 ARIMA 算法的时序挖掘模型部署到 SQL Server 2005 Analysis Services 实例时的行为可能与以往不同。  
  
 如果在预测过程中已显式设置 PREDICTION_SMOOTHING 参数来控制 ARTXP 和 ARIMA 模型的混合，则在将该模型部署到 SQL Server 2005 实例时，Analysis Services 将引发错误，指出此参数无效。 若要避免产生此错误，必须删除 PREDICTION_SMOOTHING 参数并将以上两个模型转换为纯 ARTXP 模型。  
  
 反之，如果将使用 SQL Server 2005 Analysis Services 创建的时序模型部署到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例中，则使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]打开该挖掘模型时，定义文件将首先转换为新格式，并且默认情况下有两个新参数添加到所有时序模型中。 参数 FORECAST_METHOD 是使用默认值 MIXED 添加的，而参数 PREDICTION_SMOOTHING 是使用默认值 0.5 添加的。 不过，如果不重新处理该模型，该模型仍将只使用 ARTXP 算法进行预测。 一旦重新处理该模型，预测就改为同时使用 ARIMA 和 ARTXP。  
  
 因此，如果您不希望更改此模型，则应当只浏览该模型，绝对不可处理该模型。 或者，您可以显式设置 FORECAST_METHOD 或 PREDICTION_SMOOTHING 参数。  
  
 有关配置已混合模型的详细信息，请参阅 [Microsoft 时序算法技术参考](microsoft-time-series-algorithm-technical-reference.md)。  
  
 如果用于该模型数据源的访问接口是 SQL Client Data Provider 10，则还必须修改数据源定义以指定 SQL Server Native Client 的以前版本。 否则， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 将生成一个错误，指出提供程序未注册。  
  
##  <a name="deploying-models-with-holdout"></a><a name="bkmk_Holdout"></a>部署具有维持的模型  
 如果使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 创建了包含一个维持部分（用于测试数据挖掘模型）的挖掘结构，则该挖掘结构可以部署到 SQL Server 2005 实例，但此维持部分的信息将丢失。  
  
 使用 SQL Server 2005 Analysis Services 打开该挖掘结构时， [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 将引发错误，然后重新生成该结构以删除维持部分。  
  
 重新生成结构后，维持分区的大小在属性窗口中将不再可用;但是， \<ddl100_100:HoldoutMaxPercent> \</ddl100_100:HoldoutMaxPercent> ASSL 脚本文件中仍可能存在值 30) 。  
  
##  <a name="deploying-models-with-filters"></a><a name="bkmk_Filter"></a>部署具有筛选器的模型  
 如果使用 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 将某个筛选器应用于挖掘模型，则该模型可以部署到 SQL Server 2005 实例，但不会应用该筛选器。  
  
 打开该挖掘模型时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将引发错误，然后重新生成该模型以删除该筛选器。  
  
##  <a name="restoring-from-database-backups"></a><a name="bkmk_Backup"></a>从数据库备份还原  
 不能将使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 创建的数据库备份还原到 SQL Server 2005 实例。 否则，SQL Server Management Studio 将生成错误。  
  
 如果创建 SQL Server 2005 Analysis Services 数据库的备份并在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例中还原此备份，则所有时序模型都会进行上一节所述的修改。  
  
##  <a name="using-database-synchronization"></a><a name="bkmk_Synch"></a>使用数据库同步  
 不支持从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 到 SQL Server 2005 的数据库同步。  
  
 如果尝试同步 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 数据库，则服务器将返回错误，且数据库同步失败。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 向后兼容性](../analysis-services-backward-compatibility.md)  
  
  
