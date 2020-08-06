---
title: 创建索引视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
author: stevestein
ms.author: sstein
ms.openlocfilehash: d33ff37caca04f46edd6ad92d0686713829bb270
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577462"
---
# <a name="create-indexed-views"></a>创建索引视图
  本主题将说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建索引视图。 对视图创建的第一个索引必须是唯一聚集索引。 创建唯一聚集索引后，可以创建更多非聚集索引。 为视图创建唯一聚集索引可以提高查询性能，因为视图在数据库中的存储方式与具有聚集索引的表的存储方式相同。 查询优化器可使用索引视图加快执行查询的速度。 要使优化器考虑将该视图作为替换，并不需要在查询中引用该视图。  
  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
 创建索引视图需要执行下列步骤并且这些步骤对于成功实现索引视图而言非常重要：  
  
1.  验证是否视图中将引用的所有现有表的 SET 选项都正确。  
  
2.  在创建任意表和视图之前，验证会话的 SET 选项设置是否正确。  
  
3.  验证视图定义是否为确定性的。  
  
4.  使用 WITH SCHEMABINDING 选项创建视图。  
  
5.  为视图创建唯一的聚集索引。  
  
###  <a name="required-set-options-for-indexed-views"></a><a name="Restrictions"></a> 索引视图所需的 SET 选项  
 如果执行查询时启用不同的 SET 选项，则在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中对同一表达式求值会产生不同结果。 例如，将 SET 选项 CONCAT_NULL_YIELDS_NULL 设置为 ON 后，表达式 **'** abc **'** + NULL 会返回值 NULL。 但将 CONCAT_NULL_YIEDS_NULL 设置为 OFF 后，同一表达式会生成 **'** abc **'**。  
  
 为了确保能够正确维护视图并返回一致结果，索引视图需要多个 SET 选项具有固定值。 如果出现下列情况，则必须将下表中的 SET 选项设置为**RequiredValue**列中显示的值：  
  
-   创建视图和视图上的后续索引。  
  
-   在创建表时，在视图中引用的基表。  
  
-   对构成该索引视图的任何表执行了任何插入、更新或删除操作。 此要求包括大容量复制、复制和分布式查询等操作。  
  
-   查询优化器使用该索引视图生成查询计划。  
  
    |SET 选项|所需的值|默认服务器值|默认<br /><br /> OLE DB 和 ODBC 值|默认<br /><br /> DB-Library 值|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *将 ANSI_WARNINGS 设置为 ON 隐式将 ARITHABORT 设置为 ON。  
  
 如果使用的是 OLE DB 或 ODBC 服务器连接，则唯一必须要修改的值是 ARITHABORT 设置。 必须使用 **sp_configure** 在服务器级别或使用 SET 命令从应用程序中正确设置所有 DB-Library 值。  
  
> [!IMPORTANT]  
>  极力建议在服务器的任一数据库中创建计算列的第一个索引视图或索引后，尽早在服务器范围内将 ARITHABORT 用户选项设置为 ON。  
  
### <a name="deterministic-views"></a>确定性视图  
 索引视图的定义必须是确定性的。 如果选择列表中的所有表达式、WHERE 和 GROUP BY 子句都具有确定性，则视图也具有确定性。 在使用特定的输入值集对确定性表达式求值时，它们始终返回相同的结果。 只有确定性函数可以加入确定性表达式。 例如，DATEADD 函数是确定性函数，因为对于其三个参数的任何给定参数值集它总是返回相同的结果。 GETDATE 不是确定性函数，因为总是使用相同的参数调用它，而它在每次执行时返回结果都不同。  
  
 要确定视图列是否为确定性列，请使用 **COLUMNPROPERTY** 函数的 [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) 属性。 使用 COLUMNPROPERTY 函数的 **IsPrecise** 属性确定具有架构绑定的视图中的确定性列是否为精确列。 如果为 TRUE，则 COLUMNPROPERTY 返回 1；如果为 FALSE，则返回 0；如果输入无效，则返回 NULL。 这意味着该列不是确定性列，也不是精确列。  
  
 即使是确定性表达式，如果其中包含浮点表达式，则准确结果也会取决于处理器体系结构或微代码的版本。 为了确保数据完整性，此类表达式只能作为索引视图的非键列加入。 不包含浮点表达式的确定性表达式称为精确表达式。 只有精确的确定性表达式才能加入键列，并包含在索引视图的 WHERE 或 GROUP BY 子句中。  
  
### <a name="additional-requirements"></a>其他要求  
 除对 SET 选项和确定性函数的要求外，还必须满足下列要求：  
  
-   执行 CREATE INDEX 的用户必须是视图所有者。  
  
-   创建索引时，IGNORE_DUP_KEY 选项必须设置为 OFF（默认设置）。  
  
-   在视图定义中，必须使用两部分名称（即 _schema_ **.** _tablename_ ）来引用表。  
  
-   必须已使用 WITH SCHEMABINDING 选项创建了在视图中引用的用户定义函数。  
  
-   视图中引用的任何用户定义函数都必须由两部分组成的名称（_架构_）引用 **。**_函数_。  
  
-   用户定义函数的数据访问属性必须为 NO SQL，外部访问属性必须是 NO。  
  
-   公共语言运行时 (CLR) 功能可以出现在视图的选择列表中，但不能作为聚集索引键定义的一部分。 CLR 函数不能出现在视图的 WHERE 子句中或视图中的 JOIN 运算的 ON 子句中。  
  
