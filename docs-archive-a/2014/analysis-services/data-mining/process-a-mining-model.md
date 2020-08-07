---
title: 处理挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], processing
ms.assetid: c2204472-c500-47a5-9afa-7ce2ca78b233
author: minewiskan
ms.author: owend
ms.openlocfilehash: c2fed5d72c677dc175f4c9681096d1859b30d829
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690878"
---
# <a name="process-a-mining-model"></a>处理挖掘模型
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的数据挖掘设计器的“挖掘模型”选项卡中，您可以处理与挖掘结构关联的特定挖掘模型，也可以处理与结构关联的所有模型。  
  
 可以使用以下工具处理挖掘模型：  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
 还可以使用 XMLA 处理命令。 有关详细信息，请参阅[用于处理的工具和方法 (Analysis Services)](../multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)。  
  
### <a name="process-a-single-mining-model-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 处理单个挖掘模型  
  
1.  在数据挖掘设计器的 **“挖掘模型”** 选项卡上，从网格中的一列或多列模型中选择一个挖掘模型。  
  
2.  在 **“挖掘模型”** 菜单中，选择 **“处理模型”**。  
  
     如果更改了挖掘结构，系统将提示您在处理模型之前重新部署结构。 单击 **“是”** 。  
  
3.  在 "**处理挖掘模型 \<model> ** " 对话框中，单击 "**运行**"。  
  
     此时，将打开 **“处理进度”** 对话框，以显示模型处理的详细信息。  
  
4.  成功处理完模型之后，在 **“处理进度”** 对话框中，单击 **“关闭”** 。  
  
5.  在 "**处理挖掘模型 \<model> -** " 对话框中单击 "**关闭**"。  
  
 只有挖掘结构和所选挖掘模型被处理。  
  
### <a name="process-all-mining-models-that-are-associated-with-a-mining-structure"></a>处理与挖掘结构关联的所有挖掘模型  
  
1.  在数据挖掘设计器的 **“挖掘模型”** 选项卡中，从 **“挖掘模型”** 菜单中选择 **“处理挖掘结构和所有模型”** 。  
  
2.  如果更改了挖掘结构，系统将提示您在处理模型之前重新部署结构。 单击 **“是”** 。  
  
3.  在 "**处理挖掘结构 \<structure> ** " 对话框中，单击 "**运行**"。  
  
4.  此时，将打开 **“处理进度”** 对话框，以显示模型处理的详细信息。  
  
5.  成功处理完模型之后，在 **“处理进度”** 对话框中，单击 **“关闭”** 。  
  
6.  在 "**处理 \<model> ** " 对话框中单击 "**关闭**"。  
  
 挖掘结构和所有关联的挖掘模型被处理。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)  
  
  
