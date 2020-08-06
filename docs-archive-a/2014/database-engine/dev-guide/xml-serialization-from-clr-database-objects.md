---
title: 从 CLR 数据库对象进行 XML 序列化 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ee93ee4b7bf9cba3f11b329244d4523636cb7704
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690061"
---
# <a name="xml-serialization-from-clr-database-objects"></a>从 CLR 数据库对象进行 XML 序列化
  XML 序列化是以下两种情况所必需的：  
  
-   从公共语言运行时 (CLR) 对象调用 Web 服务。  
  
-   将用户定义类型 (UDT) 转换为 XML。  
  
 通过调用 `XmlSerializer` 类执行 XML 序列化通常将生成一个附加的序列化程序集，该程序集将重载到具有源程序集的项目中。 但出于安全原因，此重载在 CLR 中被禁用。 因此，若要调用 web 服务或执行从 UDT 到 XML 的转换 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，必须使用一个名为 .NET Framework **Sgen.exe**的工具手动创建该程序集，该工具可生成所需的序列化程序集。 在调用 `XmlSerializer` 时，必须通过以下步骤手动创建序列化程序集：  
  
1.  运行与 .NET Framework SDK 一起提供的**Sgen.exe**工具，以创建包含源程序集的 XML 序列化程序的程序集。  
  
2.  使用 `CREATE ASSEMBLY` 语句在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册生成的程序集。  
  
 有关在执行 XML 序列化时可能收到的错误的信息，请参阅以下 Microsoft 支持部门文章： ["无法加载动态生成的序列化程序集"](https://support.microsoft.com/kb/913668)。  
  
 有关 XML 序列化程序不支持的数据类型的信息，请参阅 .NET Framework 文档中的“.NET Framework 中 XML 架构的绑定支持”。  
  
## <a name="see-also"></a>另请参阅  
 [从 CLR 数据库对象进行数据访问](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
