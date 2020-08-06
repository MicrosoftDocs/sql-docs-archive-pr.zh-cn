---
title: "\"添加多维数据集维度\" 对话框 (Analysis Services 多维数据) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.addcubedimensiondialog.f1
helpviewer_keywords:
- Add Cube Dimension dialog box
ms.assetid: 625a3b1f-183b-445f-9bb7-96945c324767
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0de75c02c39b0690184f35f2b0b6a07d7ed9a4f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578537"
---
# <a name="add-cube-dimension-dialog-box-analysis-services---multidimensional-data"></a>“添加多维数据集维度”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “添加多维数据集维度” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，在多维数据集中添加对数据库维度的引用。 通过执行下列操作之一，可以显示 **“添加多维数据集维度”** 对话框：  
  
-   在多维数据集设计器中的 **“多维数据集结构”** 或 **“维度用法”** 选项卡上，单击 **“工具栏”** 窗格中的 **“添加多维数据集维度”** 。  
  
-   在多维数据集设计器中的“多维数据集结构”选项卡上，右键单击“维度”窗格，再从上下文菜单中选择“添加多维数据集维度”。************  
  
-   在多维数据集设计器中的“维度用法”选项卡上，右键单击“网格”窗格，再从上下文菜单中选择“添加多维数据集维度”。************  
  
> [!NOTE]  
>  每个多维数据集维度与度量值组之间只能有一个关系。 不过，如果多维数据集维度所基于的数据库维度通过数据源视图中的多个关系与度量值组相关，则可以创建多个多维数据集维度并将其添加到多维数据集。 此类维度称为角色共享维度，通常与时间维度一起使用。  
  
## <a name="options"></a>选项  
 **选择维度**  
 选择现有数据库维度，将基于该数据库维度的多维数据集维度添加到所选多维数据集。 基于同一个数据库维度可以定义多个多维数据集维度。  
  
> [!NOTE]  
>  如果将基于同一个数据库维度的多个多维数据集维度添加到多维数据集，额外添加的多维数据集维度则称为角色共享维度。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
