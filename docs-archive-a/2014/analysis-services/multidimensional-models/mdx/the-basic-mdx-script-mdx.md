---
title: 基本 MDX 脚本 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default MDX scripts
- statements [MDX]
- expressions [MDX], scripts
- scripts [MDX], about scripts
ms.assetid: 83d9afda-7d34-42b5-8f28-20172a905f23
author: minewiskan
ms.author: owend
ms.openlocfilehash: de0d2fea002beda0eca480bd27140bdd202fcb83
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691947"
---
# <a name="the-basic-mdx-script-mdx"></a>基本 MDX 脚本 (MDX)
   (MDX) 脚本的多维表达式定义中多维数据集的计算过程 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 。 有两种类型的 MDX 脚本：  
  
 **默认 MDX 脚本**  
 当创建多维数据集时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将为该多维数据集创建一个默认的 MDX 脚本。 此脚本定义整个多维数据集的计算过程。  
  
 **用户定义 MDX 脚本**  
 创建多维数据集后，可以添加用户定义 MDX 脚本，以扩展多维数据集的计算功能。  
  
## <a name="the-default-mdx-script"></a>默认 MDX 脚本  
 定义多维数据集时由 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 创建的默认 MDX 脚本包含单个 CALCULATE 语句。 这个 CALCULATE 语句位于默认 MDX 脚本的开始处，指明在第一次计算传递过程中应计算整个多维数据集。  
  
 默认 MDX 脚本还包含用来创建命名集、赋值以及计算成员（在多维数据集设计器中创建）的脚本命令：  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 直接将脚本命令添加到默认 MDX 脚本中。  
  
-   对于多维数据集中的每个命名集，默认 MDX 脚本中都有一个对应的 CREATE SET 语句。  
  
-   对于多维数据集中定义的每个计算成员，默认 MDX 脚本中都有一个对应的 CREATE MEMBER 语句。  
  
 可以通过使用多维数据集设计器的 **“计算”** 选项卡控制默认 MDX 脚本中的脚本命令、命名集以及计算成员的顺序。 有关定义存储在默认 MDX 脚本中的计算的详细信息，请参阅 [多维模型中的计算](../calculations-in-multidimensional-models.md)。  
  
 如果多维数据集没有相关的 MDX 脚本，将使用默认的 MDX 脚本。 一个多维数据集至少要与一个 MDX 脚本相关联，因为多维数据集依赖于 MDX 脚本来确定计算行为。 也就是说，未与 MDX 脚本关联或与空 MDX 脚本关联的多维数据集不会也不能计算任何单元。 如果使用 Analysis Services 脚本语言 (ASSL) 命令或 Analysis Management Objects (AMO) 通过编程的方式创建多维数据集，建议为该多维数据集创建包含单个 CALCULATE 语句的默认 MDX 脚本。  
  
## <a name="mdx-script-content"></a>MDX 脚本的内容  
 MDX 脚本可以包含下列语句和表达式：  
  
 所有 MDX 脚本语句  
 在 MDX 脚本中，MDX 脚本语句控制计算的上下文和作用域，并管理 MDX 脚本中其他语句的行为。 此类别包括下列语句：  
  
-   [计算](/sql/mdx/mdx-scripting-calculate)  
  
-   [&](/sql/mdx/mdx-scripting-freeze)  
  
-   [内](/sql/mdx/mdx-scripting-scope)  
  
 有关 MDX 脚本编写语句的详细信息，请参阅 [MDX 脚本编写语句](/sql/mdx/mdx-scripting-statements-mdx)。  
  
 [CREATE MEMBER](/sql/mdx/mdx-data-definition-create-member)  
 CREATE MEMBER 语句可以创建计算成员。 有关如何创建计算成员的详细信息，请参阅[在 MDX 中生成计算成员 (MDX)](mdx-calculated-members-building-calculated-members.md)。  
  
 [CREATE SET](/sql/mdx/mdx-data-definition-create-set)  
 CREATE SET 语句可以创建命名集。 有关如何创建命名集的详细信息，请参阅[在 MDX 中生成命名集 (MDX)](mdx-named-sets-building-named-sets.md)。  
  
 条件语句  
 条件语句可以将条件逻辑添加到 MDX 脚本中。 此类别包括 [CASE](/sql/mdx/case-statement-mdx) 语句和 [IF](/sql/mdx/mdx-scripting-if) 语句。  
  
 赋值表达式  
 赋值表达式为受约束的子多维数据集指定表达式，例如值。 受约束的子多维数据集表达式是定义 MDX 脚本中子多维数据集的“边界”的受约束的集表达式的集合。 下列代码显示了受约束的子多维数据集表达式的语法：  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 语言参考 &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [MDX 脚本编写基础知识 (Analysis Services)](mdx-scripting-fundamentals-analysis-services.md)  
  
  
