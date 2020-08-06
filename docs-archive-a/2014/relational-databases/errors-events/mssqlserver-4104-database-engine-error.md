---
title: MSSQLSERVER_4104 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cbbc28a3e15af6fdc8fd44633ccbdfc46e49149d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589130"
---
# <a name="mssqlserver_4104"></a>MSSQLSERVER_4104
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|4104|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|ALG_MULTI_ID_BAD|  
|消息正文|无法绑定由多个部分组成的标识符 "%.*ls"。|  
  
## <a name="explanation"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中实体的名称称为其“标识符”。 在引用实体（例如在查询中指定列名和表名）时可以使用标识符。 由多个部分组成的标识符包含一个或多个作为标识符前缀的限定符。 例如，表标识符可能以诸如包含表的数据库和架构的名称之类的限定符作为前缀，而列标识符可能以诸如表名称或表别名之类的限定符作为前缀。  
  
 错误 4104 表示无法将指定的由多个部分组成的标识符映射到现有实体。 在以下情况下可能会返回此错误：  
  
-   作为列名称前缀提供的限定符与查询中使用的任何表名或别名均不对应。  
  
     例如，下面的语句使用表别名 (`Dept`) 作为列前缀，但是此表别名未在 FROM 子句中引用。  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
     在下面的语句中，在属于两个表之间的 JOIN 条件的 WHERE 子句中指定了由多个部分组成的列标识符 `TableB.KeyCol`，但是 `TableB` 未在查询中显式引用。  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   在 FROM 子句中提供了表的别名，但为列提供的相应限定符却是表名称。 例如，下面的语句使用表名称 `Department` 作为列前缀，但是，在 FROM 子句中引用的是表别名 (`Dept`)。  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
     使用别名时，不能在语句中的其他地方使用表名称。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法确定由多个部分组成的标识符是指由表作为前缀的列，还是指由列作为前缀的 CLR 用户定义数据类型 (UDT) 的属性。 出现这种情况的原因是：UDT 列的属性是通过在列名称和属性名称之间使用句号分隔符 (.) 引用的，而这与用表名称作为列名称前缀的方式相同。 以下示例创建两个表：`a` 和 `b`。 表 `b` 包含列 `a`，此列使用 CLR UDT `dbo.myudt2` 作为其数据类型。 SELECT 语句包含由多个部分组成的标识符 `a.c2`。  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
     假定 UDT `myudt2` 不具有名为 `c2` 的属性，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将无法确定标识符 `a.c2` 是指表 `a` 中的列 `c2`，还是指表 `b` 中的列 `a`、属性 `c2`。  
  
## <a name="user-action"></a>用户操作  
  
-   使列前缀与在查询的 FROM 子句中指定的表名或别名相匹配。 如果在 FROM 子句中为表名称定义了别名，则只能将此别名用作与该表关联的列的限定符。  
  
     上面引用 `HumanResources.Department` 表的语句可以进行如下更正：  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   确保在查询中指定所有表，并确保正确地指定表之间的 JOIN 条件。 上面的 DELETE 语句可以进行如下更正：  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
     上面 `TableA` 的 SELECT 语句可以进行如下更正：  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
     或  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   为标识符使用明确定义的唯一名称。 这样做可以使您的代码更易于理解和维护，并可以将不明确引用多个实体的风险降至最低。  
  
## <a name="see-also"></a>另请参阅  
 [MSSQLSERVER_107](mssqlserver-107-database-engine-error.md)   
 [数据库标识符](../databases/database-identifiers.md)  
  
  
