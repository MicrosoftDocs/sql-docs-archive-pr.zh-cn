---
title: 定义引用的关系和引用的关系属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- referenced dimension relationship
- relationships [Analysis Services], referenced dimensions
ms.assetid: 5bb44b41-635b-4398-8fe9-0bfbb142553e
author: minewiskan
ms.author: owend
ms.openlocfilehash: a84cf2ed95ab3660c5a6b3c039dc58351dc43264
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689638"
---
# <a name="define-a-referenced-relationship-and-referenced-relationship-properties"></a>定义引用的关系和引用的关系属性
  引用维度关系是在多维数据集设计器的 **“维度用法”** 选项卡中定义的。 可通过指定下列各项来定义引用维度关系：  
  
-   要联接到的中间维度。 该维度可以是常规维度，也可以是其他引用维度。  
  
-   定义维度相对于度量值组进行聚合时可用的最低级别的引用维度属性。  
  
-   中间维度中对应于引用维度属性的（外键）属性。  
  
 注意将引用维度链接到事实数据表的列（通常是指引用维度中的键属性）还必须定义为中间维度中的属性。 当您创建引用维度链时，请从创建该链中第一个维度与度量值组之间的常规关系开始。 然后按顺序创建其他每个被引用关系。 只能对与该度量值组具有现有关系的维度建立被引用关系。  
  
 当创建引用维度关系时，便会默认具体化维度属性链接。 在处理过程中，具体化维度属性链接可在维度的 MOLAP 结构中具体化或存储事实数据表和每行的引用维度之间的链接值。 这样做对处理性能和存储要求的影响不大，但会增强查询性能。  
  
 在引用维度中，通过标识定义引用维度与对应于该维度主表的度量值组之间的关系的属性来指定粒度。 当多个引用维度相互链接时，这些引用便会定义从最外面的维度到度量值组的关系。  
  
  
