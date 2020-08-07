---
title: 教程：所有权链和上下文切换 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e9072a68dd3179e5900fda06d4fea58b484a37e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580102"
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
  本教程使用一个应用场景说明 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安全性概念，其中包括所有权链和用户上下文切换。  
  
> [!NOTE]  
>  若要运行本教程中的代码，您必须已配置混合模式安全性并且已安装 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库。 有关混合模式安全性的详细信息，请参阅 [选择身份验证模式](security/choose-an-authentication-mode.md)。  
  
## <a name="scenario"></a>场景  
 在此应用场景中，两个用户需要帐户访问存储在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中的采购订单数据。 要求如下：  
  
-   第一个帐户 (TestManagerUser) 必须能够查看每个采购订单中的所有详细信息。  
  
-   第二个帐户 (TestEmployeeUser) 必须能够根据采购订单号，查看已收到部分货物的项的采购订单号、订单日期、发货日期、产品 ID 号以及每个采购订单中已定购和已收到的项。  
  
-   所有其他帐户必须保留当前的权限。  
  
 若要满足本应用场景的要求，此示例分为四个部分来说明所有权链和上下文切换的概念：  
  
1.  配置环境。  
  
2.  创建存储过程以按采购订单访问数据。  
  
3.  通过存储过程访问数据。  
  
4.  重置环境。  
  
 本示例中的每个代码块都将逐一加以说明。 若要复制完整的示例，请参阅本教程结尾部分的 [完整示例](#CompleteExample) 。  
  
## <a name="1-configure-the-environment"></a>1.配置环境  
 使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 和以下代码打开 `AdventureWorks2012` 数据库，然后使用 `CURRENT_USER` [!INCLUDE[tsql](../includes/tsql-md.md)] 语句检查 dbo 用户是否显示为上下文。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
 有关 CURRENT_USER 语句的详细信息，请参阅 [CURRENT_USER (Transact-SQL)](/sql/t-sql/functions/current-user-transact-sql)。  
  
 使用此代码以使 dbo 用户在服务器及 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中创建两个用户。  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
 有关 CREATE USER 语句的详细信息，请参阅 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)。 有关 CREATE LOGIN 语句的详细信息，请参阅 [CREATE LOGIN (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql)。  
  
 使用以下代码将 `Purchasing` 架构的所有权更改为 `TestManagerUser` 帐户。 这样将允许该帐户对其包含的对象使用所有数据操作语言 (DML) 语句访问权限（如 `SELECT` 和 `INSERT` 权限）。 `TestManagerUser` 授予创建存储过程的能力。  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
 有关 GRANT 语句的详细信息，请参阅 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)。 有关存储过程的详细信息，请参阅[存储过程（数据库引擎）](stored-procedures/stored-procedures-database-engine.md)。 有关所有权限的海报 [!INCLUDE[ssDE](../includes/ssde-md.md)] ，请参阅 [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf) 。  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2.创建存储过程以访问数据  
 若要切换数据库内的上下文，请使用 EXECUTE AS 语句。 EXECUTE AS 需要 IMPERSONATE 权限。  
  
 使用以下代码中的 `EXECUTE AS` 语句将上下文更改为 `TestManagerUser` ，并创建一个仅显示 `TestEmployeeUser`需要的数据的存储过程。 为了满足这些要求，存储过程接受一个代表采购订单号的变量并且不显示财务信息，WHERE 子句则将结果限制为部分货物。  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
 当前 `TestEmployeeUser` 对任何数据库对象都没有访问权限。 以下代码（仍位于 `TestManagerUser` 上下文中）授予用户帐户通过存储过程查询基表信息的能力。  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
 即使没有显式指定架构，存储过程也是 `Purchasing` 架构的一部分，因为默认情况下系统将把 `TestManagerUser` 分配给 `Purchasing` 架构。 您可以使用系统目录信息查找对象，如以下代码所示。  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
 完成本部分示例之后，代码使用 `REVERT` 语句将上下文切换回 dbo。  
  
```  
REVERT;  
GO  
```  
  
 有关 REVERT 语句的详细信息，请参阅 [REVERT (Transact-SQL)](/sql/t-sql/statements/revert-transact-sql)。  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3.通过存储过程访问数据  
 `TestEmployeeUser` 除了拥有一个登录名以及分配给公共数据库角色的权限之外，对 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库对象没有其他权限。 如果 `TestEmployeeUser` 试图访问基表，以下代码在将返回一个错误。  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
 因为在最后一部分中创建的存储过程引用的对象由 `TestManagerUser` 凭借 `Purchasing` 架构所有权而拥有，因此 `TestEmployeeUser` 可以通过此存储过程访问基表。 以下代码仍使用 `TestEmployeeUser` 上下文将采购订单 952 作为参数传递。  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4.重置环境  
 以下代码使用 `REVERT` 命令将当前帐户的上下文返回至 `dbo`，然后重置环境。  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
##  <a name="complete-example"></a><a name="CompleteExample"></a>完整示例  
 本部分显示完整的示例代码。  
  
> [!NOTE]  
>  此代码不包括两个说明 `TestEmployeeUser` 无法从基表中进行选择的预期错误。  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
