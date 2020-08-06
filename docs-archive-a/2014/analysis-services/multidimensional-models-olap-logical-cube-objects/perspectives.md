---
title: 透视 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- ready-only cube view
- OLAP objects [Analysis Services], perspectives
- storing data [Analysis Services], perspectives
- perspectives [Analysis Services]
- cubes [Analysis Services], perspectives
- visibility [Analysis Services]
- storage [Analysis Services], perspectives
ms.assetid: b064171e-b1b4-4f32-95e5-59e1b831c4c9
author: minewiskan
ms.author: owend
ms.openlocfilehash: f385fd078500739d97394cd8856fc8bd6a3b87e8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690189"
---
# <a name="perspectives"></a>透视
  透视是一种定义，允许用户以一种更简单的方式查看多维数据集。 透视是多维数据集功能的子集。 管理员使用透视可以创建多维数据集的视图，从而帮助用户将注意力集中在与他们关系最为密切的数据上。 透视包含多维数据集所有对象的子集。 但它不能包含父多维数据集中未定义的元素。  
  
 简单 <xref:Microsoft.AnalysisServices.Perspective> 对象由基本信息、维度、度量值组、计算、KPI 和操作组成。 基本信息包括透视的名称和默认度量值。 维度是多维数据集维度的子集。 度量值组是多维数据集度量值组的子集。 计算是多维数据集计算的子集。 KPI 是多维数据集 KPI 的子集。 操作是多维数据集操作的子集。  
  
 使用透视之前，必须先更新和处理多维数据集。  
  
 多维数据集可能是非常复杂的对象，供用户浏览 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 单个多维数据集可以表示完整的数据仓库内容，一个多维数据集中可以有多个度量值组，以表示基于多个维度表的多个事实数据表和多个维度。 此类多维数据集可能非常复杂并且功能强大，但用户可能只需要与多维数据集的一小部分进行交互即可满足其商业智能和报表要求，因此这样的多维数据集会令用户感到过于复杂。  
  
 在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以使用透视来减小中多维数据集的感知复杂性 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 透视可定义多维数据集的可查看子集，借此您可以将注意力集中在多维数据集中的特定业务或特定应用程序上。 透视可控制多维数据集所包含对象的可见性。 可在透视中显示或隐藏以下对象：  
  
-   维度  
  
-   属性  
  
-   层次结构  
  
-   度量值组  
  
-   度量值  
  
-   关键绩效指标 (KPI)  
  
-   计算（计算成员、命名集和脚本命令）  
  
-   操作  
  
 例如，示例数据库中的**艾德工作**多维数据集 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含十一个度量值组和二十个不同的多维数据集维度，表示销售、销售预测和财务数据。 客户端应用程序可以直接引用完整的多维数据集，但如果用户试图提取基本销售预期信息，则这一点可能颇具吸引力。 相反，同一用户可以使用 "**销售目标**" 透视将 "**艾德公司**" 多维数据集的视图仅限制为与销售预测相关的对象。  
  
 多维数据集中通过透视对用户隐藏的对象仍可以使用 XML for Analysis (XMLA)、多维表达式 (MDX) 或数据挖掘扩展插件 (DMX) 语句直接进行引用和检索。 透视不会限制对多维数据集中对象的访问，而且也不应以此方式进行使用，相反，应使用透视来为访问多维数据集的用户提供更好的体验。  
  
 透视是多维数据集的只读视图；无法使用透视来重命名或更改多维数据集中的对象。 同样，也无法使用透视更改多维数据集的行为或功能（如可见总计的用法）。  
  
## <a name="security"></a>安全性  
 透视的用途不是为了作为一种安全机制，而是作为一个可在商业智能应用程序中为用户提供更好体验的工具。 特定透视的所有安全性都从基础多维数据集继承。 例如，透视无法让用户访问该用户尚未拥有访问权的多维数据集中的对象。 必须先解决多维数据集的安全性，然后才能通过透视访问多维数据集中的对象。  
  
  
