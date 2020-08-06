---
title: 将表添加到 CDC 实例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: edcd84db9e3c464334d407987cb3567f78edd44e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87683032"
---
# <a name="add-tables-to-a-cdc-instance"></a>将表添加到 CDC 实例
  使用“表选择”对话框可以将 Oracle 源中的附加表添加到 CDC 实例。 选定的表将添加到属性编辑器的 **“表”** 选项卡的列表中。  
  
 默认情况下，此对话框的表的列表中不包含任何表。 可以选中“(全选)”  复选框或搜索特定表。  
  
 **搜索特定表**  
 按如下所示输入搜索条件，然后单击“搜索”  ：  
  
-   **架构**：从列表中选择数据库架构。 只有具有该架构的表才会出现在列表中。  
  
-   **表名称模式**：输入任意字符串。 将仅显示包含输入的字符串的表。  
  
> [!NOTE]  
>  您可以在其中一个或全部两个字段中输入条件。  
  
-   **显示前 1000 个匹配表**：默认情况下选中此复选框。 它将显示限制为前 1000 个匹配表。 如果取消选中该复选框，将显示条件相匹配的所有表。 如果有大量的表，则此方法可能需要较长的时间来显示列表。  
  
 **选择要包括在 CDC 实例中的表**  
 单击要包含的任何表旁边的复选框，然后单击“添加”  。 相应的表将添加到新建实例向导的 **“选择表和列”** 页的列表中。  
  
 单击 **“关闭”** 将关闭该对话框并且不添加任何表。  
  
> [!NOTE]  
>  如果您选择包含不支持的数据类型的表，将会看到一条错误消息，并且将不会包含该表。  
  
> [!NOTE]  
>  您可以在查看器中查看表的列表。 在使用查看器时，信息是只读的。 查看器还在表中包括捕获列的列表。 有关如何访问查看器的信息，请参阅 [How to Manage a CDC Instance](manage-a-cdc-instance.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何编辑 CDC 实例属性](how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [为捕获更改选择 Oracle 表](select-oracle-tables-for-capturing-changes.md)  
  
  
