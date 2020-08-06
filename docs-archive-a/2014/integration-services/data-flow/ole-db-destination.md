---
title: OLE DB 目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdest.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5227175e80db3a8f31a8b8db8c3d6bee3061bae
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579674"
---
# <a name="ole-db-destination"></a>OLE DB 目标
  OLE DB 目标用数据库表或视图或者用 SQL 命令，将数据加载到各种符合 OLE DB 的数据库中。 例如，OLE DB 源可以将数据加载到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表中。  
  
 OLE DB 目标为数据加载提供了五种数据访问模式：  
  
-   表或视图。 可以指定现有的表或视图，也可以创建新表。  
  
-   使用快速加载选项的表或视图。 可以指定现有的表或者创建新表。  
  
-   变量中指定的表或视图。  
  
-   使用快速加载选项在变量中指定的表或视图。  
  
-   SQL 语句的运行结果。  
  
> [!NOTE]  
>  OLE DB 目标不支持参数。 如果需要执行参数化 INSERT 语句，请考虑使用 OLE DB 命令转换。 有关详细信息，请参阅 [OLE DB Command Transformation](transformations/ole-db-command-transformation.md)。  
  
 当 OLE DB 目标加载使用双字节字符集 (DBCS) 的数据时，如果没有使用快速加载选项的数据访问模式，并且 OLE DB 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB)，则该数据可能会被损坏。 为了确保 DBCS 数据的完整性，应将 OLE DB 连接管理器配置为使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 或使用以下任一快速加载访问模式：“表或视图 - 快速加载”  或“表名称或视图名称变量 - 快速加载”  。 这两个选项都可以在 **“OLE DB 目标编辑器”** 对话框中使用。 在对对象模型进行编程时 [!INCLUDE[ssIS](../../includes/ssis-md.md)] ，应将 AccessMode 属性设置为 `OpenRowset Using FastLoad` 、或 `OpenRowset Using FastLoad From Variable` 。  
  
> [!NOTE]  
>  如果用 **设计器中的** “OLE DB 目标编辑器” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 对话框创建 OLE DB 目标要向其插入数据的目标表，可能需要手动选择新创建的表。 当 OLE DB 访问接口（如 OLE DB Provider for DB2）自动将架构标识符添加到表名称时，需要进行手动选择。  
  
> [!NOTE]  
>  **“OLE DB 目标编辑器”** 对话框生成的 CREATE TABLE 语句可能需要修改，具体取决于目标类型。 例如，某些目标不支持 CREATE TABLE 语句所使用的数据类型。  
  
 此目标使用 OLE DB 连接管理器连接数据源，该连接管理器指定要使用的 OLE DB 访问接口。 有关详细信息，请参阅 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目还提供了可从中创建 OLE DB 连接管理器的数据源对象，使数据源和数据源视图可用于 OLE DB 目标。  
  
 OLE DB 目标包括输入列和目标数据源中的列之间的映射。 您不必将输入列映射到所有目标列，但有时如果没有将输入列映射到目标列可能会出错，具体取决于目标列的属性。 例如，如果目标列不允许出现 Null 值，则必须将输入列映射到该列。 另外，映射的列的数据类型必须是兼容的。 例如，不能将数据类型为字符串的输入列映射到数据类型为数值的目标列。  
  
 OLE DB 目标具有一个常规输入和一个错误输出。  
  
 有关数据类型的详细信息，请参阅 [Integration Services Data Types](integration-services-data-types.md)。  
  
## <a name="fast-load-options"></a>快速加载选项  
 如果 OLE DB 目标使用快速加载数据访问模式，则可以在用户界面“OLE DB 目标编辑器”  中为目标指定以下快速加载选项：  
  
-   保持导入数据文件的标识值或使用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]分配的唯一值。  
  
-   在大容量加载操作过程中保留 Null 值。  
  
-   在大容量导入操作过程中检查目标表或视图的约束。  
  
-   在大容量加载操作期间获取表级锁。  
  
-   指定批中的行数和提交大小。  
  
 某些快速加载选项存储在 OLE DB 目标的特定属性中。 例如，FastLoadKeepIdentity 指定是否保持标识值，FastLoadKeepNulls 指定是否保持 Null 值，而 FastLoadMaxInsertCommitSize 则指定作为批提交的行数。 其他快速加载选项则存储在 FastLoadOptions 属性内的以逗号分隔的列表中。 如果 OLE DB 目标使用存储在 FastLoadOptions 中并在 " **OLE DB 目标编辑器**" 对话框中列出的所有快速加载选项，则该属性的值将设置为 `TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000` 。 值 1000 指示已将目标配置为使用 1000 行组成的批。  
  
> [!NOTE]  
>  目标中任何约束失败都将导致 FastLoadMaxInsertCommitSize 所定义的整批行失败。  
  
 除了在“OLE DB 目标编辑器”  对话框中公开的快速加载选项以外，还可以通过在“高级编辑器”  对话框的 FastLoadOptions 属性中键入选项，将 OLE DB 目标配置为使用以下大容量加载选项。  
  
|快速加载选项|说明|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|指定要插入的大小 (KB)。 选项的格式为 `KILOBYTES_PER_BATCH`  =  \<positive integer value**> * *。|  
|FIRE_TRIGGERS|指定是否在插入表上激发触发器。 选项的格式为 **FIRE_TRIGGERS**。 出现该选项说明要激发触发器。|  
|ORDER|指定输入数据如何排序。 选项格式为 ORDER \<column name> ASC&#124;DESC。 可以列出任何列数，是否包括排序顺序是可选的。 如果省略排序顺序，则插入操作假定数据不排序。<br /><br /> 注意：如果使用 ORDER 选项根据表中的聚集索引对输入数据进行排序，可以提升性能。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 关键字传统上采用大写字母键入，但并不区分大小写。  
  
 若要了解快速加载选项的详细信息，请参阅[BULK INSERT (Transact-SQL)](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
## <a name="troubleshooting-the-ole-db-destination"></a>OLE DB 目标故障排除  
 可以记录 OLE DB 目标对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 OLE DB 目标在执行将数据保存到外部数据源的操作进行故障排除。 若要记录 OLE DB 目标对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-destination"></a>配置 OLE DB 目标  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 **“OLE DB 目标编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [OLE DB 目标编辑器（“连接管理器”页）](../ole-db-destination-editor-connection-manager-page.md)  
  
-   [OLE DB 目标编辑器（“映射”页）](../ole-db-destination-editor-mappings-page.md)  
  
-   [OLE DB 目标编辑器（“错误输出”页）](../ole-db-destination-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 自定义属性](ole-db-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [通过使用 OLE DB 目标来加载数据](ole-db-destination.md)  
  
-   [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
 [OLE DB 源](ole-db-source.md)  
  
 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)  
  
 [数据流](data-flow.md)  
  
  
