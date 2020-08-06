---
title: 创建用户定义函数（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SCHEMABINDING clause
- schema-bound functions [SQL Server]
- user-defined functions [SQL Server], creating
- CREATE FUNCTION statement
- valid statements [SQL Server]
ms.assetid: f0d5dd10-73fd-4e05-9177-07f56552bdf7
author: rothja
ms.author: jroth
ms.openlocfilehash: 790fa1b969f933890e050311173fcde3f12c37ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590608"
---
# <a name="create-user-defined-functions-database-engine"></a>创建用户定义函数（数据库引擎）
  本主题介绍了如何通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中创建用户定义函数。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **创建用户定义函数：**  
  
     [创建标量函数](#Scalar)  
  
     [创建表值函数](#TVF)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   用户定义函数不能用于执行修改数据库状态的操作。  
  
-   用户定义函数不能包含将表作为其目标的 OUTPUT INTO 子句。  
  
-   用户定义函数不能返回多个结果集。 如果您需要返回多个结果集，请使用存储过程。  
  
-   在用户定义函数中，错误处理受限制。 UDF 不支持 TRY .。。CATCH @ERROR 或 RAISERROR。  
  
-   用户定义函数不能调用存储过程，但是可调用扩展存储过程。  
  
-   用户定义函数不能使用动态 SQL 或临时表。 允许表变量。  
  
-   在用户定义函数中不允许 SET 语句。  
  
-   不允许 FOR XML 子句  
  
-   用户定义函数可以嵌套；也就是说，用户定义函数可相互调用。 被调用函数开始执行时，嵌套级别将增加；被调用函数执行结束后，嵌套级别将减少。 用户定义函数的嵌套级别最多可达 32 级。 如果超出最大嵌套级别数，整个调用函数链将失败。 从 Transact-SQL 用户定义函数对托管代码的任何引用都将根据 32 级嵌套限制计入一个级别。 从托管代码内部调用的方法不根据此限制进行计数。  
  
-   下列 Service Broker 语句不能包含在 Transact-SQL 用户定义函数的定义中：  
  
    -   BEGIN DIALOG CONVERSATION  
  
    -   END CONVERSATION  
  
    -   GET CONVERSATION GROUP  
  
    -   MOVE CONVERSATION  
  
    -   RECEIVE  
  
    -   SEND  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要在数据库中具有 CREATE FUNCTION 权限，并对创建函数时所在的架构具有 ALTER 权限。 如果函数指定用户定义类型，则需要对该类型具有 EXECUTE 权限。  
  
##  <a name="scalar-functions"></a><a name="Scalar"></a>标量函数  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中创建一个多语句标量函数。 此函数输入一个值 `ProductID`，而返回一个单个数据值（指定库存产品的聚合量）。  
  
```  
IF OBJECT_ID (N'dbo.ufnGetInventoryStock', N'FN') IS NOT NULL  
    DROP FUNCTION ufnGetInventoryStock;  
GO  
CREATE FUNCTION dbo.ufnGetInventoryStock(@ProductID int)  
RETURNS int   
AS   
-- Returns the stock level for the product.  
BEGIN  
    DECLARE @ret int;  
    SELECT @ret = SUM(p.Quantity)   
    FROM Production.ProductInventory p   
    WHERE p.ProductID = @ProductID   
        AND p.LocationID = '6';  
     IF (@ret IS NULL)   
        SET @ret = 0;  
    RETURN @ret;  
END;  
GO  
  
```  
  
 下例使用 `ufnGetInventoryStock` 函数返回 `ProductModelID` 介于 75 和 80 之间的产品的当前库存量。  
  
```  
SELECT ProductModelID, Name, dbo.ufnGetInventoryStock(ProductID)AS CurrentSupply  
FROM Production.Product  
WHERE ProductModelID BETWEEN 75 and 80;  
  
```  
  
##  <a name="table-valued-functions"></a><a name="TVF"></a>表值函数  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中创建内联表值函数。 此函数的输入参数为客户（商店）ID，而返回 `ProductID`、 `Name`以及 `YTD Total` （销售到商店的每种产品的本年度节截止到现在的销售总额）列。  
  
```  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
  
```  
  
 下面的示例调用此函数并指定客户 ID 为 602。  
  
```  
SELECT * FROM Sales.ufn_SalesByStore (602);  
  
```  
  
 下面的示例在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中创建表值函数。 此函数具有一个输入参数 `EmployeeID` ，它返回直接或间接向指定员工报告的所有员工的列表。 然后在指定雇员 ID 109 的情况下调用此函数。  
  
```  
IF OBJECT_ID (N'dbo.ufn_FindReports', N'TF') IS NOT NULL  
    DROP FUNCTION dbo.ufn_FindReports;  
GO  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0 -- Get the initial list of Employees for Manager n  
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1 -- Join recursive member to anchor  
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [用户定义函数](user-defined-functions.md)   
 [CREATE FUNCTION (Transact-SQL)](/sql/t-sql/statements/create-function-transact-sql)  
  
  
