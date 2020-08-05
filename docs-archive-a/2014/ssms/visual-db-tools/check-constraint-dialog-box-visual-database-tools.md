---
title: “CHECK 约束”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7244984b869a1c68e597984a1cd03e16e53d0306
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576486"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>“CHECK 约束”对话框 (Visual Database Tools)
  如果在表设计器中右键单击表定义网格，再单击“CHECK 约束”  ，则会显示此对话框。 此对话框包含附加到数据库中表的非唯一约束的一组属性。 应用于唯一约束的属性则包含在“索引/键”  对话框中。  
  
> [!NOTE]  
>  如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="options"></a>选项  
 **选定的 CHECK 约束**  
 列出可用的 CHECK 约束。 若要查看约束的属性，请在列表中将其选定。  
  
 **添加**  
 为选定的数据库表创建一个新约束，并为该约束提供默认名称和其他值。 只有在为该约束输入表达式之后，该约束才会生效。  
  
 **删除**  
 从表中移除选定的约束。 若要取消添加 CHECK 约束，请使用此按钮来移除约束。  
  
 **常规类别**  
 展开此项可显示“表达式”  属性字段。  
  
 **表达式**  
 显示选定的 CHECK 约束的表达式。 对于新约束，必须先输入表达式，然后才能退出此框。 您还可以编辑现有的 CHECK 约束。 有关详细信息，请参阅 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。  
  
 **标识类别**  
 展开此项可显示“名称”  和“说明”  的属性。  
  
 **名称**  
 显示选定的 CHECK 约束的名称。 若要更改此约束的名称，请直接在属性字段键入文本。  
  
 **说明**  
 描述此 CHECK 约束。 既可以在属性字段中键入内容来编辑说明，也可以单击属性字段右侧显示的省略号按钮(…)，然后在“说明属性”对话框中编辑说明   。  
  
 **表设计器类别**  
 展开此项可显示“在创建或重新启用时检查现有数据”  、“强制用于 INSERT 和 UPDATE”  和“强制用于复制”  的属性。  
  
 **在创建或重新启用时检查现有数据**  
 指定是否根据约束验证所有预先存在的数据（创建约束前存在于表中的数据）。  
  
 **强制用于 INSERT 和 UPDATE**  
 指定在表中插入或更新数据时是否强制约束。  
  
 **强制用于复制**  
 指示当复制代理对此表执行插入或更新操作时是否强制约束。  
  
## <a name="see-also"></a>另请参阅  
 [Unique 约束和 Check 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [Visual Database Tools &#40;的 "索引和键" 对话框&#41;](visual-database-tools.md)  
  
  
