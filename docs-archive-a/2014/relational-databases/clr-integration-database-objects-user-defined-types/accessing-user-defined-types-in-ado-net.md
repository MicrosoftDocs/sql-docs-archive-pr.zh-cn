---
title: 在 ADO.NET 中访问用户定义类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: a94e333ad743ed07dff6b973ebfe227312a1cab2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589144"
---
# <a name="accessing-user-defined-types-in-adonet"></a>在 ADO.NET 中访问用户定义类型
   (Udt) 的用户定义类型是使用 .NET Framework 公共语言运行时支持的任何一种语言编写的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ， (CLR) 生成可验证代码。 这包括 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic。 使用 UDT 可在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储对象和自定义数据结构。 数据公开为 .NET Framework 类或结构的公共成员，行为则由类或结构的方法来定义。 UDT 可用作表的列定义、[!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的变量，还可用作 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或存储过程的参数。  
  
 在 ADO.NET 中，`System.Data.SqlClient` 访问接口以如下方式公开 UDT：  
  
-   作为对象通过 `System.Data.SqlClient.SqlDataReader`。  
  
-   作为原始字节通过 `SqlDataReader`。  
  
-   作为 `System.Data.SqlClient.SqlParameter` 对象的参数。  
  
## <a name="in-this-section"></a>本节内容  
 [检索 UDT 数据](accessing-user-defined-types-retrieving-udt-data.md)  
 介绍如何检索 UDT 数据和如何指定参数。  
  
 [使用 DataAdapter 更新 UDT 列](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 介绍如何在 `DataSets` 中使用 UDT 以及如何使用 `DataAdapters` 更新 UDT 数据。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](clr-user-defined-types.md)  
  
  
