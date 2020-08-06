---
title: 数据库属性（“选项”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
ms.openlocfilehash: e856e820719054ad1f01fe0e0306aa278d62ec2c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689430"
---
# <a name="database-properties-options-page"></a>数据库属性（“选项”页）
  使用此页可以查看或修改所选数据库的选项。 有关此页上可用选项的详细信息，请参阅[ALTER DATABASE SET options &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
## <a name="page-header"></a>页眉  
 **排序规则**  
 通过从列表中进行选择来指定数据库的排序规则。 有关详细信息，请参阅 [Set or Change the Database Collation](../collations/set-or-change-the-database-collation.md)。  
  
 **恢复模式**  
 指定下列模式之一来恢复数据库：**完整**、**大容量日志**或**简单**。 有关恢复模式的详细信息，请参阅[恢复模式 (SQL Server)](../backup-restore/recovery-models-sql-server.md)。  
  
 **兼容性级别**  
 指定数据库支持的最新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 可能的值有  **SQL Server 2014 (120)**、  **SQL Server 2012 (110)** 和 **SQL Server 2008 (100)**。 当 SQL Server 2005 数据库升级到 SQL Server 2014 时，该数据库的兼容级别将从 90 更改为 100。  在 SQL Server 2014 中不支持 90 兼容级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
 **包含类型**  
 指定无或部分以便指定这是否为包含数据库。 有关包含的数据库的详细信息，请参阅 [Contained Databases](contained-databases.md)。 服务器属性 **“启用包含的数据库”** 必须首先设置为 **TRUE** ，然后才能将某个数据库配置为包含数据库。  
  
> [!IMPORTANT]  
>  启用部分包含数据库会将对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的访问控制委托给该数据库的所有者。 有关详细信息，请参阅 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)。  
  
## <a name="automatic"></a>自动  
 **自动关闭**  
 指定在上一个用户退出后，数据库是否完全关闭并释放资源。 可能的值为 `True` 和 `False`。 如果为 `True`，将完全关闭数据库，并在最后一个用户注销后释放该数据库的资源。  
  
 自动创建增量统计信息  
 指定在创建每个分区的统计信息时是否使用增量选项。 有关增量统计信息的信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自动创建统计信息**  
 指定数据库是否自动创建缺少的优化统计信息。 可能的值为 `True` 和 `False`。 如果为 `True`，将在优化过程中自动生成优化查询所需的任何缺少的统计信息。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自动收缩**  
 指定数据库文件是否可定期收缩。 可能的值为 `True` 和 `False`。 有关详细信息，请参阅 [Shrink a Database](shrink-a-database.md)。  
  
 **自动更新统计信息**  
 指定数据库是否自动更新过期的优化统计信息。 可能的值为 `True` 和 `False`。 如果为 `True`，将在优化过程中自动生成优化查询所需的任何过期统计信息。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自动异步更新统计信息**  
 如果 `True` 为，则启动过期统计信息的自动更新的查询在编译前不会等待统计信息更新。 后续查询将使用可用的已更新统计信息。  
  
 如果为 `False` ，则启动自动更新过期统计信息的查询将等待，直到更新的统计信息可在查询优化计划中使用。  
  
 如果将 " `True` **自动更新统计信息**" 设置为，则将此选项设置为不起作用 `True` 。  
  
