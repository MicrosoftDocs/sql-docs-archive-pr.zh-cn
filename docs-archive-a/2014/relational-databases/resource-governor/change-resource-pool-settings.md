---
title: 更改资源池设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2183cceaaf8a3e183d96c154075f9a922942c2c6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688804"
---
# <a name="change-resource-pool-settings"></a>更改资源池设置
  可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]更改资源池设置。  
  
-   **开始之前：** [限制和局限](#LimitationsRestrictions)、[权限](#Permissions)  
  
-   若要更改资源池的设置，请使用：[SQL Server Management Studio](#ChgRPProp)、[Transact-SQL](#ChgRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 最大 CPU 百分比必须大于或等于最小 CPU 百分比。 最大内存百分比必须大于或等于最小内存百分比。  
  
 所有资源池的最小 CPU 百分比和最小内存百分比的总和不得超过 100。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 权限  
 更改资源池设置需要 CONTROL SERVER 权限。  
  
##  <a name="change-resource-pool-settings-using-sql-server-management-studio"></a><a name="ChgRPProp"></a> 使用 SQL Server Management Studio 更改资源池设置  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，然后依次逐步展开“管理”  节点直至其中包含“资源池” 。  
  
2.  右键单击要修改的资源池，然后单击“属性”。  
  
3.  在 **“资源调控器属性”** 页中，如果资源池所在的行未自动选中，则在 **“资源池”** 网格内将其选中。  
  
4.  在行中单击或双击要更改的单元，然后输入新值。  
  
5.  若要保存更改，请单击 **“确定”** 。  
  
##  <a name="change-resource-pool-settings-using-transact-sql"></a><a name="ChgRPTSQL"></a> 使用 Transact-SQL 更改资源池设置  
 **使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  运行指定要更改的属性值的 `ALTER RESOURCE POOL` 语句。  
  
2.  运行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例更改名为 `poolAdhoc`的资源池的最大 CPU 百分比设置。  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [创建资源池](create-a-resource-pool.md)   
 [删除资源池](delete-a-resource-pool.md)   
 [资源调控器工作负荷组](resource-governor-workload-group.md)   
 [资源调控器分类器函数](resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL (Transact-SQL)](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
