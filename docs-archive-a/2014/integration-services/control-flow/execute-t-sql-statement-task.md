---
title: 执行 T-SQL 语句任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ebc73ad843ac7fcf1dfbe7699ecd8ea53edcdad
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688107"
---
# <a name="execute-t-sql-statement-task"></a>执行 T-SQL 语句任务
  执行 T-SQL 语句任务运行 Transact-SQL 语句。 有关详细信息，请参阅 [Transact-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)和 [Integration Services (SSIS) 查询](../integration-services-ssis-queries.md)。  
  
 此任务类似于执行 SQL 任务。 但是，执行 T-SQL 语句任务只支持 SQL 语言的 Transact-SQL 版本，在使用 SQL 语言的其他方言的服务器上无法使用此任务来运行语句。 如果需要运行参数化查询，将查询结果保存到变量，或使用属性表达式，那么您应当使用执行 SQL 任务而不是执行 T-SQL 语句任务。 有关详细信息，请参阅 [Execute SQL Task](execute-sql-task.md)。  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>执行 T-SQL 任务的配置  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“执行 T-SQL 语句”任务（维护计划）](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [控制流](control-flow.md)   
 [在 Integration Services 包中执行 MERGE](merge-in-integration-services-packages.md)  
  
  
