---
title: 撤消签出 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ff6e6041b59caa75bf7f8530d915db48e0379338
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577793"
---
# <a name="undo-checkouts"></a>撤消签出
  您可以使用 "**撤消签出**" 命令取消现有的签出。 如果您修改并保存了文件，但事后需要回滚所做的更改，此命令尤其有用。  
  
 根据你在 "**撤消签出高级选项**" 对话框中设置的选项，Studio 环境会将项的工作副本保留在本地磁盘上，或将其替换为最新的受源代码管理的版本。 如果有人在源代码管理系统环境以外更改了项，那么检索到的版本就可能不是最新版本。  
  
### <a name="to-undo-a-checkout"></a>撤消签出  
  
1.  在“解决方案资源管理器”中，选择项目。  
  
2.  在 "**文件**" 菜单上，指向 "**源代码管理**"，然后单击 "**撤消签出**"。  
  
3.  在 "**撤消签出**" 对话框中，选择相应的选项，然后单击 "**撤消签出**" 按钮。  
  
     **“列”**  
     标识要显示的列及其显示顺序。  
  
     **平面视图**  
     将项在其源代码管理连接下显示为平面列表。  
  
     **名称**  
     显示要撤消签出的项的名称。 所显示项旁边的复选框处于选中状态。 如果不想撤消对某项的签出，请清除其复选框。  
  
     **选项**  
     单击按钮右侧的箭头时，显示源代码管理插件特定的撤消签出选项。  
  
     **Sort**  
     对显示列进行排序。  
  
     **树视图**  
     显示要撤消签出的项的文件夹和项层次结构。  
  
     **撤消签出**  
     撤消签出，放弃对已签出文件所做的任何更改。  
  
## <a name="see-also"></a>另请参阅  
 [签出文件](../../2014/database-engine/check-out-files.md)   
 [管理签出](../../2014/database-engine/manage-checkouts.md)  
  
  
