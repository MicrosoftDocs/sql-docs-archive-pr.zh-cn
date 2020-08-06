---
title: 用于演示内存中 OLTP 的 AdventureWorks 扩展 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0186b7f2-cead-4203-8360-b6890f37cde8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73a87751aa6cd4734f81b60cdd87a62939ba4ead
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693051"
---
# <a name="extensions-to-adventureworks-to-demonstrate-in-memory-oltp"></a>演示内存中 OLTP 的 AdventureWorks 扩展
    
## <a name="overview"></a>概述  
 此示例演示属于 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 一部分的新 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]功能。 它演示新的内存优化表和本机编译的存储过程，可以用于展示 [!INCLUDE[hek_2](../includes/hek-2-md.md)]的性能优势。  
  
> [!NOTE]  
>  若要查看 SQL Server 2016 的本主题，请参阅 [演示内存中 OLTP 的 AdventureWorks 扩展](https://msdn.microsoft.com/library/mt465764.aspx)  
  
 该示例将 AdventureWorks 数据库中的 5 个表迁移到内存优化表，并包括销售订单处理演示工作负荷。 可以使用此演示工作负荷了解在服务器上使用 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 的性能优势。  
  
 在示例说明中，我们讨论将表迁移到 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 时进行的权衡，以说明 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]中对内存优化表（尚未）不支持的功能。  
  
 此示例的文档的结构如下：  
  
