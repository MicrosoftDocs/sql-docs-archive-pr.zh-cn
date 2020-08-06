---
title: " (Analysis Services) 设置分区切片属性 |Microsoft Docs"
ms.custom: ''
ms.date: 08/05/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
author: minewiskan
ms.author: owend
ms.openlocfilehash: f42c4536b99ba3fecf9b947942b881a3be72784f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588715"
---
# <a name="set-the-partition-slice-property-analysis-services"></a>设置分区切片属性 (Analysis Services)
  数据切片是一种很重要的优化功能，可以帮助将查询指向相应分区的数据。 通过覆盖为 MOLAP 和 HOLAP 分区生成的默认切片来显式设置 Slice 属性可提高查询性能。 此外，Slice 属性还在处理分区时提供额外的验证检查。  
  
 创建分区后，但在处理它之前，可以使用 Slice 属性指定一个数据切片。 在“分区”选项卡上，展开一个度量值组，右键单击一个分区，然后选择“属性”****。  
  
## <a name="defining-a-slice"></a>定义切片  
 Slice 属性的有效值是 MDX 成员、集合或元组。 以下示例说明了有效的切片语法：  
  
|切片|成员、集合或元组|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|对包含 2010 年的事实的分区指定此切片（假定模型包括具有 Calendar Year 层次的 Date 维度，且 2010 是其中的成员）。 虽然分区源 WHERE 子句或表可能已经按 2010 筛选，指定切片也能在处理过程以及查询执行期间的更有针对性的扫描中再一次进行检查。|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|对包含了具有销售区域信息的事实的分区指定此切片。 切片可以是由两个或更多成员组成的 MDX 集合。|  
|[Measures].[Sales Amount Quota] > '5000'|此切片显示了一个 MDX 表达式。|  
  
 分区的数据切片应尽可能真实地反映分区中的数据。 例如，如果某个分区仅限于 2012 年的数据，则分区的数据切片应该指定 Time 维度的成员 2012。 并不是所指定的每一个数据切片都能确切地反映分区内容。 例如，如果分区只包含 January 和 February 的数据，但 Time 维度的级别是 Year、Quarter 和 Month，则分区向导将无法同时选中成员 January 和 February。 在此情况下，应选择反映了分区内容的成员的父级成员。 在上例中，应选择 Quarter 1。  
  
 要了解有关数据切片好处的说明，请参阅 [对您的 SSAS 多维数据集分区设置切片](https://go.microsoft.com/fwlink/?LinkId=317783)。  
  
> [!NOTE]  
>  请注意，动态 MDX 函数（如 [Generate (MDX)](/sql/mdx/generate-mdx) 或 [Except (MDX)](/sql/mdx/except-mdx-function)）在分区的切片属性中不受支持。 你必须通过使用显式元组或成员引用定义切片。  
>   
>  例如，不是使用[： &#40;范围&#41; &#40;MDX&#41;](/sql/mdx/range-mdx)函数来定义一个范围，你需要按特定年份枚举每个成员。  
>   
>  如果需要定义复杂的切片，我们建议使用 XMLA Alter 脚本在切片中定义元组。 然后，你可以使用 ascmd 命令行工具或 SSIS [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) 任务运行该脚本并立即创建指定的成员集，之后再处理分区。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理本地分区 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)  
  
  
