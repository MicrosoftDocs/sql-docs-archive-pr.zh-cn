---
title: 多维模型中的计算 |Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculations [Analysis Services], creating
- deleting calculations
- calculations [Analysis Services], scripts
- Cube Designer
- modifying scripts
- removing calculations
- calculations [Analysis Services], deleting
- scripts [Analysis Services], calculations
- cubes [Analysis Services], calculations
- solve orders [Analysis Services]
ms.assetid: c21b3459-9bef-45a2-aba5-c992eba5b66e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 64a9733c4fd198a9906e28c437f7ba4fb10dd39a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691998"
---
# <a name="calculations-in-multidimensional-models"></a>多维模型中的计算
  可以使用多维数据集设计器的“计算”选项卡创建计算成员、命名集和其他多维表达式 (MDX) 计算。****  
  
 **“计算”** 选项卡有以下三个窗格：  
  
-   **“脚本组织程序”** 窗格列出了多维数据集中的计算。 使用此窗格可以创建、组织和选择计算，以便进行编辑。  
  
-   **“计算工具”** 窗格提供了创建计算所需的元数据、函数和模板。  
  
-   “计算表达式”窗格支持窗体视图和脚本视图。  
  
> [!NOTE]  
>  有关 MDX 脚本编写的详细信息，请参阅 Microsoft TechNet 网站上[Analysis Services 2005 SQL Server](https://go.microsoft.com/fwlink/?LinkId=80853)的[Mdx 脚本编写介绍 Microsoft SQL Server 2005 中](https://go.microsoft.com/fwlink/?LinkId=81892)的 "其他资源" 部分。 有关与多维数据集设计相关的性能问题的详细信息，请参阅 [SQL Server 2005 Analysis Services 性能指南](https://download.microsoft.com/download/8/5/e/85eea4fa-b3bb-4426-97d0-7f7151b2011c/ssas2005perfguide.doc)。  
  
## <a name="creating-a-new-calculation"></a>创建新计算  
 若要创建新计算，请在多维数据集设计器的 **“计算”** 选项卡的 **“多维数据集”** 菜单中，单击 **“新建计算成员”**、 **“新建命名集”** 或 **“新建脚本命令”**，具体取决于希望创建的计算的类型。 还可以在工具栏上单击任何相应的按钮，或在“脚本组织程序”窗格中右键单击任何位置，再在快捷菜单中单击一个命令。**** 此操作会在 **“脚本组织程序”** 窗格中添加新的计算，并在“计算表达式”窗格内的计算窗体中显示它的字段。 如果创建新脚本，则此操作将在“计算表达式”窗格中打开“脚本”视图。 有关生成这三种计算类型的详细信息，请参阅 [创建计算成员](create-calculated-members.md)、 [创建命名集](create-named-sets.md)和 [定义赋值和其他脚本命令](define-assignments-and-other-script-commands.md)。  
  
## <a name="editing-scripts"></a>编辑脚本  
 在 "**计算**" 选项卡的 "计算表达式" 窗格中编辑脚本。"计算表达式" 窗格有两个视图：脚本视图和窗体视图。 窗体视图显示单个命令的表达式和属性。 编辑 MDX 脚本时，表达式框将充满整个窗体视图。  
  
 脚本视图提供了用来编辑脚本的代码编辑器。 当“计算表达式”窗格在脚本视图中时， **“脚本组织程序”** 窗格将隐藏。 脚本视图提供了彩色编码、括号匹配、自动完成和 MDX 代码区域。 MDX 代码区域可以折叠或展开，以便于进行编辑。  
  
 通过单击 **“多维数据集”** 菜单，再指向 **“计算显示位置”**，再单击 **“脚本”** 或 **“窗体”**，可以在窗体视图和脚本视图之间进行切换。 还可以在工具栏上单击 **“窗体视图”** 或 **“脚本视图”** 。  
  
## <a name="changing-solve-order"></a>更改求解顺序  
 将按照计算在 **“脚本组织程序”** 窗格中的列出的顺序来对计算求解。 通过右键单击任何计算，再在快捷菜单上单击“上移”或“下移”，可以让计算重新排序。******** 还可以单击计算，再单击工具栏上的 **“上移”** 或 **“下移”** 按钮。  
  
 对于计算单元和计算成员，可以手动覆盖此顺序。 有关传递顺序和求解次序的详细信息，请参阅[理解传递顺序和求解次序 (MDX)](mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
## <a name="deleting-a-calculation"></a>删除计算  
 若要删除现有计算，请在 **“计算”** 选项卡中的 **“脚本组织程序”** 窗格中选择要删除的计算，再在 **“编辑”** 菜单中单击 **“删除”** ，或在工具栏上单击 **“删除”** 图标。 还可以在“脚本组织程序”窗格中右键单击计算，并从快捷菜单中选择“删除”。********  
  
  