## <a name="containment"></a>Containment  
 在包含数据库中，可以在数据库级别配置通常在服务器级别配置的某些设置。  
  
 **默认全文语言 LCID**  
 指定全文检索列的默认语言。 全文检索数据的语言分析取决于数据的语言。 该选项的默认值为服务器的语言。 有关与所显示设置相对应的语言，请参阅 [sys.fulltext_languages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。  
  
 **默认语言**  
 所有新包含数据库用户的默认语言，除非另行指定。  
  
 **启用嵌套的触发器**  
 允许触发器激发其他触发器。 触发器最多可以嵌套 32 级。 有关详细信息，请参阅 [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql) 中的“嵌套触发器”部分。  
  
 **转换干扰词**  
 取消干扰词（即非索引字）导致全文查询的布尔操作返回零行时所产生的错误消息。 有关详细信息，请参阅 [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。  
  
 **两位数年份截止**  
 指示可作为两位数年份输入的最高年数。 可将所列年份及其之前的 99 年作为两位数年份输入。 所有其他年份必须作为四位数年份输入。  
  
 例如，2049 的默认设置表明：作为 '3/14/49' 输入的日期将被解释为 2049 年 3 月 14 日，而作为 '3/14/50' 输入的日期则将被解释为 1950 年 3 月 14 日。 有关详细信息，请参阅 [配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。  
  
## <a name="cursor"></a>游标  
 **提交时关闭游标功能已启用**  
 指定在提交了打开游标的事务之后是否关闭游标。 可能的值为 `True` 和 `False`。 如果为 `True`，则提交或回滚事务时打开的任何游标将被关闭。 如果为 `False`，则提交事务时这些游标仍处于打开状态。 如果为 `False`，回滚事务时将关闭除定义为 INSENSITIVE 或 STATIC 的游标以外的所有游标。 有关详细信息，请参阅 [SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql)。  
  
 **默认游标**  
 指定默认的游标行为。 如果为 `True`，则游标声明默认为 LOCAL。 如果 `False` 为，则 [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标默认为 GLOBAL。  
  
## <a name="filestream"></a>FILESTREAM  
 **FILESTREAM 目录名称**  
 为与所选数据库相关联的 FILESTREAM 数据指定目录名称。  
  
 **FILESTREAM 非事务访问**  
 为从文件系统到 FileTables 中存储的 FILESTREAM 数据的非事务性访问指定以下选项之一：**OFF**、**READ_ONLY** 或 **FULL**。 如果在服务器上未启用 FILESTREAM，则该值将设置为 OFF 并且被禁用。 有关详细信息，请参阅 [FileTables (SQL Server)](../blob/filetables-sql-server.md)。  
  
## <a name="miscellaneous"></a>杂项  
 **ANSI NULL 默认值**  
 在 `NOT NULL` 或 `CREATE TABLE` 语句执行过程中，没有显式定义为 `ALTER TABLE` 的所有用户定义的数据类型或列允许为 Null 值（默认状态）。 有关详细信息，请参阅 [SET ANSI_NULL_DFLT_ON (Transact-SQL)](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql) 和 [SET ANSI_NULL_DFLT_OFF (Transact-SQL)](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql)。  
  
 **ANSI NULLS 已启用**  
 指定等于 (`=`) 和不等于 (`<>`) 比较运算符在与 Null 值一起使用时的行为。 可能的值 `True` 在) 上 (， `False` () 。 如果为 `True`，所有与空值的比较的结果值都为 UNKNOWN。 `False` `True` 如果这两个值都为 null，则非 UNICODE 值与 null 值的比较结果为。 有关详细信息，请参阅 [SET ANSI_NULLS (Transact-SQL)](/sql/t-sql/statements/set-ansi-nulls-transact-sql)。  
  
 **ANSI 填充已启用**  
 指定 ANSI 填充状态是开还是关。 允许的值 `True` 在) 上 (， `False` () 。 有关详细信息，请参阅 [SET ANSI_PADDING (Transact-SQL)](/sql/t-sql/statements/set-ansi-padding-transact-sql)。  
  
 **ANSI 警告已启用**  
 对于几种错误条件指定 ISO 标准行为。 为时 `True` ，如果聚合函数中出现 null 值 (如 SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP 或 COUNT) ，则会生成警告消息。 如果 `False` 为，则不会发出任何警告。 有关详细信息，请参阅 [SET ANSI_WARNINGS (Transact-SQL)](/sql/t-sql/statements/set-ansi-warnings-transact-sql)。  
  
 **算术中止已启用**  
 指定是否启用数据库的算术中止选项。 可能的值为 `True` 和 `False`。 如果为 `True`，则溢出或被零除错误将导致查询或批查询终止。 如果错误发生在事务内，则回滚事务。 如果为 `False`，则将显示警告消息，但会继续执行查询、批处理或事务，就像没有发生错误一样。 有关详细信息，请参阅 [SET ARITHABORT (Transact-SQL)](/sql/t-sql/statements/set-arithabort-transact-sql)。  
  
 **串联的 Null 结果为 Null**  
 指定在与 Null 值连接时的行为。 当属性值为时 `True` ， `string` + NULL 返回 null。 如果 `False` 为，则结果为 `string` 。 有关详细信息，请参阅 [SET CONCAT_NULL_YIELDS_NULL (Transact-SQL)](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)。  
  
 **跨数据库所有权链接已启用**  
 该只读值指示跨数据库所有权链接是否已启用。 如果为 `True` ，则数据库可以是跨数据库所有权链的源或目标。 使用 ALTER DATABASE 语句设置此属性。  
  
 **日期相关性优化已启用**  
 如果 `True` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为，则维护数据库中由 FOREIGN KEY 约束链接并包含列的任意两个表之间的相关统计信息 `datetime` 。  
  
 如果 `False` 为，则不维护相关统计信息。  
  
 **数值舍入中止**  
 指定数据库处理舍入错误的方式。 可能的值为 `True` 和 `False`。 如果为 `True`，则表达式中缺少精度时将生成错误。 如果 `False` 为，则精度损失不会生成错误消息，并将结果舍入为存储结果的列或变量的精度。 有关详细信息，请参阅 [SET NUMERIC_ROUNDABORT (Transact-SQL)](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)。  
  
 **参数化**  
 如果设置为 **SIMPLE**，则基于数据库的默认行为使查询参数化。 如果设置为 **FORCED**，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使数据库中的所有查询参数化。  
  
 **允许带引号的标识符**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关键字在用引号引起来时是否可以用作标识符（对象名或变量名）。 可能的值为 `True` 和 `False`。 有关详细信息，请参阅 [SET QUOTED_IDENTIFIER (Transact-SQL)](/sql/t-sql/statements/set-quoted-identifier-transact-sql)。  
  
 **递归触发器已启用**  
 指定触发器是否可以由其他触发器激发。 可能的值为 `True` 和 `False`。 当设置为时 `True` ，将启用触发器的递归激发。 当设置为时 `False` ，仅阻止直接递归。 若要禁用间接递归，请使用 sp_configure 将 nested triggers 服务器选项设置为 0。 有关详细信息，请参阅 [创建嵌套触发器](../triggers/create-nested-triggers.md)。  
  
 `Trustworthy`  
 显示时 `True` ，此只读选项指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许在数据库中建立的模拟上下文中访问数据库外部的资源。 可以使用 EXECUTE AS 用户语句或数据库模块上的 EXECUTE AS 子句在数据库内建立模拟上下文。  
  
 若要具有访问权限，数据库的所有者也需要具有服务器级的 AUTHENTICATE SERVER 权限。  
  
 使用此属性，还可以在数据库内创建和执行不安全的程序集和外部访问程序集。 除了将此属性设置为 `True` 以外，数据库的所有者还必须拥有服务器级的 EXTERNAL ACCESS ASSEMBLY 或 UNSAFE ASSEMBLY 权限。  
  
 默认情况下，所有用户数据库和所有系统 (数据库（ **MSDB**) 除外）都将此属性设置为 `False` 。 对于 **model** 和 **tempdb** 数据库，不能更改此值。  
  
 每当数据库附加到服务器时，都要将 TRUSTWORTHY 设置为 `False`。  
  
 在模拟上下文内访问数据库以外资源的建议方法是使用证书和签名替代 `Trustworthy` 选项。  
  
 若要设置此属性，请使用 ALTER DATABASE 语句。  
  
 **VarDecimal 存储格式已启用**  
 此选项是只读的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ，从及更高版本开始，所有数据库都启用了 vardecimal 存储格式。 此选项使用 [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)。  
  
## <a name="recovery"></a>恢复  
 **页验证**  
 指定用于发现和报告由磁盘 I/O 错误导致的不完整 I/O 事务的选项。 可能的值为 **None**、 **TornPageDetection**和 **Checksum**。 有关详细信息，请参阅 [管理 suspect_pages 表 (SQL Server)](../backup-restore/manage-the-suspect-pages-table-sql-server.md)在  中还原页。  
  
 **目标恢复时间（秒）**  
 指定在发生崩溃的情况下恢复指定数据库的最长时间（秒）。 有关详细信息，请参阅[数据库检查点 (SQL Server)](../logs/database-checkpoints-sql-server.md)。  
  
## <a name="state"></a>状态  
 **数据库为只读**  
 指定数据库是否为只读。 可能的值为 `True` 和 `False`。 如果为 `True`，用户只能读取数据库中的数据。 用户不能修改数据或数据库对象；不过，数据库本身可以通过使用 DROP DATABASE 语句自行删除。 在为 **“数据库为只读”** 选项指定新值时，数据库不能处于使用状态。 master 数据库是个例外，在设置该选项时，只有系统管理员才能使用 master 数据库。  
  
 **数据库状态**  
 查看数据库的当前状态。 该策略不能编辑。 有关 **“数据库状态”** 的详细信息，请参阅 [Database States](database-states.md)。  
  
 **限制访问**  
 指定哪些用户可以访问该数据库。 可能的值包括：  
  
-   **多个**  
  
     生产数据库的正常状态，允许多个用户同时访问该数据库。  
  
-   **Single**  
  
     用于维护操作，一次只允许一个用户访问该数据库。  
  
-   **Restricted**  
  
     只有 db_owner、dbcreator 或 sysadmin 角色的成员才能使用该数据库。  
  
 **已启用加密**  
 如果 `True` 为，则对此数据库启用数据库加密。 加密时需要数据库加密密钥。 有关详细信息，请参阅[透明数据加密 (TDE)](../security/encryption/transparent-data-encryption.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
