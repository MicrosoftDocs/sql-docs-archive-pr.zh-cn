---
title: 教程：使用证书为存储过程签名 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fe387c43431436ba5fba5bcab879584ecdad533
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591206"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>教程：使用证书为存储过程签名
  本教程说明了如何使用由 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]生成的证书对存储过程进行签名。  
  
> [!NOTE]  
>  若要运行本教程中的代码，您必须已配置混合模式安全性并且已安装 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库。 方案  
  
 如果要求对于存储过程的权限但又不希望显式授予用户那些权限，此时使用证书对存储过程进行签名是很有效的方法。 虽然可以通过其他方法完成此任务，如使用 EXECUTE AS 语句，但使用证书可以使用跟踪来查找存储过程的原始调用方。 这样可提供一种高级审核，尤其是在进行安全操作或数据定义语言 (DDL) 操作时。  
  
 您可以在 master 数据库中创建一个证书以提供服务器级别的权限，或者可以在任何用户数据库中创建一个证书以提供数据库级别的权限。 在此应用场景中，无权访问基表的用户必须访问 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中的存储过程，并且您要审核对象访问轨迹。 您将创建一个无权访问基对象的服务器和数据库用户帐户和一个有权访问表和存储过程的数据库用户帐户，而不是使用其他所有权链方法。 存储过程和第二个数据库用户帐户都将通过证书得到保护。 第二个数据库帐户将对所有对象拥有访问权限，并将向第一个数据库用户帐户授予存储过程的访问权限。  
  
 在此应用场景中，首先您将创建数据库证书、存储过程和用户，然后按以下这些步骤测试此过程：  
  
1.  配置环境。  
  
2.  创建证书。  
  
3.  创建存储过程并使用证书对存储过程进行签名。  
  
4.  使用证书创建证书帐户。  
  
5.  向证书帐户授予数据库权限。  
  
6.  显示访问权限上下文。  
  
7.  重置环境。  
  
 本示例中的每个代码块都将逐一加以说明。 若要复制完整的示例，请参阅本教程结尾部分的 [完整示例](#CompleteExample) 。  
  
## <a name="1-configure-the-environment"></a>1.配置环境  
 若要设置示例的初始上下文，请在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中打开一个新的查询，然后运行以下代码以打开 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库。 此代码将数据库上下文更改为 `AdventureWorks2012` 并创建一个新的使用密码的服务器登录名和数据库用户帐户 (`TestCreditRatingUser`)。  
  
```  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
 有关 CREATE USER 语句的详细信息，请参阅 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)。 有关 CREATE LOGIN 语句的详细信息，请参阅 [CREATE LOGIN (Transact-SQL)](/sql/t-sql/statements/create-login-transact-sql)。  
  
## <a name="2-create-a-certificate"></a>2.创建证书  
 您可以在使用 master 数据库或用户数据库作为上下文的服务器中创建证书，也可以在同时使用上述两者作为上下文的服务器中创建证书。 有多种选项用于保护证书。 有关证书的详细信息，请参阅 [CREATE CERTIFICATE (Transact-SQL)](/sql/t-sql/statements/create-certificate-transact-sql)。  
  
 运行此代码以创建数据库证书并使用密码对其进行保护。  
  
```  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3.创建存储过程并使用证书对存储过程进行签名  
 使用以下代码创建一个存储过程，该存储过程从 `Vendor` 数据库架构的 `Purchasing` 表中选择数据，并只允许信用等级为 1 的公司访问。 请注意，存储过程的第一部分显示运行该存储过程的用户帐户的上下文，它仅用于说明概念。 不必满足此要求。  
  
```  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
 运行此代码，使用密码通过数据库证书对存储过程进行签名。  
  
```  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
 有关存储过程的详细信息，请参阅[存储过程（数据库引擎）](stored-procedures/stored-procedures-database-engine.md)。  
  
 有关对存储过程签名的详细信息，请参阅 [ADD SIGNATURE (Transact-SQL)](/sql/t-sql/statements/add-signature-transact-sql)。  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4.使用证书创建证书帐户  
 运行此代码通过证书创建一个数据库用户 (`TestCreditRatingcertificateAccount`)。 该帐户没有服务器登录名，并将最终控制对基础表的访问权限。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5.向证书帐户授予数据库权限  
 运行此代码，向 `TestCreditRatingcertificateAccount` 授予对基表和存储过程的访问权限。  
  
```  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
 有关授予对象的权限的详细信息，请参阅 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)。  
  
## <a name="6-display-the-access-context"></a>6.显示访问权限上下文  
 若要显示与存储过程访问有关的权限，请运行以下代码向 `TestCreditRatingUser` 用户授予运行存储过程的权限。  
  
```  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
 接下来，运行下列代码以用于服务器的 dbo 登录名运行存储过程。 查看用户上下文信息输出结果。 输出结果所显示的上下文是具有自身权限而非作为组成员身份的 dbo 帐户。  
  
```  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 运行以下代码，使用 `EXECUTE AS` 语句将用户上下文更改为 `TestCreditRatingUser` 帐户并运行存储过程。 此时您将看到用户上下文设置为 USER MAPPED TO CERTIFICATE 上下文。  
  
```  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 此时将显示可用审核，因为您已对存储过程进行签名。  
  
> [!NOTE]  
>  使用 EXECUTE AS 在数据库中切换上下文。  
  
## <a name="7-reset-the-environment"></a>7.重置环境  
 以下代码使用 `REVERT` 语句将当前帐户的上下文返回至 dbo 并重置环境。  
  
```  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
 有关 REVERT 语句的详细信息，请参阅 [REVERT (Transact-SQL)](/sql/t-sql/statements/revert-transact-sql)。  
  
##  <a name="complete-example"></a><a name="CompleteExample"></a>完整示例  
 本部分显示完整的示例代码。  
  
```  
/* Step 1 - Open the AdventureWorks2012 database */  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
