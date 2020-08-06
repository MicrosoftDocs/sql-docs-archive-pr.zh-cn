---
title: BLOB 和 OLE 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: rothja
ms.author: jroth
ms.openlocfilehash: 15f8b4915ba9b05a5be19854a2e27a2e8ff3a346
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693800"
---
# <a name="blobs-and-ole-objects"></a>BLOB 和 OLE 对象
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序公开了**ISequentialStream**接口，以支持使用者访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**、 **text**、 **image**、 **varchar (max) **、 **nvarchar (max) **、 **varbinary (max) **和 xml 数据类型为二进制大型对象 (blob) 。 通过对 ISequentialStream 执行 Read 方法，使用者可以用便于管理的方式成块检索大量数据********。  
  
 有关演示此功能的示例，请参阅[设置大型数据 (OLE DB)](../native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]当使用者在访问器中提供用于数据修改的接口指针时，Native Client OLE DB 提供程序可以使用使用者实现的**IStorage**接口。  
  
 对于大值数据类型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序检查**IROWSET**和 DDL 接口中的类型大小假设。 使用最大大小设置为 "无限制" 的**varchar**、 **nvarchar**和**varbinary**数据类型的列将通过架构行集和返回列数据类型的接口表示为 ISLONG。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序以) 、 (和) 分别公开**varchar (max) **、 **varbinary (max DBTYPE_STR**和**nvarchar DBTYPE_BYTES 最**大 DBTYPE_WSTR 类型。  
  
 若要使用这些类型，应用程序具有以下选项：  
  
-   绑定为字节（DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR）。 如果缓冲区不够大，将发生截断，这与早期版本中的这些类型完全相同（但是现在可以使用更大的值）。  
  
-   绑定为字节并指定 DBTYPE_BYREF。  
  
-   绑定为 DBTYPE_IUNKNOWN 并使用流处理。  
  
 如果绑定为 DBTYPE_IUNKNOWN，则使用 ISequentialStream 流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持将输出参数绑定为大值数据类型的 DBTYPE_IUNKNOWN，以便于在某些情况下，存储过程将这些数据类型作为返回值返回，并将其作为 DBTYPE_IUNKNOWN 公开给客户端。  
  
## <a name="storage-object-limitations"></a>存储对象限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序只能支持一个打开的存储对象。 尝试打开多个存储对象（以获取对多个 ISequentialStream 接口指针的引用）返回 DBSTATUS_E_CANTCREATE****。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序中，DBPROP_BLOCKINGSTORAGEOBJECTS 只读属性的默认值 VARIANT_TRUE。 这指示如果存储对象处于活动状态，某些方法（存储对象上的方法除外）将失败，并返回 E_UNEXPECTED。  
  
-   当创建引用存储对象的行访问器时，必须将由使用者实现的存储对象提供的数据的长度识别为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序。 使用者必须在用于创建取值函数的 DBBINDING 结构中绑定一个长度指示符。  
  
-   如果行包含多个大数据值且未 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，则使用者必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持游标的行集来检索行数据或处理所有大数据值，然后再检索其他行值。 如果 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序会将所有 xml 数据类型缓存为 () blob 的二进制大型对象，以便可以按任意顺序访问该数据类型。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [获取大型数据](getting-large-data.md)  
  
-   [设置大型数据](setting-large-data.md)  
  
-   [BLOB 输出参数的流支持](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大值类型](../native-client/features/using-large-value-types.md)  
  
  
