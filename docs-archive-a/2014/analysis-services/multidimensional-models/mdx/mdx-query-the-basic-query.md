---
title: 基本 MDX 查询 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], SELECT statement
- queries [MDX], about queries
- cellsets [MDX]
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: 4fa5a95a-fec9-4584-875c-dbf030c53e82
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6b1a70753abe8e477bd1e522a37f4513cc12a52
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589312"
---
# <a name="the-basic-mdx-query-mdx"></a>基本 MDX 查询 (MDX)
  MDX) 查询 (基本多维表达式是 SELECT 语句-MDX 中最常用的查询。 通过了解 MDX SELECT 语句如何指定结果集、SELECT 语句的语法是怎样的以及如何使用 SELECT 语句创建简单查询，您将切实理解如何使用 MDX 来查询多维数据。  
  
## <a name="specifying-a-result-set"></a>指定结果集  
 在 MDX 中，SELECT 语句可指定一个结果集，其中包含从多维数据集中返回的多维数据子集。 若要指定结果集，MDX 查询必须包含以下信息：  
  
-   希望结果集要包含的轴数。 最多可在 MDX 查询中指定 128 个轴。  
  
-   要包括在 MDX 查询的各个轴上的的成员或元组集。  
  
-   用于设置 MDX 查询上下文的多维数据集的名称。  
  
-   要包括在切片器轴上的成员或元组集。 有关切片器和查询轴的详细信息，请参阅[使用查询轴和切片器轴限定查询 (MDX)](mdx-query-and-slicer-axes-restricting-the-query.md)。  
  
 为了标识查询轴、要查询的多维数据集以及切片器轴，MDX SELECT 语句使用下列子句：  
  
-   SELECT 子句，用于确定 MDX SELECT 语句的查询轴。 有关在 SELECT 子句中构造查询轴的详细信息，请参阅[指定查询轴的内容 (MDX) ](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
-   用于确定将要查询的多维数据集的 FROM 子句。 有关 FROM 子句的详细信息，请参阅 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)。  
  
-   可选的 WHERE 子句，用于确定在切片器轴上使用哪些成员或元组来限制返回的数据。 有关在 WHERE 子句中构造切片器轴的详细信息，请参阅[指定切片器轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
> [!NOTE]  
>  有关 SELECT 语句的各种子句的详细信息，请参阅 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)。  
  
## <a name="select-statement-syntax"></a>SELECT 语句的语法  
 以下语法显示了一个包括 SELECT、FROM 和 WHERE 子句的基本 SELECT 语句用法：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 MDX SELECT 语句支持可选的语法（如 WITH 关键字），支持使用 MDX 函数来创建计算成员以便确定是否包含在轴或切片器轴中，并支持在查询中返回特定单元属性的值。 有关 MDX SELECT 语句的详细信息，请参阅 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)。  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>比较 MDX SELECT 语句的语法与 SQL 语法  
 MDX SELECT 语句所用的语法格式与 SQL 语法相似。 但也有几个基本差异：  
  
-   MDX 语法通过用大括号括住元组或成员来区分集， ({和} 个字符。 ) 有关成员、元组和集语法的详细信息，请参阅使用[成员、元组和集 &#40;MDX&#41;](working-with-members-tuples-and-sets-mdx.md)。  
  
-   MDX 查询在 SELECT 语句中可有 0、1、2 或最多 128 个查询轴。 每个轴具有完全相同的行为方式，这一点与 SQL 不同，后者的查询行为中，行和列之间存在显着的差异。  
  
-   像 SQL 查询一样，FROM 子句可为 MDX 查询指定数据源。 但是，MDX FROM 子句被限定为单个多维数据集。 若要检索来自其他多维数据集的信息，需要使用 LookupCube 函数逐个值地进行检索。  
  
-   WHERE 子句描述了 MDX 查询中的切片器轴。 它的作用就像一个无形的东西（查询中的额外轴），会对结果集的单元中显示的值进行切片；而 SQL WHERE 子句则不同，它不会直接影响查询的行轴上显示的内容。 可通过其他 MDX 功能（如 FILTER 函数）来获得 SQL WHERE 子句的功能。  
  
## <a name="select-statement-example"></a>SELECT 语句示例  
 以下示例显示了使用 SELECT 语句的基本 MDX 查询。 此查询返回包含 Southwest 销售区域 2002 和 2003 年度销售额和税额的结果集。  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 在此示例中，此查询定义了以下结果集信息：  
  
-   SELECT 子句将查询轴设置为 Measures 维度的 Sales Amount 和 Tax Amount 成员，以及 Date 维度的 2002 和 2003 成员。  
  
-   FROM 子句指明数据源为 Adventure Works 多维数据集。  
  
-   WHERE 子句将切片器轴定义为 Sales Territory 维度的 Southwest 成员。  
  
 请注意，此查询示例还使用了 COLUMNS 和 ROWS 轴别名。 也可以使用这些轴的序号位置。 以下示例显示了如何编写 MDX 查询以使用每个轴的序号位置：  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 有关更多详细示例，请参阅[指定查询轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) 和[指定切片器轴的内容 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
## <a name="see-also"></a>另请参阅  
 [MDX &#40;Analysis Services 中的关键概念&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [SELECT 语句 (MDX)](/sql/mdx/mdx-data-manipulation-select)  
  
  
