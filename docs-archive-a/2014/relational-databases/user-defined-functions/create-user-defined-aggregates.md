---
title: 创建用户定义聚合 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
ms.openlocfilehash: c91179cb194bbfb79e8e7a8476e9725877b88afa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693229"
---
# <a name="create-user-defined-aggregates"></a>创建用户定义聚合
  您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建在 CLR 程序集中进行编程的数据库对象。 能够利用由 CLR 提供的众多编程模型的数据库对象包括触发器、存储过程、函数、聚合函数和类型。  
  
 与 [!INCLUDE[tsql](../../includes/tsql-md.md)]中提供的内置聚合函数一样，用户定义聚合函数对一组值进行计算，然后返回单个值。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建用户定义聚合函数包括下列步骤：  
  
-   用一种 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 语言将用户定义聚合函数定义为类。 有关如何在 CLR 中编写用户定义聚合函数的详细信息，请参阅 [CLR 用户定义聚合函数](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)。 使用适当的语言编译器编译此类，以生成 CLR 程序集。  
  
-   使用 CREATE ASSEMBLY 语句在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中注册程序集。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的程序集的详细信息，请参阅[程序集（数据库引擎）](../clr-integration/assemblies-database-engine.md)。  
  
-   使用 CREATE AGGREGATE 语句创建引用已注册程序集的用户定义聚合函数。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 中部署 SQL Server 项目将在为该项目指定的数据库中注册程序集。 部署项目还会在数据库中为使用 `SqlUserDefinedAggregate` 属性注释的所有类定义创建用户定义聚合。 有关详细信息，请参阅 [Deploying CLR Database Objects](../clr-integration/deploying-clr-database-objects.md)。  
  
> [!NOTE]  
>  默认情况下，关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 执行 CLR 代码的功能。 可以创建、更改和删除将引用托管代码模块的数据库对象，但是不能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行这些引用，除非使用 [sp_configure (Transact-SQL)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) 启用了 [clr enabled](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)选项。  
  
 **创建、修改或删除程序集**  
  
-   [CREATE ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **创建用户定义聚合函数**  
  
-   [CREATE AGGREGATE (Transact-SQL)](/sql/t-sql/statements/create-aggregate-transact-sql)  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 (CLR) 集成编程概念](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
