---
title: CDC 拆分器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45dd16602625b28d2ca7e16f2fa6b0d62294fe81
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587944"
---
# <a name="cdc-splitter"></a>CDC 拆分器
  CDC 拆分器将更改行的单个流从 CDC 源数据流拆分到多个不同的数据流中以便用于插入、更新和删除操作。 基于必需的列 `__$operation` 及其在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更改表中的标准值来拆分数据流。  
  
|操作的值|输出|说明|  
|------------------------|------------|-----------------|  
|1|删除|删除的行|  
|2|插入|插入的行（使用“净值且具有合并”  CDC 模式时不可用）|  
|3|更新|更新前的行（仅在使用“全部且具有旧值”  CDC 模式时可用）|  
|4|更新|更新后的行（与更新前相同）|  
|5|更新|合并行（仅在使用“净值且具有合并”  CDC 模式时可用）|  
|其他|错误||  
  
 您可以使用拆分器连接到预定义的 INSERT、DELETE 和 UPDATE 输出以便进行进一步的处理。  
  
 此 CDC 拆分器转换有一个常规输入和一个错误输出。  
  
## <a name="error-handling"></a>错误处理  
 此 CDC 拆分器转换有一个错误输出。 具有 $operation 列的无效值的输入行被视为错误的，并且根据该输入的 **ErrorRowDisposition** 属性进行处理。  
  
 组件的错误输出包括以下输出列：  
  
-   **错误代码**：设置为 1。  
  
-   **错误列**：导致错误（针对转换错误）的源列。  
  
-   **错误行列**：导致了该错误的行的输入列。  
  
## <a name="configuring-the-cdc-splitter"></a>配置 CDC 拆分器  
 没有用于 CDC 拆分器的可配置属性。  
  
 有关使用 CDC 拆分器的详细信息，请参阅 Microsoft SQL Server Integration Services 的 CDC 组件。  
  
 **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
 打开 **“高级编辑器”** 对话框：  
  
-   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 CDC 拆分器，然后选择 **“显示高级编辑器”** 。  
  
## <a name="see-also"></a>另请参阅  
 [根据更改的类型定向 CDC 流](direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
