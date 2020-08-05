---
title: 创建工作负荷组 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 144bcef57b3d6e191b03b1539e9e7382a9085c93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580666"
---
# <a name="create-a-workload-group"></a>创建工作负荷组
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]创建工作负荷组。  
  
-   **开始之前：** [限制和局限](#LimitationsRestrictions)、[权限](#Permissions)  
  
-   若要创建工作负荷组，请使用：[SQL Server Management Studio](#CreWGProp)、[Transact-SQL](#CreWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 对非对齐的分区表创建索引所占用的内存与涉及的分区数成正比。 如果所需的内存总量超过工作负荷组设置为每个查询设定的限制 (REQUEST_MAX_MEMORY_GRANT_PERCENT)，则这种索引创建可能会失败。 由于默认工作负荷组允许查询超过每个查询的限制，并在开始时使用所需的最低内存以便与 SQL Server 2005 保持兼容，因此，如果默认资源池配置了足够多的内存总量以运行此类查询，则用户或许能够在默认工作负荷组中运行相同的索引创建。  
  
 允许索引创建操作使用比最初授予的工作区内存多的工作区内存，以便提高性能。 这个特别处理由资源调控器支持，然而，最初授予及任何其他内存授予都受工作负荷组和资源池设置的限制。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 权限  
 创建工作负荷组需要 CONTROL SERVER 权限。  
  
##  <a name="create-a-workload-group-using-sql-server-management-studio"></a><a name="CreWGProp"></a> 使用 SQL Server Management Studio 创建工作负荷组  
 **使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  在对象资源管理器中，依次逐步展开 **“管理”** 节点直至其中包含要修改的工作负荷组的资源池。  
  
2.  右键单击“工作负荷组”文件夹，然后单击“新建工作负荷组”。  
  
3.  在 **“资源池”** 网格中，确保突出显示要添加工作负荷组的资源池。  
  
4.  **“资源池的工作负荷组”** 网格将具有一个新行，其中包含一个空名称和其他列中的默认值。  
  
5.  单击 **“名称”** 单元，然后输入工作负荷组的名称。  
  
6.  在行中单击或双击要更改其默认设置的任何其他单元，然后输入新值。  
  
7.  若要保存更改，请单击 **“确定”** 。  
  
##  <a name="create-a-workload-group-using-transact-sql"></a><a name="CreWGTSQL"></a> 使用 Transact-SQL 创建工作负荷组  
 **使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  运行 CREATE WORKLOAD GROUP 语句，指定要设置的属性值。  
  
2.  运行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例创建一个名为 `groupAdhoc` 的工作负荷组，该组位于名为 `poolAdhoc`的资源池中。  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [创建资源池](create-a-resource-pool.md)   
 [更改工作负荷组设置](change-workload-group-settings.md)   
 [创建和测试分类器用户定义函数](create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP (Transact-SQL)](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
