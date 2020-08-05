---
title: MSSQL_ENG014157 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014157 error
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0682d740d82c995d64427f56aabce24b8a48ca65
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580690"
---
# <a name="mssql_eng014157"></a>MSSQL_ENG014157
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14157|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|由发布 '%s' 的订阅服务器 '%s' 创建的订阅已过期，且已停止。|  
  
## <a name="explanation"></a>说明  
 订阅服务器在指定的发布保持期内必须与发布服务器同步。 如果订阅服务器在此期间内没有同步，则该订阅将过期。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)。  
  
## <a name="user-action"></a>用户操作  
 必须先重新创建和初始化订阅，订阅服务器才可以再次接收数据更改：  
  
-   有关创建订阅的信息，请参阅[订阅发布](subscribe-to-publications.md)。  
  
-   有关初始化订阅的信息，请参阅[初始化订阅](initialize-a-subscription.md)。  
  
 如果订阅数据库包含尚未与发布服务器同步的更改，则可以使用 [tablediff Utility](../../tools/tablediff-utility.md) 来确定发布和订阅数据库中的哪些行不同。  
  
 可以延长发布保持期来避免订阅过期。 请谨慎设置较高的值，因为这可能导致存储更多的数据和元数据，从而影响性能。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
