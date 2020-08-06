---
title: 使用转换对数据进行转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 952d8ea4eeea2dd8010a17a2b3deba41447b6231
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590930"
---
# <a name="transform-data-with-transformations"></a>使用转换对数据进行转换
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括三种类型的数据流组件：源、转换和目标。  
  
 下列关系图显示具有一个源、两个转换和一个目标的简单数据流。  
  
 ![数据流](../../media/mw-dts-08.gif "数据流")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 转换提供下列功能：  
  
-   拆分、复制与合并行集并执行查找操作。  
  
-   应用转换（如将小写更改为大写），从而更新列值和创建新列。  
  
-   执行商业智能操作，如清除数据、挖掘文本或运行数据挖掘预测查询。  
  
-   创建由聚合值或已排序值、示例数据或者透视数据和逆透视数据构成的新行集。  
  
-   执行导出与导入数据、提供审核信息以及使用渐变维度等任务。  
  
 有关详细信息，请参阅 [Integration Services Transformations](integration-services-transformations.md)。  
  
 还可以编写自定义转换。 有关详细信息，请参阅 [开发自定义数据流组件](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 和 [开发特定类型的数据流组件](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)。  
  
 将转换添加到数据流设计器之后但配置转换之前，请将数据流中另一转换或源的输出连接到此转换的输入，从而将此转换连接到数据流。 两个数据流组件之间的连接器称为路径。 有关连接组件和使用路径的详细信息，请参阅 [使用路径连接组件](../../connect-components-with-paths.md)。  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>将转换添加到数据流  
  
-   [在数据流中添加或删除组件](../add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>将转换连接到数据流  
  
-   [连接数据流中的组件](../connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>设置转换的属性  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据流任务](../../control-flow/data-flow-task.md)   
 [数据流](../data-flow.md)   
 [使用路径连接组件](../../connect-components-with-paths.md)   
 [数据中的错误处理](../error-handling-in-data.md)   
 [数据流](../data-flow.md)  
  
  
