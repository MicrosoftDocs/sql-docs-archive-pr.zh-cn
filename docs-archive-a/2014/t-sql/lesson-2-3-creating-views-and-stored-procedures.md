---
title: 创建视图和存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 76f6ecec446536191e8be4b05547ba5fd44c9d8d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682575"
---
# <a name="creating-views-and-stored-procedures"></a>创建视图和存储过程
  既然 Mary 可以访问 **TestData** 数据库，你可能希望创建一些数据库对象（如视图和存储过程），再将它们的访问权限授予 Mary。 视图是存储的 SELECT 语句，而存储过程是以批处理方式执行的一条或多条 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。  
  
 视图像表那样进行查询，但不接受参数。 存储过程比视图更复杂。 存储过程可以同时具有输入参数和输出参数，并可以包括控制代码流的语句，如 IF 和 WHILE 语句。 将存储过程用于数据库中的所有重复操作，是一个良好的编程做法。  
  
 在此示例中，你将使用 CREATE VIEW 创建一个视图，该视图仅选择 **Products** 表中的两列。 然后，您将使用 CREATE PROCEDURE 创建一个存储过程，该存储过程接受价格参数，并仅返回价格小于指定参数值的那些产品。  
  
### <a name="to-create-a-view"></a>创建视图  
  
1.  执行以下语句创建一个非常简单的视图，该视图执行 Select 语句，并将产品的名称和价格返回给用户。  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>测试视图  
  
1.  视图的处理方式与表类似。 使用 `SELECT` 语句访问视图。  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>创建存储过程  
  
1.  以下语句创建一个名为 `pr_Names`的存储过程，接受名为 `@VarPrice` 、数据类型为 `money`的输入参数。 该存储过程打印与输入参数（已从 `Products less than` 数据类型更改为 `money` 字符数据类型）串联的语句 `varchar(10)` 。 然后，该存储过程对视图执行 `SELECT` 语句，将输入参数作为 `WHERE` 子句的一部分进行传递。 这将返回价格小于输入参数值的所有产品。  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>测试存储过程  
  
1.  若要测试存储过程，请键入并执行以下语句。 存储过程应该返回在第 1 课中向 `Products` 表中输入的、其价格小于 `10.00`的两个产品的名称。  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [授予访问数据库对象的权限](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>另请参阅  
 [CREATE VIEW (Transact-SQL)](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE (Transact-SQL)](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
