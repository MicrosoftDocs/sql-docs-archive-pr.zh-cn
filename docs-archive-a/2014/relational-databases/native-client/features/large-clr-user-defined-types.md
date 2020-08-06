---
title: 大型 CLR 用户定义类型 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types
ms.assetid: b65eb61d-ccf6-49c0-98e7-9a4ef4b2f790
author: rothja
ms.author: jroth
ms.openlocfilehash: 27f0c13caea8c4aca63d78238509c6d05f1bf7bf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688871"
---
# <a name="large-clr-user-defined-types"></a>大型 CLR 用户定义类型
  在 SQL Server 2005 中，公共语言运行时 (CLR) 中的用户定义类型 (UDT) 已限制为最大 8,000 字节。 这一限制在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更高版本中已取消。 CLR UDT 现在以针对大型对象 (LOB) 类型的类似方式处置。 也就是说，小于或等于 8,000 字节的 UDT 在行为上与 SQL Server 2005 中相同，但支持更大的 UDT 并且将其大小报告为“无限制”。  
  
 有关详细信息，请参阅 &#40;OLE DB&#41;和[大型 Clr 用户定义类型 &#40;ODBC&#41;](../odbc/large-clr-user-defined-types-odbc.md)中的[大型 Clr 用户定义类型](../ole-db/large-clr-user-defined-types-ole-db.md)。  
  
## <a name="use-cases"></a>用例  
 对于 ODBC，对大型 UDT 的支持包括能够分块将 UDT 值作为执行时数据参数发送。 这可以通过使用 SQLPutData 来完成。  
  
 对于 OLE DB，对大型 UDT 的支持包括能够通过使用 ISequentialStream 绑定在服务器之间传送 UDT 值。  
  
 小于或等于 8,000 字节的 UDT 在行为上与 SQL Server 2005 中相同。 对于 OLE DB，仍可以通过使用 ISequentialStream 绑定来流式传输小型 UDT。  
  
 有时候，本机代码将必须理解 CLR UDT 的内容，但将不必实例化托管对象。 在此情况下，您可以使用自定义序列化将服务器上的 UDT 值转换为客户端的已知格式。  
  
 对于具有现有数据访问代码的应用程序，您可以通过在本机 API 中检索 UDT 并通过在混合模式应用程序中使用 C++ CLI interop 实例化它们，在客户端上利用 CLR UDT 行为。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  
