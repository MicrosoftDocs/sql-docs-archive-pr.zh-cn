---
title: 创建 CLR 触发器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 3afd841b4f1f9ca567a93c0a20c0a7609a5b45e2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590648"
---
# <a name="create-clr-triggers"></a>创建 CLR 触发器
  可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建可在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时 (CLR) 中创建的程序集中进行编程的数据库对象。 可以利用由 CLR 提供的大量编程模型的数据库对象包括 DML 触发器、DDL 触发器、存储过程、函数、聚合函数和类型。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建 CLR 触发器（DML 或 DDL）包括以下步骤：  
  
-   使用 .NET Framework 支持的语言将触发器定义为类。 有关如何在 CLR 中对触发器进行编程的详细信息，请参阅 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。 然后，使用相应的语言编译器编译该类，在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中生成程序集。  
  
-   使用 CREATE ASSEMBLY 语句在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的程序集的详细信息，请参阅[程序集（数据库引擎）](../clr-integration/assemblies-database-engine.md)。  
  
-   创建用于引用已注册的程序集的触发器。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中部署 SQL Server 项目将在为该项目指定的数据库中注册程序集。 部署项目也还会在数据库中为所有使用 `SqlTrigger` 属性批注的方法创建 CLR 触发器。 有关详细信息，请参阅 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)。  
  
> [!NOTE]  
>  默认情况下，关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行 CLR 代码的功能。 可以创建、更改和删除引用托管代码模块的数据库对象，但是只有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_configure (Transact-SQL) [启用了](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) clr enabled 选项 [，才能在](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)中执行这些引用。  
  
 **创建、修改或删除程序集**  
  
-   [CREATE ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **创建 CLR 触发器**  
  
-   [CREATE TRIGGER (Transact-SQL)](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>另请参阅  
 [DML 触发器](dml-triggers.md)   
 [公共语言运行时 (CLR) 集成编程概念](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [从 CLR 数据库对象进行数据访问](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
