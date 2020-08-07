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
# <a name="update-table-dialog-box-visual-database-tools"></a><span data-ttu-id="87823-102">“更新表”对话框 (Visual Database Tools)</span><span class="sxs-lookup"><span data-stu-id="87823-102">Update Table Dialog Box (Visual Database Tools)</span></span>
  <span data-ttu-id="87823-103">使用此对话框，可以指定要更新的表。</span><span class="sxs-lookup"><span data-stu-id="87823-103">This dialog box allows you to specify the table to be updated.</span></span>  
  
 <span data-ttu-id="87823-104">在您将查询的类型更改为“更新”查询时，如果“关系图”窗格中显示了多个表，则将显示此对话框。</span><span class="sxs-lookup"><span data-stu-id="87823-104">This dialog box appears if more than one table is displayed in the Diagram pane when you change a query's type to be an Update query.</span></span>  
  
 <span data-ttu-id="87823-105">选择要更新的表，然后选择 **"确定"**。 </span><span class="sxs-lookup"><span data-stu-id="87823-105">Select the table to update, and then choose **OK**.</span></span>\  
  
> [!NOTE]  
>  <span data-ttu-id="87823-106">如果表是为复制发布的，则必须使用 Transact-SQL 语句 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 或 SQL Server 管理对象 (SMO) 对架构进行更改。</span><span class="sxs-lookup"><span data-stu-id="87823-106">If the table is published for replication, you must make schema changes using the Transact-SQL statement [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) or SQL Server Management Objects (SMO).</span></span> <span data-ttu-id="87823-107">使用表设计器或数据库关系图设计器更改架构后，会尝试删除并重新创建表。</span><span class="sxs-lookup"><span data-stu-id="87823-107">When schema changes are made using the Table Designer or the Database Diagram Designer, it attempts to drop and recreate the table.</span></span> <span data-ttu-id="87823-108">由于您不能删除已发布的对象，因此架构更改将失败。</span><span class="sxs-lookup"><span data-stu-id="87823-108">You cannot drop published objects, therefore the schema change will fail.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="87823-109">另请参阅</span><span class="sxs-lookup"><span data-stu-id="87823-109">See Also</span></span>  
 [<span data-ttu-id="87823-110">创建“更新”查询 (Visual Database Tools)</span><span class="sxs-lookup"><span data-stu-id="87823-110">Create Update Queries &#40;Visual Database Tools&#41;</span></span>](visual-database-tools.md)  
  
  