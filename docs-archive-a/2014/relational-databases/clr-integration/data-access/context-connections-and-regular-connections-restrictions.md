---
title: 常规连接和上下文连接的限制 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 52f50347a27cdaffe83b252d86c56382b5ef4f31
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587865"
---
# <a name="restrictions-on-regular-and-context-connections"></a>对常规连接和上下文连接的限制
  本主题讨论 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] 通过上下文和常规连接在进程中执行的代码的限制。  
  
## <a name="restrictions-on-context-connections"></a>对上下文连接的限制  
 开发应用程序时，请考虑应用于上下文连接的以下限制：  
  
-   对于给定的连接，在给定的时间，您只能打开一个上下文连接。 如果有多个语句并发运行在单独的连接中，则其中的每个语句都可以获得自己的上下文连接。 此限制不影响来自不同连接的并发请求；它只影响对给定连接的给定请求。  
  
-   上下文连接中不支持多个活动结果集 (MARS)。  
  
-   `SqlBulkCopy` 类不能在上下文连接中工作。  
  
-   不支持上下文连接中的更新批处理  
  
-   `SqlNotificationRequest` 不能用于对上下文连接执行的命令。  
  
-   不支持取消正在对上下文连接运行的命令。 `SqlCommand.Cancel` 方法会自行忽略请求。  
  
-   使用“context connection=true”时，不能使用任何其他连接字符串关键字。  
  
-   如果 `SqlConnection.DataSource` 的连接字符串为“context connection=true”，则 `SqlConnection` 属性返回 Null，而不是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。  
  
-   对上下文连接执行命令时，设置 `SqlCommand.CommandTimeout` 属性无效。  
  
## <a name="restrictions-on-regular-connections"></a>对常规连接的限制  
 开发应用程序时，请考虑应用于常规连接的以下限制：  
  
-   不支持对内部服务器异步执行命令。 如果在命令的连接字符串中包括“async=true”，然后执行命令，将导致引发 `System.NotSupportedException`。 将出现此消息：“在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程内运行时，不支持异步处理。”  
  
-   不支持 `SqlDependency` 对象。  
  
## <a name="see-also"></a>另请参阅  
 [上下文连接](context-connection.md)  
  
  
