---
title: 表和存储过程的本机编译 | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: rothja
ms.author: jroth
ms.openlocfilehash: 32c5b04610d894e06278fbeecdaf3bbebe850d60
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587818"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>表和存储过程的本机编译
  内存中 OLTP 引入了本机编译的概念。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以本机编译访问内存优化表的存储过程。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以本机编译内存优化表。 与解释型（传统） [!INCLUDE[tsql](../../includes/tsql-md.md)]相比，本机编译可提高访问数据的速度和执行查询的效率。 表和存储过程的本机编译生成 DLL。  
  
 还支持内存优化表类型的本机编译。 有关详细信息，请参阅 [Memory-Optimized Table Variables](../../database-engine/memory-optimized-table-variables.md)。  
  
 本机编译是指将编程构造转换为本机代码的过程，这些代码由处理器指令组成，无需进一步编译或解释。  
  
 内存中 OLTP 在创建内存优化表时编译内存优化表，并且在存储过程加载到本机 DLL 时本机编译存储过程。 此外，在数据库或服务器重新启动后，将重新编译这些 DLL。 重新创建 DLL 所需的信息存储在数据库元数据中。 这些 DLL 不是数据库的一部分，尽管它们与数据库相关联。 例如，这些 DLL 不包括在数据库备份中。  
  
> [!NOTE]  
>  在服务器重启过程中，将重新编译内存优化表。 为了加快数据库恢复速度，本机编译的存储过程不会在服务器重启过程中重新编译，而是在首次执行时编译。 由于这一延迟的编译，本机编译的存储过程仅在首次执行后调用 [sys.dm_os_loaded_modules (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql) 时显示。  
  
## <a name="maintenance-of-in-memory-oltp-dlls"></a>内存中 OLTP DLL 的维护  
 以下查询显示当前在服务器上的内存中加载的所有表和存储过程 DLL：  
  
```sql  
SELECT name, description FROM sys.dm_os_loaded_modules  
where description = 'XTP Native DLL'  
```  
  
 数据库管理员不需要维护由本机编译生成的文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将自动删除那些不再需要的生成的文件。 例如，删除表和存储过程时或删除数据库时将删除生成的文件。  
  
> [!NOTE]  
>  如果编译失败或中断，则某些生成的文件将不会被删除。 出于支持性目的这些文件被有意保留，并且在删除数据库时会被删除。  
  
> [!NOTE]  
>  在数据库启动过程中，SQL Server 会为进行数据库恢复所需的所有表编译 DLL。 如果某个表就在数据库重新启动之前删除，则检查点文件或事务日志中可能仍有该表的残余，因此可能会在数据库启动过程中重新编译该表的 DLL。 重新启动之后，会卸载 DLL，并由正常清除过程删除文件。  
  
## <a name="native-compilation-of-tables"></a>表的本机编译  
 如果使用 `CREATE TABLE` 语句创建内存优化表，会导致将表信息写入数据库元数据，并在内存中创建表和索引结构。 还会将该表编译为 DLL。  
  
 请考虑下面的示例脚本，它创建一个数据库和一个内存优化的表：  
  
```sql  
use master  
go  
create database db1  
go  
alter database db1 add filegroup db1_mod contains memory_optimized_data  
go  
-- adapt filename as needed  
alter database db1 add file (name='db1_mod', filename='c:\data\db1_mod') to filegroup db1_mod  
go  
use db1  
go  
create table dbo.t1  
   (c1 int not null primary key nonclustered,  
    c2 INT)  
with (memory_optimized=on)  
go  
-- retrieve the path of the DLL for table t1  
select name, description FROM sys.dm_os_loaded_modules  
where name like '%xtp_t_' + cast(db_id() as varchar(10)) + '_' + cast(object_id('dbo.t1') as varchar(10)) + '.dll'  
go  
```  
  
 创建该表时还会创建表 DLL 并在内存中加载 DLL。 CREATE TABLE 语句之后立即执行 DMV 查询将检索表 DLL 的路径。  
  
 表 DLL 了解表的索引结构和行格式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用该 DLL 来遍历索引、检索行以及存储行的内容。  
  
## <a name="native-compilation-of-stored-procedures"></a>存储过程的本机编译  
 对使用 NATIVE_COMPILATION 来标记的存储过程执行本机编译。 这意味着该过程中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句均被编译为本机代码，以便高效执行性能关键的业务逻辑。  
  
 有关本机编译的存储过程的详细信息，请参阅 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)。  
  
 考虑下面的示例存储过程，它在前一示例的表 t1 中插入行：  
  
