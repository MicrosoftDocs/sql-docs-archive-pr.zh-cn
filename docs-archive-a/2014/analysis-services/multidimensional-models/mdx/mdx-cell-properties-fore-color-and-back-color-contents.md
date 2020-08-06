---
title: " (MDX) FORE_COLOR 和 BACK_COLOR 内容 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
author: minewiskan
ms.author: owend
ms.openlocfilehash: 748754ec3c90bb44392d7acb7de8f815be24086e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691960"
---
# <a name="fore_color-and-back_color-contents-mdx"></a>FORE_COLOR 和 BACK_COLOR 内容 (MDX)
  `FORE_COLOR` 和 `BACK_COLOR` 单元属性分别以 Microsoft Windows 操作系统红绿蓝 (RGB) 格式存储单元的文本颜色信息和背景颜色信息。  
  
 普通 RGB 颜色的有效范围为 0 到 16,777,215 (&H00FFFFFF)。 此范围内数字的高位字节始终等于 0；低位的 3 个字节，从最低位字节到最高位字节分别决定了红色、绿色和蓝色的数量。 红色、绿色和蓝色成分分别由一个 0 到 255 (&HFF) 之间的数字表示。  
  
## <a name="see-also"></a>另请参阅  
 [使用单元属性 (MDX)](mdx-cell-properties-using-cell-properties.md)  
  
  