-   在视图定义中使用的 CLR 函数和 CLR 用户定义类型方法必须具有下表所示的属性设置。  
  
    |properties|注意|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|必须显式声明为 Microsoft .NET Framework 方法的属性。|  
    |PRECISE = TRUE|必须显式声明为 .NET Framework 方法的属性。|  
    |DATA ACCESS = NO SQL|通过将 DataAccess 属性设置为 DataAccessKind.None 并将 SystemDataAccess 属性设置为 SystemDataAccessKind.None 来确定。|  
    |EXTERNAL ACCESS = NO|对于 CLR 例程，该属性的默认设置为 NO。|  
  
-   必须使用 WITH SCHEMABINDING 选项创建视图。  
  
-   视图必须仅引用与视图位于同一数据库中的基表。 视图无法引用其他视图。  
  
-   视图定义中的 SELECT 语句不能包含下列 Transact-SQL 元素：  
  
    ||||  
    |-|-|-|  
    |COUNT|ROWSET 函数（OPENDATASOURCE、OPENQUERY、OPENROWSET 和 OPENXML）|OUTER 联接（LEFT、RIGHT 或 FULL）|  
    |派生表（通过在 FROM 子句中指定 SELECT 语句来定义）|自联接|通过使用 SELECT \* 或 SELECT *table_name*来指定列。*|  
    |DISTINCT|STDEV、STDEVP、VAR、VARP 或 AVG|公用表表达式 (CTE)|  
    |`float`\*、 `text` 、 `ntext` 、 `image` 、 `XML` 或 `filestream` 列|子查询|包括排名或聚合开窗函数的 OVER 子句|  
    |全文谓词（CONTAIN、FREETEXT）|引用可为 Null 的表达式的 SUM 函数|ORDER BY|  
    |CLR 用户定义聚合函数|TOP|CUBE、ROLLUP 或 GROUPING SETS 运算符|  
    |MIN、MAX|UNION、EXCEPT 或 INTERSECT 运算符|TABLESAMPLE|  
    |表变量|OUTER APPLY 或 CROSS APPLY|PIVOT、UNPIVOT|  
    |稀疏列集|内联或多语句表值函数|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*索引视图可以包含 `float` 列，但聚集索引键中不能包含此类列。  
  
-   如果存在 GROUP BY，则 VIEW 定义必须包含 COUNT_BIG(*)，并且不得包含 HAVING。 这些 GROUP BY 限制仅适用于索引视图定义。 即使一个索引视图不满足这些 GROUP BY 限制，查询也可以在其执行计划中使用该视图。  
  
-   如果视图定义包含 GROUP BY 子句，则唯一聚集索引的键只能引用 GROUP BY 子句中指定的列。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
 引用索引视图中的 `datetime` 和 `smalldatetime` 字符串文字时，建议使用确定性日期格式样式将文字显式转换为所需日期类型。 有关确定性日期格式样式的列表，请参阅 [CAST 与 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)。 将字符串隐式转换为 `datetime` 或 `smalldatetime` 所涉及的表达式被视为具有不确定性。 这是因为结果取决于服务器会话的 LANGUAGE 和 DATEFORMAT 设置。 例如，表达式 `CONVERT (datetime, '30 listopad 1996', 113)` 的结果取决于 LANGUAGE 设置，因为字符串`listopad`在不同语言中表示不同的月份。 同样，在 `DATEADD(mm,3,'2000-12-01')`表达式中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 基于 DATEFORMAT 设置解释 `'2000-12-01'` 字符串。  
  
 非 Unicode 字符数据在排序规则间的隐式转换也被视为具有不确定性。  
  
###  <a name="considerations"></a><a name="Considerations"></a> 注意事项  
 索引视图中列的 **large_value_types_out_of_row** 选项的设置继承的是基表中相应列的设置。 此值是使用 [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql)设置的。 从表达式组成的列的默认设置为 0。 这意味着大值类型存储在行内。  
  
 可以对已分区表创建索引视图，并可以由其自行分区。  
  
 若要防止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用索引视图，请在查询中包含 OPTION (EXPAND VIEWS) 提示。 此外，任何所列选项设置不正确均会阻止优化器使用视图上的索引。 有关 OPTION (EXPAND VIEWS) 提示的详细信息，请参阅 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)。  
  
 若删除视图，该视图的所有索引也将被删除。 若删除聚集索引，视图的所有非聚集索引和自动创建的统计信息也将被删除。 视图中用户创建的统计信息受到维护。 非聚集索引可以分别删除。 删除视图的聚集索引将删除存储的结果集，并且优化器将重新像处理标准视图那样处理视图。  
  
 可以禁用表和视图的索引。 禁用表的聚集索引时，与该表关联的视图的索引也将被禁用。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求在数据库中具有 CREATE VIEW 权限，并具有在其中创建视图的架构的 ALTER 权限。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>创建索引视图  
  
1.  在 **“对象资源管理器”** 中，连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 该示例将创建一个视图并为该视图创建索引。 包含两个使用该索引视图的查询。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 有关详细信息，请参阅 [CREATE VIEW (Transact-SQL)](/sql/t-sql/statements/create-view-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE INDEX (Transact-SQL)](/sql/t-sql/statements/create-index-transact-sql)   
 [SET ANSI_NULLS (Transact-SQL)](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING (Transact-SQL)](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS (Transact-SQL)](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [SET ARITHABORT (Transact-SQL)](/sql/t-sql/statements/set-arithabort-transact-sql)   
 [SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [SET NUMERIC_ROUNDABORT (Transact-SQL)](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)   
 [SET QUOTED_IDENTIFIER (Transact-SQL)](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
  
