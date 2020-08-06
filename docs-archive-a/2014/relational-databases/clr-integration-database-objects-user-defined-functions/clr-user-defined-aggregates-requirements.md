---
title: CLR 用户定义聚合的要求 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 8123f8324d43212007857dbb596a4fc61872bd2e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587429"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>CLR 用户定义聚合的要求
  只要公共语言运行时 (CLR) 程序集中的类型实现了所需的聚合约定，就可以将它作为用户定义聚合函数注册。 此约定由 `SqlUserDefinedAggregate` 属性和聚合约定方法组成。 聚合约定包括保存聚合中间状态的机制以及累计新值的机制，它由四个方法组成：`Init`、`Accumulate`、`Merge` 和 `Terminate`。 满足这些要求后，你将能够在中充分利用用户定义的聚合 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 本主题的以下章节提供有关如何创建和使用用户定义聚合的其他详细信息。 有关示例，请参阅[调用 CLR 用户定义聚合函数](clr-user-defined-aggregate-invoking-functions.md)。  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 有关详细信息，请参阅[SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="aggregation-methods"></a>聚合方法  
 注册为用户定义聚合的类应支持以下实例方法。 这些是查询处理器计算聚合所用的方法。  
  
|方法|语法|说明|  
|------------|------------|-----------------|  
|`Init`|公共 void Init ( # A1;|查询处理器使用此方法初始化聚合的计算。 对于查询处理器正在聚合的每个组调用此方法一次。 查询处理器可以选择重用聚合类的同一实例来计算多个组的聚合。 `Init` 方法应在上一次使用此实例后根据需要执行清除，并允许重新启动新的聚合计算。|  
|`Accumulate`|公共 void 累积 ( 输入类型值 [，输入类型值，...]) ;|表示该函数的参数的一个或多个参数。 *input_type*应是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等效于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句中*input_sqltype*指定的本机数据类型的托管数据类型 `CREATE AGGREGATE` 。 有关详细信息，请参阅[映射 CLR 参数数据](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。<br /><br /> 对于用户定义类型 (UDT)，input-type 与 UDT 类型相同。 查询处理器使用此方法累计聚合值。 对于正在聚合的组中的每个值调用此方法一次。 查询处理器仅在为聚合类的指定实例调用 `Init` 方法之后才调用此方法。 此方法的实现应更新实例的状态以反映正在传递的参数值的累计。|  
|`Merge`|公共 void Merge ( udagg_class 值) ;|此方法可以将此聚合的另一实例与当前实例合并。 查询处理器使用此方法合并聚合的多个部分计算。|  
|`Terminate`|public return_type 终止 ( # A1;|此方法完成聚合计算并返回聚合的结果。 *Return_type*应为托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，该类型是语句中指定的*return_sqltype*的托管等效项 `CREATE AGGREGATE` 。 *Return_type*也可以是用户定义的类型。|  
  
### <a name="table-valued-parameters"></a>表值参数  
 表值参数 (TVP) 即传递到某一过程或函数的用户定义表类型，它提供了一种将多行数据传递到服务器的高效方法。 TVP 提供与参数数组类似的功能，但灵活性更高并且与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的集成更紧密。 它们还提供提升性能的潜力。 TVP 还有助于减少到服务器的往返次数。 可以将数据作为 TVP 发送到服务器，而不是向服务器发送多个请求（例如，对于标量参数列表）。 用户定义表类型不能作为表值参数传递到在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数，也不能从这些存储过程或函数中返回。 而且，TVP 不能在上下文连接的作用域内使用。 但是，如果在非上下文连接中使用 TVP，则 TVP 可用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中执行的托管存储过程或函数中的 SqlClient。 该连接可以是对执行托管过程或函数的同一服务器的连接。 有关 Tvp 的详细信息，请参阅[&#40;数据库引擎使用表值参数&#41;](../tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|更新了 `Accumulate` 方法的说明；该方法现在接受多个参数。|  
  
## <a name="see-also"></a>另请参阅  
 [CLR 用户定义类型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [调用 CLR 用户定义聚合函数](clr-user-defined-aggregate-invoking-functions.md)  
  
  
