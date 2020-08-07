---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e0142cd53006609e9274972e4f5964132f5982c2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589664"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|137|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|P_SCALAR_VAR_NOTFOUND|  
|消息正文|必须声明标量变量 "%.*ls"。|  
  
## <a name="explanation"></a>说明  
 如果未首先声明某个变量就在 SQL 脚本中使用它，则会出现此错误。 下面的示例对 SET 和 SELECT 语句都返回错误137，因为未 **@mycol** 声明。  
  
 SET @mycol = 'ContactName';  
  
 SELECT @mycol;  
  
 之所以发生此错误，一个更为复杂的原因就是使用在 EXECUTE 语句外部声明的变量。 例如， **@mycol** select 语句中指定的变量是 select 语句的局部变量，因此它位于 EXECUTE 语句外部。  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>用户操作  
 确认先声明 SQL 脚本中所使用的任何变量，然后再将其用在脚本中的其他位置。  
  
 重新编写该脚本，以便不在 EXECUTE 语句中引用在其外部声明的变量。 例如：  
  
 USE AdventureWorks2012;  
  
 GO  
  
 DECLARE @mycol nvarchar(20);  
  
 SET @mycol = 'Name';  
  
 EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>另请参阅  
 [EXECUTE (Transact-SQL)](/sql/t-sql/language-elements/execute-transact-sql)   
 [SET 语句 (Transact-SQL)](/sql/t-sql/statements/set-statements-transact-sql)   
 [DECLARE @local_variable (Transact-SQL)](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
  
