---
title: 数据库存储位置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], storage location
ms.assetid: cf88c62e-581e-42f2-846f-a9bf1d7c3292
author: minewiskan
ms.author: owend
ms.openlocfilehash: ab370889396f40f52a348523e7f268892f549192
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689057"
---
# <a name="database-storage-location"></a>数据库存储位置
  通常会出现这样的情况， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库管理员 (dba) 希望某个数据库驻留在服务器数据文件夹之外。 这些情况通常是由于业务需要，如提高性能或扩展存储。 对于这些情况， `DbStorageLocation` 数据库属性使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 能够指定本地磁盘或网络设备中的数据库位置。  
  
## <a name="dbstoragelocation-database-property"></a>DbStorageLocation 数据库属性  
 `DbStorageLocation` 数据库属性指定了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建和管理所有数据库数据和元数据文件的文件夹。 除数据库元数据文件之外（它存储在服务器数据文件夹中），所有元数据文件都存储在 `DbStorageLocation` 文件夹中。 在设置 `DbStorageLocation` 数据库属性的值时，需考虑两个重要的注意事项：  
  
-   必须将 `DbStorageLocation` 数据库属性设置为现有 UNC 文件夹路径或空字符串。 空字符串是服务器数据文件夹的默认值。 如果该文件夹不存在，则在执行 `Create`、`Attach`、或 `Alter` 命令时会产生错误。  
  
-   不能将 `DbStorageLocation` 数据库属性设置为指向服务器数据文件夹或它的任何一个子文件夹。 如果该位置指向服务器数据文件夹或它的任何一个子文件夹，则在执行 `Create`、`Attach`、或 `Alter` 命令时会产生错误。  
  
> [!IMPORTANT]  
>  建议您设置 UNC 路径以使用存储区域网络 (SAN)、基于 iSCSI 的网络或本地附加的磁盘。 网络共享的任何 UNC 路径或任何长滞后时间远程存储解决方案导致不支持的安装.  
  
### <a name="dbstoragelocation-compared-to-storagelocation"></a>相对于 StorageLocation 的 DbStorageLocation  
 `DbStorageLocation` 指定了所有数据库数据和元数据文件所在的文件夹，而 `StorageLocation` 指定了多维数据集的一个或多个分区所在的文件夹。 `StorageLocation` 可以独立于 `DbStorageLocation` 进行设置。 这是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 根据预期的结果做出的决定，很多时候一个属性或另一个属性的使用会重叠。  
  
## <a name="dbstoragelocation-usage"></a>DbStorageLocation 用法  
 在数据库命令 `DbStorageLocation` `Create` `Detach` / `Attach` 序列、 `Backup` / `Restore` 数据库命令序列或 `Synchronize` 数据库命令中，将数据库属性用作数据库命令的一部分。 更改 `DbStorageLocation` 数据库属性被认为是数据库对象的结构更改。 这意味着必须重新创建所有元数据并且重新处理数据。  
  
> [!IMPORTANT]  
>  不应使用 `Alter` 命令更改数据库存储位置。 相反，我们建议你使用一系列 `Detach` / `Attach` 数据库命令 (参阅[移动 Analysis Services 数据库](move-an-analysis-services-database.md)、[附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)) 。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft.analysisservices.sharepoint.integration.dll. DbStorageLocation *](/dotnet/api/microsoft.analysisservices.core.database.dbstoragelocation)   
 [附加和分离 Analysis Services 数据库](attach-and-detach-analysis-services-databases.md)   
 [移动 Analysis Services 数据库](move-an-analysis-services-database.md)   
 [DbStorageLocation 元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)   
 [&#40;XMLA&#41;创建元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)   
 [附加元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Synchronize 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla)  
  
  