```sql  
create procedure dbo.native_sp  
with native_compilation, schemabinding, execute as owner  
as  
begin atomic  
with (transaction isolation level=snapshot, language=N'us_english')  
  
  declare @i int = 1000000  
  while @i > 0  
  begin  
    insert dbo.t1 values (@i, @i+1)  
    set @i -= 1  
  end  
  
end  
go  
exec dbo.native_sp  
go  
-- reset  
delete from dbo.t1  
go  
```  
  
 native_sp 的 DLL 可直接与 t1 的 DLL 以及内存中 OLTP 存储引擎交互，以尽快插入行。  
  
 内存中 OLTP 编译器利用查询优化器为存储过程中的每个查询创建高效的执行计划。 请注意，如果表中的数据更改了，本机编译的存储过程不会自动重新编译。 有关使用内存中 OLTP 维护统计信息和存储过程的详细信息，请参阅 [内存优化表的统计信息](memory-optimized-tables.md)。  
  
## <a name="security-considerations-for-native-compilation"></a>有关本机编译的安全注意事项  
 表和存储过程的本机编译使用内存中 OLTP 编译器。 此编译器生成的文件将写入磁盘和载入内存。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用以下机制限制访问这些文件。  
  
### <a name="native-compiler"></a>本机编译器  
 编译器可执行文件以及本机编译所需的二进制文件和头文件安装在文件夹 MSSQL\Binn\Xtp 下，作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的一部分。 因此，如果默认实例安装在 C:\Program files 下，则编译器文件安装在 C:\Program files \MSSQL12. 中 \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。MSSQLSERVER\MSSQL\Binn\Xtp.  
  
 为了限制访问编译器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用访问控制列表 (ACL) 限制访问二进制文件。 通过 ACL 保护所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二进制文件免遭修改或篡改。 本机编译器的 ACL 还限制使用编译器；仅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和系统管理员对本机编译器文件具有读取和执行权限。  
  
### <a name="files-generated-by-a-native-compilation"></a>本机编译生成的文件  
 编译表或存储过程时生成的文件包括 DLL 和中间文件，其中包括如下扩展名的文件：.c、.obj、.xml 和 .pdb。 生成的文件保存在默认数据文件夹的一个子文件夹中。 该子文件夹称为 Xtp。 在用默认数据文件夹安装默认实例时，生成的文件放置在 C:\Program files \MSSQL12. 中 \\ [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。MSSQLSERVER\MSSQL\DATA\Xtp.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过以下三种方式防止纂改所生成的 DLL：  
  
-   将表或存储过程编译为 DLL 后，此 DLL 将立即载入内存并链接到 sqlserver.exe 进程。 DLL 链接到进程后，即无法修改该 DLL。  
  
-   重新启动数据库后，将根据数据库元数据重新编译所有表和存储过程（删除再重新创建）。 这样将消除恶意代理对所生成的文件作出的任何更改。  
  
-   所生成的文件被视为用户数据的一部分，并且其安全限制（通过 ACL）与数据库文件相同：仅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和系统管理员可访问这些文件。  
  
 无需用户干预即可管理这些文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将根据需要创建和删除文件。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表](memory-optimized-tables.md)   
 [本机编译的存储过程](natively-compiled-stored-procedures.md)  
  
  
