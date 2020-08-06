---
title: CLR 用户定义类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
ms.openlocfilehash: e4e19323eeac9e0a1148924543f71aa7de5619b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591405"
---
# <a name="clr-user-defined-types"></a>CLR 用户定义类型
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于创建基于以 .NET Framework 公共语言运行时 (CLR) 创建的程序集而编写的数据库对象。 数据库对象包括触发器、存储过程、函数、聚合函数和类型，它们可以利用 CLR 提供的丰富的编程模型。  
  
> [!NOTE]  
>  默认情况下，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中关闭了执行 CLR 代码的功能。 可以使用**sp_configure**系统存储过程来启用 CLR。  
  
 从开始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，你可以使用用户定义的类型 (udt) 来扩展服务器的标量类型系统，从而能够在数据库中存储 CLR 对象 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 UDT 可以包含多个元素，还可以有行为，这使它们与由单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型组成的传统别名数据类型区分开来。  
  
 因为 UDT 作为整体供系统访问，所以其对复杂数据类型的使用可能会对性能有负面影响。 通常，使用传统的行和表可以对复杂数据进行最佳建模。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 UDT 非常适合以下各项：  
  
-   日期、时间、货币和扩展数字类型  
  
-   地理空间应用程序  
  
-   编码或加密数据  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中开发 UDT 的过程由以下步骤组成：  
  
1.  **编码和生成定义 UDT 的程序集。** 使用生成可验证代码的 .NET Framework 公共语言运行时 (CLR) 所支持的任何语言都可以定义 UDT， 这包括 Visual C# 和 Visual Basic .NET。 数据作为 .NET Framework 类或结构的字段和属性公开，其行为由类或结构的方法定义。  
  
2.  **注册程序集。** 可以通过在数据库项目中使用 Visual Studio 用户界面，或通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY 语句（该语句将包含类或结构的程序集复制到数据库中），来部署 UDT。  
  
3.  **在 SQL Server 中创建 UDT。** 一旦程序集加载到宿主数据库中，则使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE 语句创建 UDT，并将该类或结构的成员作为此 UDT 的成员公开。 UDT 仅在单个数据库的上下文中存在，一旦注册，则不依赖于从其创建它们的外部文件。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前，不支持从 .NET Framework 程序集创建的 UDT。 不过，你仍然可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sp_addtype**来使用别名数据类型。 本机 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户定义数据类型和 UDT 都可以用 CREATE TYPE 语法创建。  
  
4.  **使用 UDT 创建表、变量或参数**从开始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，用户定义类型可用作表的列定义、批处理中的变量 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，或者用作 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数或存储过程的参数。  
  
## <a name="in-this-section"></a>本节内容  
 [创建用户定义类型](creating-user-defined-types.md)  
 描述如何创建 UDT。  
  
 [在 SQL Server 中注册用户定义类型](registering-user-defined-types-in-sql-server.md)  
 描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册和管理 UDT。  
  
 [使用 SQL Server 中的用户定义类型](working-with-user-defined-types-in-sql-server.md)  
 描述如何使用 UDT 创建查询。  
  
 [在 ADO.NET 中访问用户定义类型](accessing-user-defined-types-in-ado-net.md)  
 描述如何在 ADO.NET 中使用用于 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来处理 UDT。  
  
  
