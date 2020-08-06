---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 74c152404cf2d3710bbe98b29da7a96d86f58859
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688937"
---
# <a name="mssqlserver_1505"></a>MSSQLSERVER_1505
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1505|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DUP_KEY|  
|消息正文|因为发现对象名称“%.\*ls”和索引名称“%.\*ls”有重复的键，所以 CREATE UNIQUE INDEX 已终止。  重复的键值为 %ls。|  
  
## <a name="explanation"></a>说明  
 如果表中有多行包含指定的重复值，那么，当您尝试创建唯一索引时，会发生此错误。 当您创建索引并指定 UNIQUE 关键字时，或者当您创建 UNIQUE 约束时，会创建唯一索引。 对于表内的任何行，索引或约束中所定义的列中都不能有重复值。  
  
 请考虑以下 **Employee** 表中的数据：  
  
|LastName|FirstName|JobTitle|HireDate|  
|--------------|---------------|--------------|--------------|  
|Walters|Rob|Senior Tool Designer|2004-11-19|  
|Brown|Kevin|Marketing Assistant|Null|  
|Brown|Jo|Design Engineer|Null|  
|Walters|Rob|Tool Designer|2001-08-09|  
  
 由于行中存在重复值，因此不能针对 **LastName** 列或 **LastName** 列与 **FirstName** 列的组合创建唯一索引。  
  
 **HireDate** 列中可能存在不太明显的唯一性冲突。 为了利于创建索引，NULL 值与 NULL 值的比较结果为相等。 因此，如果不止一行中的键值为 NULL，则不能创建唯一索引或唯一约束。 有了上面的数据，不能针对 **HireDate** 列或 **LastName** 列与 **HireDate** 列的组合创建唯一索引。  
  
 错误消息 1505 返回第一个违反唯一性约束的行。 该表中可能存在其他重复行。 若要查找所有的重复行，请查询指定的表，然后使用 GROUP BY 和 HAVING 子句报告重复行。 例如，下面的查询返回 **Employee** 表中具有重复名字和姓氏的行：  
  
 从 dbo 中选择 "LastName"、"名字"、"计数" (\*) 。员工组按 LastName，名字 \*)  (> 1;  
  
## <a name="user-action"></a>用户操作  
 请考虑以下解决方案。  
  
-   在索引或约束定义中添加或删除列以创建唯一组合。 在前面的例子中，向索引或约束定义中添加 **MiddleName** 列可以解决重复问题。  
  
-   当为唯一索引或唯一约束选择列时，请选择那些定义为 NOT NULL 的列。 这样，当多行的键值包含 NULL 时，就消除了导致唯一性冲突的可能性。  
  
-   如果重复值是因数据输入错误而引起的，则可以先手动更正数据，然后创建索引或约束。 有关删除表中重复行的信息，请参阅知识库文章 139444：[如何从 SQL Server 中的表中删除重复行](https://support.microsoft.com/kb/139444)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)   
 [创建唯一索引](../indexes/indexes.md)   
 [创建唯一约束](../tables/create-unique-constraints.md)  
  
  
