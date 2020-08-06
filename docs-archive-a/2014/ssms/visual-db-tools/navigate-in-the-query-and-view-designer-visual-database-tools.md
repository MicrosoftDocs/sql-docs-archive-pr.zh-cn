---
title: 在查询和视图设计器中导航 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, navigating
- shortcuts [SQL Server]
- Query Designer [SQL Server], navigating
- keyboard shortcuts [Visual Database Tools]
ms.assetid: 1c65acef-6dfa-463a-bf37-5a5335fe3865
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96ed54f7dfe2c2e7b76696b0c94def420775929b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693163"
---
# <a name="navigate-in-the-query-and-view-designer-visual-database-tools"></a>在查询和视图设计器中导航 (Visual Database Tools)
  可以使用键盘或鼠标在查询和视图设计器中工作。 具体使用方法，请参考以下各表：  
  
## <a name="any-pane"></a>任意窗格  
  
|**收件人**|**请按**|**单击“网络和共享中心”**|  
|------------|---------------|---------------|  
|在查询和视图设计器窗格中移动|F6、Shift+F6|目标窗格中的任意位置|  
  
> [!TIP]  
>  使用快捷键 Ctrl+Tab 不仅可以将焦点更改到查询和视图设计器窗格，还可以更改到其他窗格。  
  
## <a name="diagram-pane"></a>“关系图”窗格  
  
|**收件人**|**请按**|**单击“网络和共享中心”**|  
|------------|---------------|---------------|  
|在表、其他表结构对象和联接线（如果可用）之间移动|Tab 或 Shift+Tab|要移动到的表、表结构对象或联接线|  
|在表或表结构对象中的列之间移动|箭头键|要移动到的列|  
|选择要输出的选定数据列|空格键或加号键|列名旁的复选框|  
|从查询输出中移除选定的数据列|空格键或减号键|列名旁的复选框|  
|从查询中移除选定的表、表结构对象或联接线|DELETE|右键单击，再选择“删除” |  
  
> [!NOTE]  
>  如果选择了多个项，则按此键将影响所有选定的项。 按住 Ctrl 键并单击要选择的项，可以选择多个项。  
  
 有关详细信息，请参阅[“关系图”窗格 (Visual Database Tools)](visual-database-tools.md)。  
  
## <a name="criteria-pane"></a>“条件”窗格  
  
|目标|请按|单击|  
|--------|-----------|-----------|  
|在单元格之间移动|箭头键、Tab 或 Shift+Tab|目标单元格|  
|移动到选定列中的最后一行|Ctrl+向下键||  
|移动到选定列中的第一行|Ctrl+向上键||  
|移动到网格可见部分的左上角单元格|Ctrl+Home||  
|移动到右下角单元格|Ctrl+End||  
|在下拉列表中移动|向上键或向下键|单元格中的按钮|  
|选择整个网格列|Ctrl + 空格键|列标头|  
|在编辑模式和单元格选择模式间切换|F2||  
|将单元格中的选定文本复制到剪贴板（在编辑模式下）|Ctrl+C||  
|剪切单元格中的选定文本并将其放到剪贴板上（在编辑模式下）|Ctrl+X||  
|从剪贴板中粘贴文本（在编辑模式下）|CTRL+V||  
|在单元格中进行编辑时，在插入和替换模式间切换|Ins||  
|切换输出列中的复选框|空格键|复选框|  
|清除单元格中的选定内容|DELETE||  
|清除选定网格列的所有值|DELETE||  
|在现有行之间插入行|在选择网格行后按 Ins||  
|添加“或...”列|在选择任意“或...”列后按 Ins||  
  
> [!NOTE]  
>  如果选择了多个项，则按此键将影响所有选定的项。  
  
 有关详细信息，请参阅[“条件”窗格 (Visual Database Tools)](criteria-pane-visual-database-tools.md)。  
  
## <a name="sql-pane"></a>SQL 窗格  
 在 SQL 窗格中工作时，可以使用标准 Windows 编辑键（例如 Ctrl + 箭头键）在字词之间移动游标，也可使用“编辑”菜单上的“剪切”、“复制”和“粘贴”命令。  
  
> [!NOTE]  
>  只能插入文本；没有替换模式。  
  
 有关详细信息，请参阅 [ SQL 窗格 (Visual Database Tools)](sql-pane-visual-database-tools.md)。  
  
## <a name="results-pane"></a>“结果”窗格  
  
|**收件人**|**请按**|**单击“网络和共享中心”**|  
|------------|---------------|---------------|  
|在单元格之间移动|箭头键、Tab 或 Shift+Tab|目标单元格|  
|移动到当前行中的第一个或最后一个单元格|Home 或 End||  
|移动到当前列中的第一行|Ctrl+向上键||  
|移动到左上角的单元格|Ctrl+Home||  
|移动到第一列中的底部单元格|Ctrl+向下键||  
|选择到单元格中的第一个字符|Shift+Home||  
|选择到单元格中的最后一个字符|Shift+End||  
|在编辑模式和单元格选择模式间切换|F2||  
|在单元格中进行编辑时，在插入和替换模式间切换|Ins||  
|从表中删除行|DELETE||  
|撤消对当前单元格的更改|在更改的单元格中按 Esc||  
|撤消对当前行的更改|在尚未更改的单元格中按 Esc||  
|向单元格中输入空值|Ctrl+0||  
|将选定列或选定行复制到剪贴板|Ctrl+C||  
|将单元格中的选定文本复制到剪贴板（在编辑模式下）|Ctrl+C||  
|将单元格中的选定文本剪切到剪贴板（在编辑模式下）|Ctrl+X||  
|从剪贴板中粘贴文本（在编辑模式下）|CTRL+V||  
  
> [!NOTE]  
>  如果选择了多个项，则按此键将影响所有选定的项。  
  
 有关详细信息，请参阅 [“结果”窗格 (Visual Database Tools)](results-pane-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设计查询和视图操作指南主题 (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
