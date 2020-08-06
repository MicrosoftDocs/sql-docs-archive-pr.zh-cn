---
title: 列排序 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e5fe56688a009fd60a7731b199f32352d78bb5eb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694445"
---
# <a name="sort-columns"></a>列排序
  可以使用 **“列排序”** 对话框，根据一个或多个列对复制监视器中的网格进行排序。 （也可以单击复制监视器网格中的列标题，按单个列进行排序）。 例如，若要基于状态对 **“所有订阅”** 选项卡中的订阅进行排序，再基于连接类型进行排序，请执行以下步骤：  
  
1.  在网格的第一行中，选择 **“列名”** 列中的 **“状态”** 并从 **“排序顺序”** 列中选择一个值。  
  
2.  在网格的第二行中，选择 **“列名”** 列中的 **“连接类型”** 并从 **“排序顺序”** 列中选择一个值。  
  
## <a name="options"></a>选项  
 **列名称**  
 要作为排序依据的列的名称。 可以按一个或多个列进行排序。 出于列值计算方式方面的原因，不能按 **“发布”** 选项卡上的 **“当前平均性能”** 或 **“当前最差的性能”** 列进行排序。  
  
 **排序顺序**  
 指定值为 **“升序”** 或 **“降序”** 。  
  
 **全部清除**  
 清除排序网格中的所有行。 若要移除某个行，请选择该行，然后按 Delete 键。  
  
## <a name="see-also"></a>另请参阅  
 [监视复制](monitoring-replication.md)  
  
  
