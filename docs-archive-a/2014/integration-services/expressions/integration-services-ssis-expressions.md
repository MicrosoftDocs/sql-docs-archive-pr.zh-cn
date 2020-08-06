---
title: Integration Services (SSIS) 表达式 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ff0bd46034108537ebede7567b042997c94871ce
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689990"
---
# <a name="integration-services-ssis-expressions"></a>Integration Services (SSIS) 表达式
  表达式是生成单个数据值的符号（标识符、文字、函数和运算符）的组合。 简单的表达式可以是单个常量、变量或函数。 更多情况下，表达式较为复杂，会使用多个运算符和函数，并且引用多个列和变量。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，表达式可以用于定义 CASE 语句的条件，创建和更新数据列中的值，为变量赋值，在运行时更新或填充属性，定义优先约束中的约束，以及提供 For 循环容器所使用的表达式。  
  
 表达式基于表达式语言和表达式计算器。 表达式计算器分析表达式，并确定表达式是否按照表达式语言的规则执行。 有关表达式语法和支持的文本和标识符的详细信息，请参阅以下主题：  
  
-   [语法 (SSIS)](syntax-ssis.md)  
  
-   [文字 (SSIS)](numeric-string-and-boolean-literals.md)  
  
-   [标识符 (SSIS)](identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>使用表达式的组件  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中的下列元素可以使用表达式：  
  
-   有条件拆分转换可以根据表达式实现决策结构，将数据行定向到不同目标。 有条件拆分转换中所使用的表达式的计算结果必须为 `true` 或 `false`。 例如，如果行满足表达式“Column1 > Column2”中的条件，则可以路由到单独的输出。  
  
-   派生列转换使用通过表达式所创建的值来填充数据流中的新列或更新现有列。 例如，表达式 Column1 + " ABC" 可以用于更新值，或创建具有串联字符串的新值。  
  
-   变量可以使用表达式来设置其值。 例如，GETDATE() 可以将变量的值设置为当前日期。  
  
-   优先约束可以使用表达式指定确定在包中运行约束任务还是容器的条件。 优先约束中使用的表达式的计算结果必须为 `true` 或 `false`。 例如，表达式“\@A > \@B”比较两个用户定义的变量，以确定是否运行受约束任务。  
  
-   For 循环容器可以使用表达式来生成循环结构使用的初始化语句、计算语句、增量语句。 例如，表达式 \@Counter = 1 初始化循环计数器。  
  
 表达式还可以用于更新包、容器（如 For 循环和 Foreach 循环）、任务、包和项目级连接管理器、日志提供程序以及 Foreach 枚举器的属性值。 例如，使用属性表达式，可以将字符串“Localhost.AdventureWorks”分配给执行 SQL 任务的 ConnectionName 属性。 有关详细信息，请参阅 [在包中使用属性表达式](use-property-expressions-in-packages.md)。  
  
## <a name="icon-markers-for-expressions"></a>表达式的图标标记  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，设置有表达式的连接管理器、变量和任务旁边会显示特殊的图标标记。 **HasExpressions** 属性在支持表达式（变量除外）的所有 SSIS 对象上均可用。 通过该属性，您可以轻松识别出哪些对象具有表达式。  
  
## <a name="expression-builder"></a>表达式生成器  
 表达式生成器是一种用于生成表达式的图形工具。 **“有条件拆分转换编辑器”** 对话框、 **“派生列转换编辑器”** 对话框和 **“表达式生成器”** 对话框中提供的表达式生成器是用于生成表达式的图形工具。  
  
 表达式生成器提供包含包特定元素的文件夹，还提供包含表达式语言所提供的函数、类型转换和运算符的文件夹。 包特定元素包括系统变量和用户定义的变量。 在 **“有条件拆分转换编辑器”** 对话框和 **“派生列转换编辑器”** 对话框中，您还可以查看数据列。 若要为转换生成表达式，可以将项从文件夹中拖到 **“条件”** 或 **“表达式”** 列中，也可以直接在列中键入表达式。 表达式生成器会自动添加所需的语法元素，如变量名的 \@ 前缀。  
  
> [!NOTE]  
>  用户定义的变量名和系统变量名区分大小写。  
  
 变量具有作用域，因此表达式生成器中的 **“变量”** 文件夹只列出处于作用域中并且可以使用的变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [在数据流组件中使用表达式](../use-an-expression-in-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
 social.technet.microsoft.com 上的技术文章 [SSIS 表达式示例](https://go.microsoft.com/fwlink/?LinkId=220761)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
