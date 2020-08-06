---
title: 数据库演化问题 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], multuser database changes
- database evolution [SQL Server]
ms.assetid: 1ed6ae10-d212-4ec2-8569-1b94ab1cba6d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 80daa694cd015a83657368902b07da254e6196ec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693166"
---
# <a name="issues-of-database-evolution-visual-database-tools"></a>数据库演化问题 (Visual Database Tools)
  如果更改已部署的数据库的结构，则必须特别留意更改应与现有的数据和数据库结构兼容。 当进行以下修改时，可能需要采取特殊步骤：  
  
-   **添加约束** 在添加约束时，数据库可能已经包含不满足该约束的数据。 当尝试保存新约束时，[“保存后通知”对话框 (Visual Database Tools)](visual-database-tools.md) 将通知你数据库服务器无法创建该约束。 若要强制数据库接受新约束，可以清除“在创建时检查现有数据”  复选框。  
  
-   **添加关系** 在添加关系时，数据库可能已经包含在主键表中没有相应行的外键表中的行。 即现有数据可能不满足引用完整性。 尝试保存新关系时，[“保存后通知”对话框 (Visual Database Tools)](visual-database-tools.md) 将通知你数据库服务器无法保存修改过的外键表。 若要强制数据库接受修改，可以清除“在创建时检查现有数据”  复选框。  
  
-   **修改分配给索引视图的表** 如果修改分配给 Microsoft SQL Server 索引视图的表，该视图的索引将丢失。 有关重新创建索引的信息，请参阅 SQL Server 联机丛书。  
  
-   **删除对象** 在删除某个对象（例如列、表或视图）时，应首先确保数据库中没有其他对象引用该对象。  
  
 无论如何更改数据库设计，都应保留更改的历史记录。 可以通过保留对成品数据库进行的所有修改的 SQL 脚本来保留所做更改。  
  
## <a name="see-also"></a>另请参阅  
 [Unique 约束和 Check 约束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [多用户环境 (Visual Database Tools)](multiuser-environments-visual-database-tools.md)  
  
  
