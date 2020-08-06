---
title: 删除程序集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
ms.openlocfilehash: 45d02cbb57459a4c1c11330446021c32dc897353
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691239"
---
# <a name="dropping-an-assembly"></a>删除程序集
  使用 CREATE ASSEMBLY 语句在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中注册的程序集可以进行删除（如果不再需要程序集所提供的功能）。 删除程序集时，将从数据库中删除程序集和它的所有关联文件，如调试文件。 若要删除程序集，可按照如下语法使用 DROP ASSEMBLY 语句：  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 DROP ASSEMBLY 不会干扰引用当前正在运行的程序集的任何代码，但是，执行 DROP ASSEMBLY 之后，任何调用程序集代码的尝试都将失败。  
  
 如果程序集被存在于该数据库中的另一个程序集引用，或者它被当前数据库中的公共语言运行时 (CLR) 函数、过程、触发器、用户定义类型 (UDT) 或用户定义聚合 (UDA) 使用，则 DROP ASSEMBLY 返回错误。 首先可使用 DROP AGGREGATE、DROP FUNCTION、DROP PROCEDURE、DROP TRIGGER 和 DROP TYPE 语句删除该程序集中所包含的所有托管数据库对象。  
  
## <a name="removing-a-udt-from-the-database"></a>从数据库中删除 UDT  
 使用 DROP TYPE 语句从当前数据库中删除 UDT。 删除了 UDT 之后，可使用 DROP ASSEMBLY 语句从数据库中删除程序集。  
  
 如果对象依赖于 UDT，则 DROP TYPE 语句将失败，如以下情况：  
  
-   数据库中的表包含使用 UDT 定义的列。  
  
-   在数据库中使用 WITH SCHEMABINDING 子句创建了使用 UDT 变量或参数的函数、存储过程或触发器。  
  
### <a name="finding-udt-dependencies"></a>查找 UDT 依赖关系  
 在执行 DROP TYPE 语句之前，首先必须删除所有依赖对象。 下面的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 查询查找使用**AdventureWorks**数据库中的 UDT 的所有列和参数。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>另请参阅  
 [管理 CLR 集成程序集](managing-clr-integration-assemblies.md)   
 [更改程序集](altering-an-assembly.md)   
 [创建程序集](creating-an-assembly.md)   
 [DROP &#40;Transact-sql&#41;](/sql/t-sql/statements/drop-aggregate-transact-sql)   
 [DROP FUNCTION (Transact-SQL)](/sql/t-sql/statements/drop-function-transact-sql)   
 [DROP PROCEDURE &#40;Transact-sql&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP TRIGGER (Transact-SQL)](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [DROP TYPE (Transact-SQL)](/sql/t-sql/statements/drop-type-transact-sql)  
  
  