-   安装示例和运行演示工作负荷的[先决条件](#Prerequisites)  
  
-   [基于 AdventureWorks 安装内存中 OLTP 示例](#InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks)的说明  
  
-   [示例表和过程的说明](#Descriptionofthesampletablesandprocedures)-这包括通过示例添加到 AdventureWorks 的表和过程的说明，以及将 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 一些原始 AdventureWorks 表迁移到内存优化的注意事项  
  
-   执行[使用演示工作负荷执行度量](#PerformanceMeasurementsusingtheDemoWorkload)的说明 - 包括有关安装和运行 ostress（一种用于驱动工作负荷的工具）以及运行演示工作负荷本身的说明  
  
-   [示例中的内存和磁盘空间利用率](#MemoryandDiskSpaceUtilizationintheSample)  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]RTM-评估版、开发人员版或企业版  
  
-   对于性能测试，服务器的规格类似于生产环境。 对于此特定示例，应至少有 16 GB 内存可供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用。 有关硬件的一般指导原则 [!INCLUDE[hek_2](../includes/hek-2-md.md)] ，请参阅以下博客文章：[https://cloudblogs.microsoft.com/sqlserver/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014/](https://cloudblogs.microsoft.com/sqlserver/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014/)  
  
##  <a name="installing-the-hek_2-sample-based-on-adventureworks"></a><a name="InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks"></a>基于 AdventureWorks 安装 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 示例  
 请按照以下步骤安装示例：  
  
1.  下载用于 AdventureWorks2014 数据库完整备份的存档：  
  
    1.  打开以下内容： [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661) 。  
  
    2.  提示保存文件时，选择本地文件夹。  
  
2.  将 **AdventureWorks2014.bak** 文件提取到本地文件夹，例如“c:\temp”。  
  
3.  使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 或 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]还原数据库备份：  
  
    1.  标识数据文件的目标文件夹和文件名，例如  
  
         “h:\DATA\AdventureWorks2014_Data.mdf”  
  
    2.  标识日志文件的目标文件夹和文件名，例如  
  
         “i:\DATA\AdventureWorks2014_log.ldf”  
  
        1.  日志文件应置于与数据文件不同的驱动器上，最好是低延迟驱动器（如 SSD 或 PCIe 存储）以实现最大性能。  
  
     示例 T-SQL 脚本：  
  
    ```  
    RESTORE DATABASE [AdventureWorks2014]   
      FROM DISK = N'C:\temp\AdventureWorks2014.bak'   
        WITH FILE = 1,    
      MOVE N'AdventureWorks2014_Data' TO N'h:\DATA\AdventureWorks2014_Data.mdf',    
      MOVE N'AdventureWorks2014_Log' TO N'i:\DATA\AdventureWorks2014_log.ldf'  
     GO  
    ```  
  
4.  通过在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的查询窗口中运行命令，将数据库所有者更改为您服务器上的某个登录名：  
  
    ```  
    ALTER AUTHORIZATION ON DATABASE::AdventureWorks2014 TO [<NewLogin>]  
    ```  
  
5.  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[hek_2](../includes/hek-2-md.md)] 从[SQL Server 2014 RTM 内存中 OLTP 示例中](https://go.microsoft.com/fwlink/?LinkID=396372)将示例脚本 "rtm sample" 下载到本地文件夹。  
  
6.  更新脚本 "RTM Sample" 中变量 "checkpoint_files_location" 的值 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[hek_2](../includes/hek-2-md.md)] ，以指向 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 检查点文件的目标位置。 检查点文件应置于具有良好顺序 IO 性能的驱动器上。  
  
     将变量“database_name”的值更新为指向 AdventureWorks2014 数据库。  
  
    1.  请确保在 \' 路径名称中包含反斜杠 "  
  
    2.  示例：  
  
        ```  
        :setvar checkpoint_files_location "d:\DBData\"  
        ...  
        :setvar database_name "AdventureWorks2014"  
        ```  
  
7.  以下列两种方式之一执行示例脚本：  
  
    1.  使用 sqlcmd 命令行实用工具。 例如，通过在包含脚本的文件夹中，从命令提示符处运行以下命令：  
  
        ```  
        sqlcmd -S . -E -i "ssSQL14 RTM hek_2 Sample.sql"  
        ```  
  
    2.  使用 Management Studio：  
  
        1.  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[hek_2](../includes/hek-2-md.md)] 在查询窗口中打开脚本 "RTM Sample .sql"  
  
        2.  连接到包含数据库 AdventureWorks2014 的目标服务器  
  
        3.  通过单击 "查询 > SQLCMD 模式" 启用 SQLCMD 模式  
  
        4.  单击按钮 "执行" 以运行脚本  
  
##  <a name="description-of-the-sample-tables-and-procedures"></a><a name="Descriptionofthesampletablesandprocedures"></a> 示例表和过程的说明  
 示例基于 AdventureWorks 中的现有表为产品和销售订单创建新表。 新表的架构类似于现有表，不过有几个区别，如下所述。  
  
 新的内存优化表带有后缀“_inmem”。 示例还包括带有后缀“_ondisk”的对应表 - 这些表可以用于在系统上进行内存优化表与基于磁盘的表性能之间的一对一比较。  
  
 请注意，用于性能比较的工作负荷中使用的内存优化表具有完全持久性并且会完整记录。 这些表不会牺牲持久性或可靠性来获取性能提升。  
  
 此示例的目标工作负荷是销售订单处理，我们还考虑在其中包含产品和折扣信息。 为此，创建了表 SalesOrderHeader、SalesOrderDetail、Product、SpecialOffer 和 SpecialOfferProduct。  
  
 两个新存储过程 Sales.usp_InsertSalesOrder_inmem 和 Sales.usp_UpdateSalesOrderShipInfo_inmem 用于插入销售订单和更新给定销售订单的发货信息。  
  
 新架构“Demo”包含用于执行演示工作负荷的帮助器表和存储过程。  
  
 具体而言， [!INCLUDE[hek_2](../includes/hek-2-md.md)] 示例向 AdventureWorks 添加以下对象：  
  
### <a name="tables-added-by-the-sample"></a>示例添加的表  
  
#### <a name="the-new-tables"></a>新表  
 Sales.SalesOrderHeader_inmem  
  
-   有关销售订单的表头信息。 每个销售订单都在此表中有对应的一行。  
  
 Sales.SalesOrderDetail_inmem  
  
-   销售订单的详细信息。 销售订单的每个行项都在此表中有对应的一行。  
  
 Sales.SpecialOffer_inmem  
  
-   有关特价商品的信息，包括与每个特价商品关联的折扣百分比。  
  
 Sales.SpecialOfferProduct_inmem  
  
-   特价商品与产品之间的引用表。 每个特价商品可以包含零个或多个产品，每个产品可以包含在零个或多个特价商品中。  
  
 Production.Product_inmem  
  
-   有关产品的信息，包括其标价。  
  
 Demo.DemoSalesOrderDetailSeed  
  
-   在演示工作负荷中用于构造示例销售订单。  
  
 表的基于磁盘的变体：  
  
-   Sales.SalesOrderHeader_ondisk  
  
-   Sales.SalesOrderDetail_ondisk  
  
-   Sales.SpecialOffer_ondisk  
  
-   Sales.SpecialOfferProduct_ondisk  
  
-   Production.Product_ondisk  
  
#### <a name="differences-between-original-disk-based-and-the-and-new-memory-optimized-tables"></a>原始基于磁盘的表与新内存优化表之间的区别  
 在很大程度上，此示例引入的新表使用的列和数据类型与原始表相同。 但二者之间存在一些区别。 下面列出了区别以及更改的理由。  
  
 Sales.SalesOrderHeader_inmem  
  
-   内存优化表支持*默认约束* ，大多数默认约束按原样迁移。 但是，原始表 Sales.SalesOrderHeader 包含两个为列 OrderDate 和 ModifiedDate 检索当前日期的默认约束。 在具有大量并发的高吞吐量订单处理工作负荷中，任何全局资源都可能成为争用点。 系统时间就是全局资源，我们观察到，它可能在运行插入销售订单的 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 工作负荷时成为瓶颈，特别是如果需要为销售订单表头中的多列以及销售订单详细信息检索系统时间。 此示例中解决问题的方式是仅为插入的每个销售订单检索系统时间一次，然后将该值用于 SalesOrderHeader_inmem 和 SalesOrderDetail_inmem 中的 datetime 列以及存储过程 Sales.usp_InsertSalesOrder_inmem。  
  
-   *别名 UDT* - 原始表将两个别名用户定义数据类型 (UDT) dbo.OrderNumber 和 dbo.AccountNumber 分别用于列 PurchaseOrderNumber 和 AccountNumber。 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 在内存优化表中不支持别名 UDT，因而新表分别使用系统数据类型 nvarchar(25) 和 nvarchar(15)。  
  
-   *索引键中可以为 Null 的列* - 在原始表中，列 SalesPersonID 可以为 Null，而在新表中，该列不可为 Null，并且默认约束值为 -1。 这是因为内存优化表中的索引不能在索引键中具有可以为 Null 的列；-1 是这种情况下 NULL 的代理项。  
  
-   计算列 - 省略了计算列 SalesOrderNumber 和 TotalDue，因为 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 在内存优化表中不支持计算列。 新视图 Sales.vSalesOrderHeader_extended_inmem 反映了列 SalesOrderNumber and TotalDue。 因此，如果需要这些列，可以使用此视图。  
  
-   在*中，内存优化表不支持* 外键约束 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。 此外，SalesOrderHeader_inmem 是示例工作负荷中的热表，并且外键约束需要对所有 DML 操作进行附加处理，因为它需要在这些约束引用的所有其他表中进行查找。 因此，假设应用程序可确保引用完整性，从而在插入行时不验证引用完整性。 可以使用以下脚本，通过存储过程 dbo.usp_ValidateIntegrity 验证此表中数据的引用完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   在 SQL Server 2014 中，内存优化表不支持*检查约束* 。 使用以下脚本可随引用完整性一起验证域完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - 省略了 rowguid 列。 虽然内存优化表支持 uniqueidentifier，但是 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]中不支持选项 ROWGUIDCOL。 这种列通常用于合并复制或具有文件流列的表。 此示例不包括其中任何一种。  
  
 Sales.SalesOrderDetail  
  
-   *默认约束* - 类似于 SalesOrderHeader，未迁移需要系统时间/时间的默认约束，而是由插入销售订单的存储过程负责在第一次插入时插入当前系统日期/时间。  
  
-   *计算列* - 在 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中，内存优化表不支持未作为计算列迁移的计算列 LineTotal。 若要访问此列，请使用视图 Sales.vSalesOrderDetail_extended_inmem。  
  
-   *Rowguid* - 省略了 rowguid 列。 有关详细信息，请参见表 SalesOrderHeader 的说明。  
  
-   对于 *检查* 和 *外键* 约束，请参见 SalesOrderHeader 的说明。 以下脚本可用于验证此表的域和引用完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
 Production.Product  
  
-   *别名 UDT* - 原始表使用等效于系统数据类型位的用户定义数据类型 dbo.Flag。 迁移的表改用位数据类型。  
  
-   *BIN2 排序规则*-列 Name 和 ProductNumber 包含在索引键中，因此必须在中具有 BIN2 排序规则 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 。 这里假设应用程序不依赖于排序规则具体内容（如区分大小写）。  
  
-   *Rowguid* - 省略了 rowguid 列。 有关详细信息，请参见表 SalesOrderHeader 的说明。  
  
-   *唯一*、 *检查* 和 *外键约束* 通过两种方式实现：存储过程 Product.usp_InsertProduct_inmem 和 Product.usp_DeleteProduct_inmem 可以用于插入和删除产品；这些过程验证域和引用完整性，在违反完整性时会失败。 此外，以下脚本还可用于按原样验证域和引用完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Production.Product')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
    -   请注意，存储过程 usp_InsertProduct_inmem 和 usp_DeleteProduct_inmem 仅考虑迁移的表之间的外键。 不考虑对其他表 ProductModel、ProductSubcategory 和 UnitMeasure 的引用。  
  
 Sales.SpecialOffer  
  
-   *检查* 和 *外键约束* 通过两种方式实现：存储过程 Sales.usp_InsertSpecialOffer_inmem 和 Sales.usp_DeleteSpecialOffer_inmem 可用于插入和删除特价商品；这些过程验证域和引用完整性，在违反完整性时会失败。 此外，以下脚本还可用于按原样验证域和引用完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOffer_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - 省略了 rowguid 列。 有关详细信息，请参见表 SalesOrderHeader 的说明。  
  
 Sales.SpecialOfferProduct  
  
-   *外键约束* 通过两种方式实现：存储过程 Sales.usp_InsertSpecialOfferProduct_inmem 可用于插入和删除特价商品与产品之间的关系；此过程验证引用完整性，在违反完整性时会失败。 此外，以下脚本还可用于按原样验证引用完整性：  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOfferProduct_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* - 省略了 rowguid 列。 有关详细信息，请参见表 SalesOrderHeader 的说明。  
  
#### <a name="considerations-for-indexes-on-memory-optimized-tables"></a>有关内存优化表的索引的注意事项  
 内存优化表的基线索引是 NONCLUSTERED 索引，该索引支持点查找（采用相等谓词的索引查找）、范围扫描（采用不相等谓词的索引查找）、全文索引扫描和有序扫描。 此外，NONCLUSTERED 索引还支持对索引键的前导列进行搜索。 事实上，内存优化 NONCLUSTERED 索引支持基于磁盘的 NONCLUSTERED 索引支持的所有操作，唯一的例外是向后扫描。 因此，使用 NONCLUSTERED 索引是针对索引的安全选择。  
  
 HASH 索引可用于进一步优化工作负荷。 这些索引特别针对点查找和行插入进行了优化。 但是，必须考虑到这些索引不支持范围扫描、有序扫描或是对前导索引键列进行的搜索。 因此，使用这些索引时需要谨慎。 此外，还需要在创建时指定 bucket_count。 它通常应设置为索引键值的一到二倍之间，不过估计过高通常不是什么问题。  
  
 有关 [索引指南](https://technet.microsoft.com/library/dn133166\(v=sql.120\).aspx) 和 [选择正确 bucket_count](https://technet.microsoft.com/library/dn494956\(v=sql.120\).aspx)的指南的详细信息，请参阅联机丛书。  
  
 迁移的表中的索引针对演示销售订单处理工作负荷进行了优化。 该工作负荷依赖于表 Sales.SalesOrderHeader_inmem 和 Sales.SalesOrderDetail_inmem 中的插入和点查找，还依赖于对表 Production.Product_inmem 和 Sales.SpecialOffer_inmem 中的主键列进行的点查找。  
  
 Sales.SalesOrderHeader_inmem 有三个索引，因为性能原因，而且工作负荷无需有序或范围扫描，所以这些索引都是 HASH 索引。  
  
-   (SalesOrderID) 上的 HASH 索引：bucket_count 大小为 1000 万（向上舍入为 1600 万），因为预期销售订单数为 1000 万  
  
-   (SalesPersonID) 上的 HASH 索引：bucket_count 为 1000 万。 提供的数据集不包含许多销售人员，但是允许将来增加，并且不会因 bucket_count 过大而影响点查找性能。  
  
-   (CustomerID) 上的 HASH 索引：bucket_count 为 1 万。 提供的数据集不包含许多客户，但是允许将来增加。  
  
 Sales.SalesOrderDetail_inmem 有三个索引，因为性能原因，而且工作负荷无需有序或范围扫描，所以这些索引都是 HASH 索引。  
  
-   (SalesOrderID, SalesOrderDetailID) 上的 HASH 索引：这是主键索引，即使不会经常对 (SalesOrderID, SalesOrderDetailID) 进行查找，将哈希索引用于该键也可加快行插入速度。 bucket_count 大小为 5000 万（向上舍入为 6700 万）：预期销售订单数为 1000 万，这是针对平均每个订单 5 个项目确定的大小  
  
-   (SalesOrderID) 上的 HASH 索引：经常按销售订单进行查找：您要查找对应于单个订单的所有行项。  bucket_count 大小为 1000 万（向上舍入为 1600 万），因为预期销售订单数为 1000 万  
  
-   (ProductID) 上的 HASH 索引：bucket_count 为 1 万。 提供的数据集不包含许多产品，但是允许将来增加。  
  
 Production.Product_inmem 有三个索引  
  
-   (ProductID) 上的 HASH 索引：对 ProductID 进行的查找是演示工作负荷的关键因素，因此这是哈希索引  
  
-   (Name) 上的 NONCLUSTERED 索引：这允许进行产品名称的有序扫描  
  
-   (ProductNumber) 上的 NONCLUSTERED 索引：这允许进行产品编号的有序扫描  
  
 Sales.SpecialOffer_inmem 在 (SpecialOfferID) 上有一个 HASH 索引：对特价商品进行的点查找是演示工作负荷的关键因素。 bucket_count 大小为 100 万，允许将来增加。  
  
 Sales.SpecialOfferProduct_inmem 未在演示工作负荷中进行引用，因而表面上无需使用此表中的哈希索引优化工作负荷 - (SpecialOfferID, ProductID) 和 (ProductID) 上的索引是 NONCLUSTERED。  
  
 请注意，以上某些 bucket_count 过大，但是 SalesOrderHeader_inmem 和 SalesOrderDetail_inmem 上的索引的 bucket_count 并非如此：其大小仅用于 1000 万个销售订单。 这样做是为了可以在内存可用性较低的系统上安装示例，不过在这些情况下，演示工作负荷会由于内存不足而失败。 如果的确要扩展为远远超过 1000 万个销售订单，可以随意相应地提高桶计数。  
  
#### <a name="considerations-for-memory-utilization"></a>内存利用率注意事项  
 示例数据库中的内存利用率（运行演示工作负荷之前以及之后）在 [内存优化表的内存利用率](#Memoryutilizationforthememory-optimizedtables)一节中进行了讨论。  
  
### <a name="stored-procedures-added-by-the-sample"></a>示例添加的存储过程  
 用于插入销售订单和更新发货详细信息的两个重要存储过程如下：  
  
-   Sales.usp_InsertSalesOrder_inmem  
  
    -   在数据库中插入新销售订单并输出该销售订单的 SalesOrderID。 它采用销售订单表头的详细信息以及订单中的行项作为输入参数。  
  
    -   输出参数：  
  
        -   @SalesOrderID int - 刚插入的销售订单的 SalesOrderID  
  
    -   输入参数（必需）：  
  
        -   @DueDate datetime2  
  
        -   @CustomerID int  
  
        -   @BillToAddressID [int]  
  
        -   @ShipToAddressID [int]  
  
        -   @ShipMethodID [int]  
  
        -   @SalesOrderDetails Sales.SalesOrderDetailType_inmem - 包含订单行项的 TVP  
  
    -   输入参数（可选）：  
  
        -   @Status [tinyint]  
  
        -   @OnlineOrderFlag [bit]  
  
        -   @PurchaseOrderNumber [nvarchar](25\)  
  
        -   @AccountNumber [nvarchar](15\)  
  
        -   @SalesPersonID [int]  
  
        -   @TerritoryID [int]  
  
        -   @CreditCardID [int]  
  
        -   @CreditCardApprovalCode [varchar](15\)  
  
        -   @CurrencyRateID [int]  
  
        -   @Comment nvarchar(128)  
  
-   Sales.usp_UpdateSalesOrderShipInfo_inmem  
  
    -   更新给定销售订单的发货信息。 这也会更新销售订单所有行项的发货信息。  
  
    -   这是本机编译的存储过程 Sales.usp_UpdateSalesOrderShipInfo_native 的包装过程，其中的重试逻辑用于处理与更新该订单的并发事务形成的（意外）潜在冲突。 有关重试逻辑的更多信息，请参见 [此处](https://technet.microsoft.com/library/dn169141\(v=sql.120\).aspx)的联机丛书主题。  
  
-   Sales.usp_UpdateSalesOrderShipInfo_native  
  
    -   这是实际处理发货信息更新的本机编译的存储过程。 它可以从包装存储过程 Sales.usp_UpdateSalesOrderShipInfo_inmem 进行调用。 如果客户端可以处理失败并实现重试逻辑，则您可以直接调用此过程，而不是使用包装存储过程。  
  
 以下存储过程用于演示工作负荷。  
  
-   Demo.usp_DemoReset  
  
    -   通过清空 SalesOrderHeader 和 SalesOrderDetail 表并对这两个表重设种子来重置演示。  
  
 以下存储过程用于对内存优化表进行插入和删除，同时保证域和引用完整性。  
  
-   Production.usp_InsertProduct_inmem  
  
-   Production.usp_DeleteProduct_inmem  
  
-   Sales.usp_InsertSpecialOffer_inmem  
  
-   Sales.usp_DeleteSpecialOffer_inmem  
  
-   Sales.usp_InsertSpecialOfferProduct_inmem  
  
 最后，以下存储过程用于验证域和引用完整性。  
  
1.  dbo.usp_ValidateIntegrity  
  
    -   可选参数：@object_id - 要验证其完整性的对象的 ID  
  
    -   此过程依赖于用于需要验证的完整性规则的表 dbo.DomainIntegrity、dbo.ReferentialIntegrity 和 dbo.UniqueIntegrity - 示例基于对 AdventureWorks 数据库中的原始表存在的检查、外键和唯一约束来填充这些表。  
  
    -   它依赖于帮助器过程 dbo.usp_GenerateCKCheck、dbo.usp_GenerateFKCheck 和 dbo.GenerateUQCheck 来生成执行完整性检查所需的 T-SQL。  
  
##  <a name="performance-measurements-using-the-demo-workload"></a><a name="PerformanceMeasurementsusingtheDemoWorkload"></a> 使用演示工作负荷执行度量  
 Ostress 是由 [!INCLUDE[msCoName](../includes/msconame-md.md)] CSS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持团队开发的命令行工具。 此工具可以用于并行执行查询或运行存储过程。 可以配置线程数来并行运行给定 T-SQL 语句，并且可以指定应对此线程执行语句的次数；Ostress 会加快线程，对所有线程并行执行语句。 对所有线程完成执行之后，Ostress 会报告所有线程完成执行所花费的时间。  
  
### <a name="installing-ostress"></a>安装 Ostress  
 Ostress 作为 RML 实用工具的一部分进行安装；Ostress 没有独立安装。  
  
 安装步骤：  
  
1.  从以下页面下载并运行 RML 实用工具的 x64 安装包：[https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx](https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)  
  
2.  如果出现指示某些文件正在使用的对话框，请单击“继续”  
  
### <a name="running-ostress"></a>运行 Ostress  
 Ostress 从命令行提示符运行。 从“RML 命令提示符”（作为 RML 实用工具的一部分安装）运行该工具是最方便的。  
  
 若要打开 RML 命令提示符，请按照以下说明执行：  
  
 在 Windows Server 2012 [R2] 以及 Windows 8 和 8.1 中，通过单击 Windows 键打开“开始”菜单，然后键入“rml”。 单击“RML 命令提示符”（处于搜索结果列表中）。  
  
 确保命令提示符位于 RML 实用工具安装文件夹中。 例如：  
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP01.jpg)  
  
 在不使用任何命令行选项的情况下仅运行 ostress.exe 时，可以查看 Ostress 的命令行选项。 对此示例运行 Ostress 时要考虑的主要选项有：  
  
-   -S 要连接到的 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称  
  
-   -E 使用 Windows 身份验证连接 (默认) ;如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证，请使用选项-u 和-P 分别指定用户名和密码  
  
-   -d 数据库的名称，对于此示例为 AdventureWorks2014  
  
-   -Q 要执行的 T-SQL 语句  
  
-   -n 处理每个输入文件/查询的连接数  
  
-   -r 每个连接执行每个输入文件/查询的迭代数  
  
### <a name="demo-workload"></a>演示工作负荷  
 演示工作负荷中使用的主要存储过程是 Sales.usp_InsertSalesOrder_inmem/ondisk。 下面的脚本使用示例数据构造一个表值参数 (TVP)，并调用该过程以插入包含 5 个行项的销售订单。  
  
 Ostress 工具用于并行执行存储过程调用，以模拟并发插入销售订单的客户端。  
  
 在每次执行 Demo.usp_DemoReset 的压力运行之后重置演示。 此过程删除内存优化表中的行、截断基于磁盘的表并执行数据库检查点。  
  
 以下脚本并发执行，以模拟销售订单处理工作负荷：  
  
```  
DECLARE   
      @i int = 0,   
      @od Sales.SalesOrderDetailType_inmem,   
      @SalesOrderID int,   
      @DueDate datetime2 = sysdatetime(),   
      @CustomerID int = rand() * 8000,   
      @BillToAddressID int = rand() * 10000,   
      @ShipToAddressID int = rand() * 10000,   
      @ShipMethodID int = (rand() * 5) + 1;   
  
INSERT INTO @od   
SELECT OrderQty, ProductID, SpecialOfferID   
FROM Demo.DemoSalesOrderDetailSeed   
WHERE OrderID= cast((rand()*106) + 1 as int);   
  
WHILE (@i < 20)   
BEGIN;   
      EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od;   
      SET @i += 1   
END  
  
```  
  
 借助此脚本，构造的每个示例订单会通过在 WHILE 循环中执行的 20 个存储过程插入 20 次。 因为数据库用于构造示例订单，所以使用该循环。 在典型生产环境中，中间层应用程序将构造要插入的销售订单。  
  
 上面的脚本将销售订单插入内存优化表中。 用于将销售订单插入基于磁盘的表中的脚本通过将两个“_inmem”替换为“_ondisk”而派生。  
  
 我们将使用 Ostress 工具通过几个并发连接执行脚本。 我们将使用参数“-n”控制连接数，使用参数“r”控制对每个连接执行脚本的次数。  
  
#### <a name="functional-validation-of-the-workload"></a>工作负荷的功能验证  
 若要验证一切是否正常运行，我们将从一个示例测试开始，使用10个并发连接和5个迭代，同时插入总共 10 * 5 \* 20 = 1000 销售订单。  
  
 对于以下命令，我们假设在本地计算机上使用默认实例。 如果使用命名实例或使用远程服务器，请使用参数 -S 相应地更改服务器名称。  
  
 在 RML 命令提示符处使用以下命令，将 1000 个销售订单插入内存优化表：  
  
 单击“复制”按钮复制该命令，将其粘贴到 RML 实用工具命令提示符处。  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 如果一切正常，则命令窗口类似于以下这样。 不会出现错误消息。  
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP02.jpg)  
  
 通过在 RML 命令提示符处运行以下命令，可以验证工作负荷对于基于磁盘的表是否也正常工作：  
  
 单击“复制”按钮复制该命令，将其粘贴到 RML 实用工具命令提示符处。  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
#### <a name="running-the-workload"></a>运行工作负荷  
 为了进行大规模测试，我们使用 100 个连接插入 1000 万个销售订单。 此测试适合在中等服务器（例如，8 个物理核心、16 个逻辑核心以及用于日志的基本 SSD 存储）上执行。 如果该测试在你的硬件上性能不佳，请查看[解决测试运行缓慢的问题](#Troubleshootingslow-runningtests)一节。如果要降低此测试的压力级别，请通过更改参数“-n”减少连接数。 例如，若要将连接计数减少为 40，请将参数“-n100”更改为“-n40”。  
  
 作为工作负荷的性能度量，我们使用 ostress.exe 在运行工作负荷之后报告的占用时间。  
  
##### <a name="memory-optimized-tables"></a>内存优化表  
 我们首先对内存优化表运行工作负荷。 以下命令打开 100 个线程，每个线程运行 5,000 次迭代。  每次迭代在单独事务中插入 20 个销售订单。 每次迭代进行 20 个插入，对数据库用于生成待插入数据进行补偿。 这会生成总共 20 * 5,000 \* 100 = 10,000,000 个销售订单插入。  
  
 打开 RML 命令提示符，执行以下命令：  
  
 单击“复制”按钮复制该命令，将其粘贴到 RML 实用工具命令提示符处。  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 在一台共有 8 个物理（16 个逻辑）核心的测试服务器上，需要 2 分 5 秒。 在另一台有 24 个物理（48 个逻辑）核心的测试服务器上，需要 1 分 0 秒。  
  
 在工作负荷运行期间观察 CPU 利用率（例如使用任务管理器）。 可以看到 CPU 利用率接近 100%。 如果不是这样，则存在日志 IO 瓶颈，另请参见 [运行缓慢的测试的故障排除](#Troubleshootingslow-runningtests)。  
  
##### <a name="disk-based-tables"></a>基于磁盘的表  
 以下命令对基于磁盘的表运行工作负荷。 请注意，此工作负荷可能要花一些时间执行，这在很大程度上是由于系统中存在闩锁争用。 内存优化表没有闩锁，因而不会遇到这个问题。  
  
 打开 RML 命令提示符，执行以下命令：  
  
 单击“复制”按钮复制该命令，将其粘贴到 RML 实用工具命令提示符处。  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 在一台共有 8 个物理（16 个逻辑）核心的测试服务器上，需要 41 分 25 秒。 在另一台有 24 个物理（48 个逻辑）核心的测试服务器上，需要 52 分 16 秒。  
  
 此测试中内存优化表与基于磁盘的表之间存在性能差异的主要因素在于，使用基于磁盘的表时， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 无法完全利用 CPU。 原因在于闩锁争用：并发事务尝试写入相同数据页；闩锁用于确保一次只有一个事务才能写入页。 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 引擎没有闩锁，数据行不是按页组织。 因而，并发事务不会阻塞彼此的插入，从而 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 能够完全利用 CPU。  
  
 在工作负荷运行期间可以观察 CPU 利用率（例如使用任务管理器）。 对于基于磁盘的表，可以看到 CPU 利用率远低于 100%。 在有 16 个逻辑处理器的测试配置中，利用率保持在 24% 左右。  
  
 或者，可以使用性能监视器通过性能计数器“\SQL Server:Latches\Latch Waits/sec”查看每秒的闩锁等待数。  
  
#### <a name="resetting-the-demo"></a>重置演示  
 若要重置演示，请打开 RML 命令提示符，执行以下命令：  
  
```  
ostress.exe -S. -E -dAdventureWorks2014 -Q"EXEC Demo.usp_DemoReset"  
```  
  
 根据硬件情况，可能需要几分钟运行。  
  
 我们建议在每次演示运行之后重置。 因为此工作负荷仅涉及插入，所以每次运行将占用更多内存，因而需要重置来防止内存不足。 运行之后占用的内存量在 [运行工作负荷之后的内存利用率](#Memoryutilizationafterrunningtheworkload)一节中进行了讨论。  
  
###  <a name="troubleshooting-slow-running-tests"></a><a name="Troubleshootingslow-runningtests"></a> 解决测试运行缓慢的问题  
 测试结果通常因硬件而异，也因测试运行中使用的并发级别而异。 结果与预期不符时要了解的几个方面有：  
  
-   并发事务数：对单个线程运行工作负荷时，通过 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 获得的性能提升可能小于 2 倍。 如果并发级别较高，则闩锁争用是唯一的大问题。  
  
-   可供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用的核心数较少：这意味着系统中的并发级别较低，因为并发执行事务的数量不能超过可供 SQL 使用的核心数。  
  
    -   症状：如果对基于磁盘的表运行工作负荷时 CPU 利用率较高，则意味着不存在很多争用，说明缺乏并发性。  
  
-   日志驱动器的速度：如果日志驱动器无法跟上系统中的事务吞吐量级别，则工作负荷会在日志 IO 方面遇到瓶颈。 虽然日志记录对于 [!INCLUDE[hek_2](../includes/hek-2-md.md)]更加高效，但是如果日志 IO 是瓶颈，则性能提升的可能性有限。  
  
    -   症状：如果对内存优化表运行工作负荷时 CPU 利用率不接近于 100% 或是非常尖峰，则可能存在日志 IO 瓶颈。 这可以通过打开资源监视器查看日志驱动器的队列长度来进行确认。  
  
##  <a name="memory-and-disk-space-utilization-in-the-sample"></a><a name="MemoryandDiskSpaceUtilizationintheSample"></a> 示例中的内存和磁盘空间利用率  
 下面我们讨论示例数据库的内存和磁盘空间利用率方面的情况。 我们还会介绍在有 16 个逻辑核心的测试服务器上看到的结果。  
  
###  <a name="memory-utilization-for-the-memory-optimized-tables"></a><a name="Memoryutilizationforthememory-optimizedtables"></a> 内存优化表的内存利用率  
  
#### <a name="overall-utilization-of-the-database"></a>数据库的总体利用率  
 以下查询可用于获取系统中 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 的总体内存利用率。  
  
```  
SELECT type  
   , name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 刚刚创建数据库之后的快照：  
  
||||  
|-|-|-|  
|type|name|**pages_MB**|  
|MEMORYCLERK_XTP|默认|94|  
|MEMORYCLERK_XTP|DB_ID_5|877|  
|MEMORYCLERK_XTP|默认|0|  
|MEMORYCLERK_XTP|默认|0|  
  
 默认内存分配器包含系统范围内存结构，相对较小。 用户数据库（在此例中是 ID 为 5 的数据库）的内存分配器大约为 900MB。  
  
#### <a name="memory-utilization-per-table"></a>每个表的内存利用率  
 以下查询可用于深化到各个表及其索引的内存利用率：  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
 下面显示此查询对于示例全新安装的结果：  
  
||||  
|-|-|-|  
|**表名**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SpecialOfferProduct_inmem|64|3840|  
|DemoSalesOrderHeaderSeed|1984|5504|  
|SalesOrderDetail_inmem|15316|663552|  
|DemoSalesOrderDetailSeed|64|10432|  
|SpecialOffer_inmem|3|8192|  
|SalesOrderHeader_inmem|7168|147456|  
|Product_inmem|124|12352|  
  
 可以看到，这些表相当小：SalesOrderHeader_inmem 的大小大约为 7MB，SalesOrderDetail_inmem 的大小大约为 15MB。  
  
 此处比较显著的是为索引分配的内存大小（与表数据大小相比）。 这是因为示例中的哈希索引针对较大数据大小预设了大小。 请注意，哈希索引有固定大小，因而其大小不会随表中的数据大小而增大。  
  
####  <a name="memory-utilization-after-running-the-workload"></a><a name="Memoryutilizationafterrunningtheworkload"></a> 运行工作负荷之后的内存利用率  
 插入 1000 万个销售订单之后，总体内存利用率类似于下面这样：  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|type|name|**pages_MB**|  
|MEMORYCLERK_XTP|默认|146|  
|MEMORYCLERK_XTP|DB_ID_5|7374|  
|MEMORYCLERK_XTP|默认|0|  
|MEMORYCLERK_XTP|默认|0|  
  
 可以看到， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将稍小于 8GB 的大小用于示例数据库中的内存优化表和索引。  
  
 在一次示例运行之后查看每个表的详细内存使用率：  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
||||  
|-|-|-|  
|**表名**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SalesOrderDetail_inmem|5113761|663552|  
|DemoSalesOrderDetailSeed|64|10368|  
|SpecialOffer_inmem|2|8192|  
|SalesOrderHeader_inmem|1575679|147456|  
|Product_inmem|111|12032|  
|SpecialOfferProduct_inmem|64|3712|  
|DemoSalesOrderHeaderSeed|1984|5504|  
  
 可以看到共有约 6.5GB 的数据。 请注意，表 SalesOrderHeader_inmem 和 SalesOrderDetail_inmem 上的索引大小与插入销售订单之前的索引大小相同。 索引大小未更改是因为这两个表都使用哈希索引，而哈希索引是静态的。  
  
#### <a name="after-demo-reset"></a>演示重置之后  
 存储过程 Demo.usp_DemoReset 可以用于重置演示。 它删除表 SalesOrderHeader_inmem 和 SalesOrderDetail_inmem 中的数据，并对原始表 SalesOrderHeader 和 SalesOrderDetail 中的数据重设种子。  
  
 现在，即使表中的行已删除，这也不意味着会立即回收内存。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 根据需要在后台从内存优化表中的已删除行回收内存。 可以看到，在演示重置之后（系统上没有事务工作负荷），尚未立即回收已删除行的内存：  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|type|name|**pages_MB**|  
|MEMORYCLERK_XTP|默认|2261|  
|MEMORYCLERK_XTP|DB_ID_5|7396|  
|MEMORYCLERK_XTP|默认|0|  
|MEMORYCLERK_XTP|默认|0|  
  
 这是预期行为：事务工作负荷运行时将回收内存。  
  
 如果启动演示工作负荷的第二次运行，可以看到内存利用率在开始时下降，因为以前删除的行会进行清理。 在某一时刻，内存大小会再次增大，直至工作负荷完成。 演示重置之后插入 1000 万行之后，内存利用率非常类似于第一次运行之后的利用率。 例如：  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|type|name|**pages_MB**|  
|MEMORYCLERK_XTP|默认|1863|  
|MEMORYCLERK_XTP|DB_ID_5|7390|  
|MEMORYCLERK_XTP|默认|0|  
|MEMORYCLERK_XTP|默认|0|  
  
### <a name="disk-utilization-for-memory-optimized-tables"></a>内存优化表的磁盘利用率  
 可以使用查询获得数据库检查点文件在给定时间的总体磁盘上大小：  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
  
```  
  
#### <a name="initial-state"></a>初始状态  
 最初创建示例文件组和示例内存优化表时，会预先创建一些检查点文件，并且系统开始填充这些文件 - 预先创建的检查点文件数取决于系统中的逻辑处理器数。 因为示例最初非常小，所以预先创建的文件在初始创建之后大部分为空。  
  
 下面是示例在有 16 个逻辑处理器的计算机上的初始磁盘上大小：  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**磁盘上大小 (MB)**|  
|2312|  
  
 可以看到，检查点文件的磁盘上大小 (2.3GB) 与实际数据大小（接近 30MB）之间存在巨大差异。  
  
 可以使用以下查询更详细地查看磁盘空间利用率的来源。 此查询返回的磁盘上大小与处于状态 5 (REQUIRED FOR BACKUP/HA)、6 (IN TRANSITION TO TOMBSTONE) 或 7 (TOMBSTONE) 的文件的大小接近。  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
 对于示例的初始状态，结果类似于下面这样（对于有 16 个逻辑处理器的服务器）：  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**计数**|**磁盘上大小 (MB)**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 可以看到，大部分空间由预先创建的数据和差异文件使用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 为每个逻辑处理器预先创建一对（数据、差异）文件。 此外，数据文件的预设大小为 128MB，差异文件的预设大小为 8MB，以便更高效地向这些文件插入数据。  
  
 内存优化表中的实际数据在单个数据文件中。  
  
#### <a name="after-running-the-workload"></a>运行工作负荷之后  
 进行插入 1000 万个销售订单的单次测试运行之后，总体磁盘上大小类似于下面这样（对于 16 核测试服务器）：  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**磁盘上大小 (MB)**|  
|8828|  
  
 磁盘上大小接近 9GB，这接近于数据的内存中大小。  
  
 更详细地查看各种状态间的检查点文件大小：  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**计数**|**磁盘上大小 (MB)**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 我们仍有 16 对预先创建的文件，准备好在关闭检查点时执行。  
  
 有一对尚在构造中，这一对会一直用到关闭当前检查点。 这一对与活动的检查点文件一起，对于内存中 6.5GB 的数据使用了 6.5GB 的磁盘。 请注意，索引不在磁盘上保存，因而在此例中，磁盘上的总体大小小于内存中的大小。  
  
#### <a name="after-demo-reset"></a>演示重置之后  
 演示重置之后，如果系统上没有事务工作负荷，则不会立即回收磁盘空间，并且没有数据库检查点。 对于要在其各个阶段中移动并最终丢弃的检查点文件，需要发生一些检查点和日志截断事件，以启动检查点文件合并以及启动垃圾收集。 如果在系统中具有事务工作负荷 [并且在使用完整恢复模式时进行定期日志备份]，则这些事件会自动发生，但是在系统处于空闲时不会自动发生（如演示方案所示）。  
  
 在示例中，演示重置之后，可能会出现如下内容  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**磁盘上大小 (MB)**|  
|11839|  
  
 差不多 12GB，这显著大于演示重置之前的 9GB。 这是因为某些检查点文件合并已启动，但是某些合并目标尚未安装，某些合并源文件尚未清理，如下所示：  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**计数**|**磁盘上大小 (MB)**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|ACTIVE|DATA|38|5152|  
|ACTIVE|DELTA|38|1331|  
|MERGE TARGET|DATA|7|896|  
|MERGE TARGET|DELTA|7|56|  
|MERGED SOURCE|DATA|13|1772|  
|MERGED SOURCE|DELTA|13|455|  
  
 事务活动在系统中进行时，合并目标会进行安装，合并源会进行清理。  
  
 第二次运行演示工作负荷（演示重置之后插入 1000 万个销售订单）之后，可以看到在第一次运行工作负荷过程中构造的文件已清理。 如果在工作负荷运行期间多次运行以上查询，则可以查看检查点文件在各个阶段间移动。  
  
 第二次运行工作负荷（插入 1000 万个销售订单）之后，可以看到磁盘利用率非常类似于第一次运行之后的情况（不过不一定相同，因为系统在本质上是动态的）。 例如：  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**计数**|**磁盘上大小 (MB)**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|2|268|  
|UNDER CONSTRUCTION|DELTA|2|16|  
|ACTIVE|DATA|41|5608|  
|ACTIVE|DELTA|41|328|  
  
 在此例中，有两个检查点文件对处于“尚在构造”状态，这意味着多个文件对已变为“尚在构造”状态（可能是因为工作负荷的并发级别较高）。 多个并发线程同时需要一个新文件对，因而将一对从“预先创建”变为“尚在构造”。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
