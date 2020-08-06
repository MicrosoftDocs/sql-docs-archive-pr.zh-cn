---
title: 移动工作负荷组 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7f73b48f0ec2255760b4ee55acfaf91dc02af7cd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689308"
---
# <a name="move-a-workload-group"></a>移动工作负荷组
  您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Transact-SQL 将资源调控器工作负荷组移动到其他资源池。  
  
-   **开始之前：** [限制和局限](#LimitationsRestrictions)、[权限](#Permissions)  
  
-   若要移动工作负荷组，请使用：[SQL Server Management Studio](#MoveWGSSMS)、[Transact-SQL](#MoveWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
 如果存在挂起的资源调控器配置操作，则无法移动工作负荷组。  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 如果存在挂起的资源调控器配置操作，则无法移动工作负荷组。 你可以通过查询 [sys.dm_resource_governor_configuration (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) 动态管理视图来获取 is_configuration_pending 的当前状态以确定是否存在配置挂起。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 权限  
 移动工作负荷组需要 CONTROL SERVER 权限。  
  
##  <a name="move-a-workload-group-using-sql-server-management-studio"></a><a name="MoveWGSSMS"></a> 使用 SQL Server Management Studio 移动工作负荷组  
 **使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  在对象资源管理器中，依次逐步展开 **“管理”** 节点直至 **“资源调控器”** 。  
  
2.  右键单击“资源调控器”  ，然后单击“属性” ，这将打开“资源调控器属性”页  。  
  
3.  在 **“资源池”** 窗口中，单击包含要移动的工作负荷组的资源池。 此时， **“工作负荷组”** 窗口会列出该资源池中的工作负荷组。  
  
4.  在“工作负荷组”窗口中，右键单击要移动的工作负荷组左侧的向右箭头，然后单击“移到”。 这将显示 **“移动工作负荷组”** 窗口。  
  
5.  在窗口中显示可用的资源池。 单击要将工作负荷组移动到的资源池的名称，然后单击 **“确定”** 执行此操作。  
  
6.  只有在您单击 **“确定”** 之后，此操作才能完成。 单击 **“确定”** 后，将执行 ALTER RESOURCE GOVERNOR RECONFIGURE 语句。  
  
7.  如果创建或重新配置资源池或工作负荷组的操作失败，错误消息摘要将显示在属性页标题下方。 若要查看详细的错误消息，请单击错误信息上的向下箭头。  
  
##  <a name="move-a-workload-group-using-transact-sql"></a><a name="MoveWGTSQL"></a> 使用 Transact-SQL 移动工作负荷组  
 **使用 Transact-SQL 移动工作负荷组**  
  
1.  运行 `ALTER WORKLOAD GROUP` 语句，该语句指定要移动的工作负荷组的名称以及该组应移到的资源池。  
  
2.  运行 **ALTER RESOURCE GOVERNOR RECONFIGURE** 语句。  
  
### <a name="example-transact-sql"></a>示例 (Transact-SQL)  
 以下示例将一个名为 `groupAdhoc` 的工作负荷组移动到默认资源池。  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [资源调控器](resource-governor.md)   
 [启用资源调控器](enable-resource-governor.md)   
 [创建资源池](create-a-resource-pool.md)   
 [创建工作负荷组](create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP (Transact-SQL)](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [ALTER RESOURCE GOVERNOR (Transact-SQL)](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
