---
title: “更新表”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 426c842b85d6404ba101b57a9b572107dbc76bb5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588188"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>“更新表”对话框 (Visual Database Tools)
  使用此对话框，可以指定要更新的表。  
  
 在您将查询的类型更改为“更新”查询时，如果“关系图”窗格中显示了多个表，则将显示此对话框。  
  
 选择要更新的表，然后选择 **"确定"**。 \  
  
> [!NOTE]  
>  如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理对象 (SMO) 对架构进行更改。 使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。 由于您不能删除已发布的对象，因此架构更改将失败。  
  
## <a name="see-also"></a>另请参阅  
 [创建“更新”查询 (Visual Database Tools)](visual-database-tools.md)  
  
  
