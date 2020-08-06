---
title: IntelliSense 支持的 Transact-SQL 语法
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: rothja
ms.author: jroth
ms.openlocfilehash: b3d34fc79dd7817e64b34b61083415477860ce97
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690491"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>IntelliSense 支持的 Transact-SQL 语法
  本主题介绍了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 IntelliSense 支持的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]语句和语法元素。  
  
## <a name="statements-supported-by-intellisense"></a>IntelliSense 支持的语句  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，IntelliSense 只支持最常用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 有些通用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器条件可能妨碍 IntelliSense 正常运行。 有关详细信息，请参阅 [IntelliSense 故障排除 (SQL Server Management Studio)](troubleshooting-intellisense.md)。  
  
> [!NOTE]  
>  IntelliSense 不能用于加密的数据库对象，例如加密的存储过程或用户定义函数。 参数帮助和快速信息不能用于扩展存储过程和 CLR 集成用户定义类型的参数。  
  
### <a name="select-statement"></a>SELECT 语句  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器为 SELECT 语句中的以下语法元素提供 IntelliSense 支持：  
  
|||  
|-|-|  
|SELECT|WHERE|  
|FROM|ORDER BY|  
|HAVING|UNION|  
|FOR|GROUP BY|  
|返回页首|OPTION（提示）|  
  
### <a name="additional-transact-sql-statements-that-are-supported"></a>支持的其他 Transact-SQL 语句  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器还为下表中列出的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句提供 IntelliSense 支持。  
  
|Transact-SQL 语句|支持的语法|  
|-----------------------------|----------------------|  
|[INSERT](/sql/t-sql/statements/insert-transact-sql)|所有语法， *execute_statement* 子句除外。|  
|[UPDATE](/sql/t-sql/queries/update-transact-sql)|所有语法。|  
|[DELETE](/sql/t-sql/statements/delete-transact-sql)|所有语法。|  
|[DECLARE @local_variable](/sql/t-sql/language-elements/declare-local-variable-transact-sql)|所有语法。|  
|[字符集@local_variable](/sql/t-sql/language-elements/set-local-variable-transact-sql)|所有语法。|  
|[EXECUTE](/sql/t-sql/language-elements/execute-transact-sql)|执行用户定义的存储过程、系统存储过程、用户定义函数和系统函数。|  
|[CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql)|所有语法。|  
|[CREATE VIEW](/sql/t-sql/statements/create-view-transact-sql)|所有语法。|  
|[CREATE PROCEDURE](/sql/t-sql/statements/create-procedure-transact-sql)|所有语法，以下情况除外：<br /><br /> 对 EXTERNAL NAME 子句不提供 IntelliSense 支持。<br /><br /> 在 AS 子句中，IntelliSense 仅支持本主题中列出的语句和语法。|  
|[ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql)|所有语法，以下情况除外：<br /><br /> 对 EXTERNAL NAME 子句不提供 IntelliSense 支持。<br /><br /> 在 AS 子句中，IntelliSense 仅支持本主题中列出的语句和语法。|  
|[USE](/sql/t-sql/language-elements/use-transact-sql)|所有语法。|  
  
## <a name="intellisense-in-supported-statements"></a>IntelliSense 在支持的语句中  
 当以下语法元素用于受支持的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 语句之一时， [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询编辑器中的 IntelliSense 提供支持：  
  
-   所有联接类型，包括 APPLY  
  
-   PIVOT 和 UNPIVOT  
  
-   对以下数据库对象的引用：  
  
    -   数据库和架构  
  
    -   表、视图、表值函数和表表达式  
  
    -   列  
  
    -   过程和过程参数  
  
    -   标量函数和标量表达式  
  
    -   局部变量  
  
    -   公用表表达式 (CTE)  
  
-   仅在脚本或批处理中的 CREATE 或 ALTER 语句中引用的数据库对象，但由于还未运行该脚本或批处理，数据库中不存在这些对象。 这些对象如下：  
  
    -   已在脚本或批处理中的 CREATE TABLE 或 CREATE PROCEDURE 语句中指定的表和过程。  
  
    -   对已在脚本或批处理中的 ALTER TABLE 或 ALTER PROCEDURE 语句中指定的表和过程的更改。  
  
    > [!NOTE]  
    >  在执行 CREATE VIEW 语句之前，IntelliSense 不能用于 CREATE VIEW 语句的列。  
  
 对于上文所列的元素，当它们在其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用时，不提供 IntelliSense 支持。 例如，对于在 SELECT 语句中使用的列名，提供 IntelliSense 支持，而对于在 CREATE FUNCTION 语句中使用的列，则不提供 IntelliSense 支持。  
  
## <a name="examples"></a>示例  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本或批处理中， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中的 IntelliSense 仅支持本主题中列出的语句和语法。 下面的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码示例显示 IntelliSense 支持哪些语句和语法元素。 例如，在以下批处理中，如果 `SELECT` 语句单独使用，则可以使用 IntelliSense，但是，如果 `SELECT` 包含在 `CREATE FUNCTION` 语句中，则不能使用 IntelliSense。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 该功能也适用于 CREATE PROCEDURE 或 ALTER PROCEDURE 语句中 AS 子句中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句组。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本或批处理中，IntelliSense 支持 CREATE 或 ALTER 语句中已指定的对象；但由于尚未执行这些语句，因此数据库中不存在这些对象。 例如，可在查询编辑器中输入以下代码：  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 键入 `SELECT`后，即使尚未执行脚本并且 **中尚不存在**，IntelliSense 也会列出 **“PrimaryKeyCol”**、 **“FirstNameCol”** 和 `MyTable` “LastNameCol” `MyTestDB`作为选择列表中的可能元素。  
  
  
