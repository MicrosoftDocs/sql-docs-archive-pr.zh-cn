---
title: 使用现有层次结构数据填充表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
author: stevestein
ms.author: sstein
ms.openlocfilehash: 966548b11ad4697abc06de5c5c239a511f80b7af
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687747"
---
# <a name="populating-a-table-with-existing-hierarchical-data"></a>使用现有层次结构数据填充表
  此任务将创建新表，然后使用 EmployeeDemo**** 表中的数据填充该表。 此任务包含以下步骤：  
  
-   创建一个包含 `hierarchyid` 列的新表。 此列可替换现有的 **EmployeeID** 和 **ManagerID** 列。 但是，您将保留这些列。 这是因为现有应用程序可能会引用这些列，而且它们还有助于您了解传输后的数据。 表定义将 **OrgNode** 指定为主键，这就要求该列包含唯一值。 **OrgNode** 列的聚集索引将使用 **OrgNode** 序列存储日期。  
  
-   创建一个用于跟踪直接向每个经理报告的雇员人数的临时表。  
  
-   使用 **EmployeeDemo** 表中的数据填充新表。  
  
### <a name="to-create-a-new-table-named-neworg"></a>创建一个名为 NewOrg 的新表  
  
-   在查询编辑器窗口中，运行下列代码以创建名为 **HumanResources.NewOrg**的新表：  
  
    ```  
    CREATE TABLE NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="to-create-a-temporary-table-named-children"></a>创建一个名为 #Children 的临时表  
  
1.  创建一个名为 **#Children** 的临时表，其中有一个名为 **Num** 的列，该列将包含每个节点的子级数：  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  添加一个索引，该索引将显著提高用于填充 **NewOrg** 表的查询的速度：  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>填充 NewOrg 表  
  
1.  递归查询禁止使用聚合进行子查询。 而是使用下列代码填充 **#Children** 表，此代码使用 [ROW_NUMBER()](/sql/t-sql/functions/row-number-transact-sql) 方法填充 **Num** 列：  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  查看 **#Children** 表。 请注意 **Num** 列包含每个经理的序号的方式。  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     `EmployeeID ManagerID Num`  
  
     `---------- --------- ---`  
  
     `1        NULL       1`  
  
     `2         1         1`  
  
     `3         1         2`  
  
     `4         2         1`  
  
     `5         2         2`  
  
     `6         2         3`  
  
     `7         3         1`  
  
     `8         3         2`  
  
     `9         4         1`  
  
     `10        4         2`  
  
3.  填充**NewOrg**表。 使用 GetRoot 和 ToString 方法将**Num**值连接到 `hierarchyid` 格式，然后使用生成的分层值更新**OrgNode**列：  
  
    ```  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   
  
    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  将 `hierarchyid` 列转换为字符格式会更易于理解。 执行下列代码查看 **NewOrg** 表中的数据，该表包含 **OrgNode** 列的两种表示形式：  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
     **LogicalNode**列将该列转换 `hierarchyid` 为表示层次结构的更易读的文本形式。 在其余的任务中，您将使用 `ToString()` 方法显示 `hierarchyid` 列的逻辑格式。  
  
5.  删除不再需要的临时表：  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
 下一个任务将创建索引以支持层次结构。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [优化 NewOrg 表](lesson-1-3-optimizing-the-neworg-table.md)  
  
  
