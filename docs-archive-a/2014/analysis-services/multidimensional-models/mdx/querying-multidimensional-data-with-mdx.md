---
title: 通过 MDX 查询多维数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7b7589a98636e56e8c592cef213785544e18f4ea
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589307"
---
# <a name="querying-multidimensional-data-with-mdx"></a>使用 MDX 查询多维数据
  多维表达式 (MDX) 是用于在中处理和检索多维数据的查询语言 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。 MDX 基于 XML for Analysis (XMLA) 规范，具有的特定扩展 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。 MDX 使用由标识符、值、语句、函数和运算符组成的表达式， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 可以通过计算表达式来检索某个对象（如集或成员）或标量值（如字符串或数字）。  
  
 中的 MDX 查询和表达式 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 用于执行以下操作：  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多维数据集返回到客户端应用程序 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。  
  
-   设置查询结果的格式。  
  
-   执行多维数据集设计任务，包括定义计算成员、命名集、范围分配和关键绩效指标 (KPI)。  
  
-   执行管理任务，包括维度和单元安全性。  
  
 MDX 在很多方面与关系数据库常用的 SQL 语法看起来很相似。 但是，MDX 并非 SQL 语言的扩展，在许多方面都有别于 SQL。 为了创建用于设计或保护多维数据集的 MDX 表达式，或创建 MDX 查询以返回多维数据并设置其格式，您需要了解有关 MDX 和维度建模的基本概念、MDX 语法元素、MDX 运算符、MDX 语句以及 MDX 函数。  
  
> [!NOTE]  
>  有关详细信息，请参阅 Microsoft TechNet 网站上的[SQL Server 2005-Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853)页上的 "其他资源" 部分。 有关与 MDX 查询和计算相关的性能问题的详细信息，请参阅[SQL Server 2005 Analysis Services 性能指南](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)中的 "编写有效的 MDX" 一节。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[MDX 中的重要概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)|您可以 (MDX) 使用多维表达式来查询多维数据或创建 MDX 表达式以便在多维数据集中使用，但首先应了解 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 维度的概念和术语。|  
|[MDX 查询基础知识 (Analysis Services)](mdx-query-fundamentals-analysis-services.md)|多维表达式 (MDX) 使您可以查询多维对象（如多维数据集）并返回包含该多维数据集的数据的多维单元集。 本主题及其子主题提供 MDX 查询的概述。|  
|[MDX 脚本编写基础知识 (Analysis Services)](mdx-scripting-fundamentals-analysis-services.md)|在中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ， (mdx) 脚本的多维表达式由一个或多个 mdx 表达式或语句构成，这些表达式或语句用计算结果填充多维数据集。<br /><br /> MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。<br /><br /> 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。|  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 语法元素 &#40;MDX&#41;](/sql/mdx/mdx-syntax-elements-mdx)   
 [MDX 语言参考 (MDX)](/sql/mdx/mdx-language-reference-mdx)  
  
  
