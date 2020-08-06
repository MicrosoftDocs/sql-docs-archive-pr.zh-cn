---
title: OLE 自动化脚本示例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- OLE Automation [SQL Server], examples
ms.assetid: e59f75a9-ed41-4f12-888e-ffc57f9b3882
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3893bc337ad4e274967b6b06838c9e5bdb47277e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591856"
---
# <a name="ole-automation-sample-script"></a><span data-ttu-id="10829-102">OLE 自动化脚本示例</span><span class="sxs-lookup"><span data-stu-id="10829-102">OLE Automation Sample Script</span></span>
  <span data-ttu-id="10829-103">本主题包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句批处理的一个示例，它使用 OLE 自动化存储过程在本地 [!INCLUDE[ssDE](../../includes/ssde-md.md)]实例中创建和使用 SQL-DMO SQLServer 对象。</span><span class="sxs-lookup"><span data-stu-id="10829-103">This topic contains an example of a [!INCLUDE[tsql](../../includes/tsql-md.md)] statement batch that uses the OLE Automation stored procedures to create and use an SQL-DMO SQLServer object in the local instance of the [!INCLUDE[ssDE](../../includes/ssde-md.md)].</span></span> <span data-ttu-id="10829-104">部分代码在 OLE 自动化系统存储过程的引用主题中用作示例。</span><span class="sxs-lookup"><span data-stu-id="10829-104">Parts of the code are used as examples in the reference topics for the OLE Automation system stored procedures.</span></span>  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @Object int;  
DECLARE @HR int;  
DECLARE @Property nvarchar(255);  
DECLARE @Return nvarchar(255);  
DECLARE @Source nvarchar(255), @Desc nvarchar(255);  
  
-- Create a SQLServer object.  
SET NOCOUNT ON;  
  
-- First, create the object.  
EXEC @HR = sp_OACreate N'SQLDMO.SQLServer',  
    @Object OUT;  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    GOTO END_ROUTINE  
END  
ELSE  
-- A DMO.SQLServer object has been successfully created.  
BEGIN  
    -- Specify Windows Authentication for connections.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'LoginSecure',  
        N'TRUE';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Set a property.  
    EXEC @HR = sp_OASetProperty @Object,  
        N'HostName',  
        N'SampleScript';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property using an output parameter.  
    EXEC @HR = sp_OAGetProperty @Object, N'HostName', @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Get a property using a result set.  
    EXEC @HR = sp_OAGetProperty @Object,  
        N'HostName';  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Get a property by calling the method.  
    EXEC @HR = sp_OAMethod @Object,  
        N'HostName',  
        @Property OUT;  
    IF @HR <> 0   
        GOTO CLEANUP  
    ELSE  
        PRINT @Property;  
  
    -- Call the connect method.  
    -- SECURITY NOTE - When possible, use Windows Authentication.  
    EXEC @HR = sp_OAMethod @Object,  
        N'Connect',  
        NULL,  
        N'localhost',  
        NULL,  
        NULL;  
    IF @HR <> 0 GOTO CLEANUP  
  
    -- Call a method that returns a value.  
    EXEC @HR = sp_OAMethod @Object,  
        N'VerifyConnection',  
        @Return OUT;  
    IF @HR <> 0  
        GOTO CLEANUP  
    ELSE  
        PRINT @Return;  
END  
  
CLEANUP:  
-- Check whether an error occurred.  
IF @HR <> 0  
BEGIN  
    -- Report the error.  
    EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
    SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
END  
  
-- Destroy the object.  
BEGIN  
    EXEC @HR = sp_OADestroy @Object;  
    -- Check if an error occurred.  
    IF @HR <> 0   
    BEGIN  
        -- Report the error.  
        EXEC sp_OAGetErrorInfo @Object,  
        @Source OUT,  
        @Desc OUT;  
        SELECT HR = convert(varbinary(4),@HR),  
        Source=@Source,  
        Description=@Desc;  
    END  
END  
  
END_ROUTINE:  
RETURN;  
GO  
```  
  
## <a name="related-content"></a><span data-ttu-id="10829-105">相关内容</span><span class="sxs-lookup"><span data-stu-id="10829-105">Related Content</span></span>  
 [<span data-ttu-id="10829-106">Transact-SQL 中的 OLE 自动化对象</span><span class="sxs-lookup"><span data-stu-id="10829-106">OLE Automation Objects in Transact-SQL</span></span>](ole-automation-objects-in-transact-sql.md)  
  
 [<span data-ttu-id="10829-107">sp_OACreate (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="10829-107">sp_OACreate &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-oacreate-transact-sql)  
  
 [<span data-ttu-id="10829-108">sp_OAGetProperty (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="10829-108">sp_OAGetProperty &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql)  
  
 [<span data-ttu-id="10829-109">sp_OASetProperty (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="10829-109">sp_OASetProperty &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql)  
  
 [<span data-ttu-id="10829-110">sp_OAMethod (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="10829-110">sp_OAMethod &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-oamethod-transact-sql)  
  
 [<span data-ttu-id="10829-111">sp_OADestroy (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="10829-111">sp_OADestroy &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-oadestroy-transact-sql)  
  
  
