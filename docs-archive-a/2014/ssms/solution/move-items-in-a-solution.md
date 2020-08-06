---
title: 在解决方案中移动项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: stevestein
ms.author: sstein
ms.openlocfilehash: fd0a8a89686c62b4d4d00aea5479bb956fe3011f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689219"
---
# <a name="move-items-in-a-solution"></a>在解决方案中移动项
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 项目中的项目项为查询、连接和杂项文件。 在解决方案资源管理器中，可以在项目之间移动查询和杂项文件，但无法移动连接。  
  
### <a name="to-move-items-in-solution-explorer"></a>在解决方案资源管理器中移动项  
  
1.  在解决方案资源管理器中，选择要移动的项。  
  
2.  在“编辑”  菜单上，单击“剪切”  。  
  
3.  在解决方案资源管理器中，选择目标位置。  
  
4.  在“编辑”  菜单上，单击“粘贴”  。  
  
 可以通过在解决方案资源管理器中拖动查询和杂项文件来移动项。 拖动可使您看到拖动操作的结果。 将查询从一个项目类型移动到另一个项目类型可能会导致查询在目标项目中被视为杂项文件。  
  
> [!NOTE]  
>  移动连接查询时不会移动与目标项目的连接。 查询移动到目标项目之后，将丢失其原有连接。  
  
## <a name="see-also"></a>另请参阅  
 [解决方案资源管理器](solution-explorer.md)   
 [复制解决方案中的项](copy-items-in-a-solution.md)  
  
  
