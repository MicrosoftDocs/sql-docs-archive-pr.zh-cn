---
title: 设置优先约束的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Precedence Constraint Editor dialog box
- precedence constraints [Integration Services], properties
ms.assetid: d990f600-5c09-4cd5-8528-0a58d79dc9f2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 55b95bdb79d801156bef6198bc0f57accb5d9517
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590271"
---
# <a name="set-the-properties-of-a-precedence-constraint"></a>设置优先约束的属性
  若要设置优先约束属性，您可以使用下列工具之一：  
  
-   可以使用 **“优先约束编辑器”** 对话框。  
  
-   可以使用“属性”窗口。 “属性”窗口列出了用于对 **“优先约束编辑器”** 对话框中未提供的优先约束进行配置的属性。 在“属性”窗口中，您可以提供优先约束的说明和名称，也可以配置要在设计图面上为优先约束显示的批注。  
  
 下面的过程介绍如何使用下列每种工具设置优先约束的属性。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-precedence-constraint-editor"></a>使用优先约束编辑器设置优先约束属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  双击优先约束。  
  
     **“优先约束编辑器”** 将打开。  
  
5.  在“求值运算”下拉列表中，选择求值运算。****  
  
6.  在 `Value` 下拉列表中，选择优先可执行文件的执行结果。  
  
7.  如果求值运算使用表达式，请在 `Expression` 框中键入表达式，然后单击 "**测试**" 以计算表达式。  
  
    > [!NOTE]  
    >  变量名称区分大小写。  
  
8.  如果多个任务或容器连接到受约束的可执行文件，请选择 "**逻辑与**" 以指定所有前面的可执行文件的执行结果必须计算为 `true` 。 选择 "**逻辑或**" 以指定只有一个执行结果的计算结果为 `true` 。  
  
9. 单击 **“确定”** ，关闭 **“优先约束编辑器”**。  
  
10. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-set-the-properties-of-a-precedence-constraint-by-using-the-properties-window"></a>使用“属性”窗口设置优先约束属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含要修改的包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 "**控制流**" 选项卡。在 "**控制流**" 选项卡的设计图面上，右键单击优先约束，然后单击 "**属性**"。 在“属性”窗口中修改属性值。  
  
4.  在“属性”窗口中，设置优先约束的下列读/写属性：****  
  
    |读/写属性|配置操作|  
    |--------------------------|--------------------------|  
    |说明|提供说明。|  
    |EvalOp|选择一个求值运算。 如果 `Expression` 选择了、 **ExpressionAndConstant**或**expressionorconstant 运算**操作，则可以指定一个表达式。|  
    |Expression|如果求值运算包含 and 表达式，则请提供一个表达式。 表达式的计算结果必须为布尔值。 有关表达式语言的详细信息，请参阅 [Integration Services (SSIS) 表达式](expressions/integration-services-ssis-expressions.md)。|  
    |LogicalAnd|设置 `LogicalAnd` 此项可指定在多个可执行文件位于或链接到受约束的可执行文件时，优先约束与其他优先约束一起计算|  
    |名称|更新优先约束的名称。|  
    |ShowAnnotation|指定要使用的批注类型。 选择 **Never** 可以禁用批注；选择 **AsNeeded** 可以启用按需批注；选择 **ConstraintName** 可以使用 Name 属性的值自动进行批注；选择 **ConstraintDescription** 可以使用 Description 属性的值自动进行批注；选择 **ConstraintOptions** 可以使用 Value 和 Expression 属性的值自动进行批注。|  
    |值|如果在 EvalOP 属性中指定的求值运算包含约束，请选择受约束的可执行文件的执行结果。|  
  
5.  关闭“属性”窗口。  
  
6.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [优先约束](control-flow/precedence-constraints.md)   
 [使用默认优先约束来连接任务和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [使用快捷菜单设置优先约束的值](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [在优先约束中使用表达式](../../2014/integration-services/use-an-expression-in-a-precedence-constraint.md)  
  
  
