---
title: 将文件加载到 FileTable 中 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 43ea31523da2dfa8b387f68ce4f7c7f07868dd6f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692965"
---
# <a name="load-files-into-filetables"></a>将文件加载到 FileTable 中
  说明如何将文件加载或迁移到 FileTable 中。  
  
##  <a name="loading-or-migrating-files-into-a-filetable"></a><a name="BasicsLoadNew"></a> 将文件加载或迁移到 FileTable  
 您选择用于将文件加载或迁移到 FileTable 的方法取决于当前存储文件的位置。  
  
|文件的当前位置|用于迁移的选项|  
|-------------------------------|---------------------------|  
|文件当前存储在文件系统中。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不识别文件。|由于 FileTable 显示为 Windows 文件系统中的文件夹，您可以使用移动或复制文件的任何方法轻松地将文件加载到新的 FileTable。 这些方法包括 Windows 资源管理器、包括 xcopy 和 robocopy 在内的命令行选项，以及自定义脚本或应用程序。<br /><br /> 不能将现有文件夹转换为 FileTable。|  
|文件当前存储在文件系统中。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含一个元数据表，该表中包含指向文件的指针。|第一步是使用上文所述的方法之一移动或复制文件。<br /><br /> 第二步是更新现有元数据的表以指向该文件的新位置。<br /><br /> 有关详细信息，请参阅本主题中的 [示例：将文件从文件系统迁移到 FileTable](#HowToMigrateFiles) 。|  
  
###  <a name="how-to-load-files-into-a-filetable"></a><a name="HowToLoadNew"></a> 如何：将文件加载到 FileTable 中  
 可用于将文件加载到 FileTable 的方法包括：  
  
-   在 Windows 资源管理器中将文件从源文件夹拖放到新的 FileTable 文件夹。  
  
-   从命令提示符下、批处理文件或脚本中使用命令行选项（如 MOVE、COPY、XCOPY 或 ROBOCOPY）。  
  
-   用 C# 或 Visual Basic.NET 编写一个自定义应用程序，该应用程序使用 **System.IO** 命名空间的方法来移动或复制文件。  
  
###  <a name="example-migrating-files-from-the-file-system-into-a-filetable"></a><a name="HowToMigrateFiles"></a> 示例：将文件从文件系统迁移到 FileTable  
 在这种情况下，您的文件存储在文件系统中，并且您具有包含指向这些文件的指针的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的元数据表。 您要将文件移入 FileTable，然后用 FileTable UNC 路径替换元数据中每个文件的原始 UNC 路径。 [GetPathLocator (Transact-SQL)](/sql/relational-databases/system-functions/getpathlocator-transact-sql) 函数帮助你实现这一目标。  
  
 在此示例中，假设存在一个 `PhotoMetadata` 包含有关照片的数据的现有数据库表。 该表具有 `varchar`(512) 类型的 `UNCPath` 列，其中包含指向 .jpg 文件的实际 UNC 路径。  
  
 要将图像文件从文件系统迁移到 FileTable，必须执行以下操作：  
  
1.  创建新的 FileTable 来保存文件。 此示例将使用表名 `dbo.PhotoTable`，但不显示用来创建该表的代码。  
  
2.  使用 xcopy 或类似的工具将 .jpg 文件连同目录结构一起复制到 FileTable 的根目录下。  
  
3.  通过使用类似于以下内容的代码修复 `PhotoMetadata` 表中的元数据：  
  
```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="bulk-loading-files-into-a-filetable"></a><a name="BasicsBulkLoad"></a> 大容量加载文件到 FileTable  
 对于大容量操作，FileTable 在行为上与普通表相似，但具有以下限制。  
  
 FileTable 具有系统定义的约束，这些约束确保维护文件和目录命名空间的完整性。 必须针对大容量加载到 FileTable 上的数据验证这些约束。 因为一些大容量插入操作允许忽略表约束，所以将强制以下要求。  
  
-   强制执行约束的大容量加载操作可以像对任何其他表一样对 FileTable 运行。 此类别包括下列操作：  
  
    -   带 CHECK_CONSTRAINTS 子句的 bcp。  
  
    -   带 CHECK_CONSTRAINTS 子句的 BULK INSERT。  
  
    -   INSERT INTO... 不带 IGNORE_CONSTRAINTS 子句的 SELECT * FROM OPENROWSET(BULK …)。  
  
-   不强制执行约束的大容量加载操作将失败，除非 FileTable 系统定义的约束已禁用。 此类别包括下列操作：  
  
    -   不带 CHECK_CONSTRAINTS 子句的 bcp。  
  
    -   不带 CHECK_CONSTRAINTS 子句的 BULK INSERT。  
  
    -   INSERT INTO... 带 IGNORE_CONSTRAINTS 子句的 SELECT * FROM OPENROWSET(BULK …)。  
  
###  <a name="how-to-bulk-load-files-into-a-filetable"></a><a name="HowToBulkLoad"></a> 如何：将文件批量到 FileTable  
 您可以使用各种方法来大容量加载文件到 FileTable：  
  
-   **bcp**  
  
    -   使用 **CHECK_CONSTRAINTS** 子句调用。  
  
    -   禁用 FileTable 命名空间并不使用 **CHECK_CONSTRAINTS** 子句调用。 然后重新启用 FileTable 命名空间。  
  
-   **BULK INSERT**  
  
    -   使用 **CHECK_CONSTRAINTS** 子句调用。  
  
    -   禁用 FileTable 命名空间并不使用 **CHECK_CONSTRAINTS** 子句调用。 然后重新启用 FileTable 命名空间。  
  
-   **INSERT INTO ...SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   使用 **IGNORE_CONSTRAINTS** 子句调用。  
  
    -   禁用 FileTable 命名空间并不使用 **IGNORE_CONSTRAINTS** 子句调用。 然后重新启用 FileTable 命名空间。  
  
 有关禁用 FileTable 约束的信息，请参阅 [管理 FileTables](manage-filetables.md)。  
  
###  <a name="how-to-disable-filetable-constraints-for-bulk-loading"></a><a name="disabling"></a> 如何：禁用针对批量加载的 FileTable 约束  
 若要在没有强制系统定义约束的开销的情况下将文件大容量加载到 FileTable 中，可以暂时禁用约束。 有关详细信息，请参阅 [管理 FileTables](manage-filetables.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Transact-SQL 访问 FileTable](access-filetables-with-transact-sql.md)   
 [使用文件输入输出 API 访问 FileTable](access-filetables-with-file-input-output-apis.md)  
  
  
