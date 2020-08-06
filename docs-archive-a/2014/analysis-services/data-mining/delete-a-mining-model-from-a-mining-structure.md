---
title: 从挖掘结构中删除挖掘模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 72c79dcdccf6225b8e75144f8b090dcab7506c10
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589967"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>从挖掘结构中删除挖掘模型
  您可以使用数据挖掘设计器、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 DMX 语句删除挖掘模型。  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 删除挖掘模型  
  
1.  在 **中，选择** “挖掘模型” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡。  
  
2.  右键单击要删除的模型，然后选择“删除”****。  
  
     将打开 **“删除对象”** 对话框。  
  
3.  单击“确定”  。  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 删除挖掘模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开包含模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
2.  展开 **“挖掘结构”**，然后展开 **“挖掘模型”**。  
  
3.  右键单击要删除的模型，然后选择“删除”****。  
  
     删除模型并不删除定型数据，只删除定型时创建的元数据和所有模式。  
  
### <a name="delete-a-mining-model-using-dmx"></a>使用 DMX 删除挖掘模型  
  
-   [删除挖掘模型 (DMX)](/sql/dmx/drop-mining-model-dmx)  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)  
  
  
