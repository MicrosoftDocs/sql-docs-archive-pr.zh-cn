---
title: “变量”窗口 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.variables.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ffd6da67386291c14ebf588da9a1cf8f399214b3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588596"
---
# <a name="variables-window"></a>“变量”窗口
  可以使用“变量”窗口创建和修改用户定义变量，以及查看系统变量。   
  
 默认情况下， **“变量”** 窗口位于 **中 SSIS 设计器的** “连接管理器” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]区域之下。 如果看不到“变量”窗口，请单击 SSIS 菜单上的“变量”以显示该窗口    。  
  
 您可以通过将 View.Variables 命令映射到在 **“选项”** 对话框的 **“键盘”** 页上选择的组合键来显示 **“变量”** 窗口。  
  
> [!NOTE]
>  `Name` 和 `Namespace` 属性的值必须以 Unicode 标准 2.0 定义的字母字符或下划线 (_) 开头。 后续字符可以是在 Unicode 标准 2.0 中定义的字母或数字，或是下划线 (\_)。  
  
## <a name="options"></a>选项  
 **添加变量**  
 添加用户定义变量。  
  
 **移动变量**  
 单击列表中的变量，然后单击“移动变量”更改变量作用域。  在 **“选择新作用域”** 对话框中，选择包或包中的容器、任务或事件处理程序，以更改变量作用域。  
  
 有关变量作用域的详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)区域之下。  
  
 **删除变量**  
 从列表中选择变量，然后单击“删除变量”。   
  
 **网格选项**  
 单击此项可打开“变量网格选项”对话框，从中可以更改列选择并对“变量”窗口应用筛选器。   有关详细信息，请参阅 [变量网格选项](../../2014/integration-services/variable-grid-options.md)。  
  
 `Name`  
 查看变量名称。 您可以更新用户定义变量的名称。  
  
 **范围**  
 查看变量的作用域。 变量的作用域可以是整个程序包，也可以是容器或任务。 变量的作用域必须足够大，以便变量对任何需要读取或设置其值的其他任务或组件都是可见的。  
  
 您可以更改作用域，方法是单击该变量，然后单击 **“变量”** 窗口中的 **“移动变量”** 。  
  
 **数据类型**  
 查看变量的数据类型。 对于用户定义变量，你可以从列表中选择数据类型。  
  
> [!NOTE]  
>  如果为变量指定表达式，则无法更改数据类型。  
  
 **值**  
 查看变量值。 您可以更新用户定义变量的值。 此值可以是文字或表达式，还可以是多线串。 若要为变量指定表达式，请单击 **“变量”** 窗口中的 **“表达式”** 列旁边的省略号按钮。  
  
 `Namespace`  
 查看命名空间名称。 用户定义变量最初在**user**命名空间中创建，但您可以在字段中更改命名空间名称 `Namespace` 。 若要显示此列，请单击 **“网格选项”**。  
  
 **引发更改事件**  
 指示在值发生更改时是否引发 `OnVariableValueChanged` 事件。 您可以更新用户定义变量和系统变量的值。 默认情况下， **“变量”** 窗口不列出此列。 若要显示此列，请单击 **“网格选项”**。  
  
 **描述**  
 查看变量说明。 您可以更改用户定义变量的说明。 默认情况下， **“变量”** 窗口不列出此列。 若要显示此列，请单击 **“网格选项”**。  
  
 **表达式**  
 查看为变量指定的表达式。 若要指定表达式，请单击省略号按钮。  
  
 如果为变量指定了表达式，该变量旁边将显示特殊的图标标记。 这个特殊的图标标记还显示在设置有表达式的连接管理器和任务旁边。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)   
 [使用包中的变量](../../2014/integration-services/use-variables-in-packages.md)   
 [Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md)   
 [生成包执行的转储文件](troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
