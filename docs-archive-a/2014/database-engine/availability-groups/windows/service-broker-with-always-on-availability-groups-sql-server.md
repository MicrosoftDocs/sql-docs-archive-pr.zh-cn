---
title: Service Broker，AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 881c20e5-1c99-44eb-b393-09fc5ea0f122
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da179219363422c4ec242d29be61f35dd1609823
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586983"
---
# <a name="service-broker-with-alwayson-availability-groups-sql-server"></a>Service Broker 与 AlwaysOn 可用性组 (SQL Server)
  本主题包含有关配置 Service Broker 以便用于 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的信息。  
  
 **本主题内容：**  
  
-   [可用性组中的服务接收远程消息的要求](#ReceiveRemoteMessages)  
  
-   [向可用性组中的远程服务发送消息的要求](#SendRemoteMessages)  
  
##  <a name="requirements-for-a-service-in-an-availability-group-to-receive-remote-messages"></a><a name="ReceiveRemoteMessages"></a> 可用性组中的服务接收远程消息的要求  
  
1.  **确保可用性组拥有侦听器。**  
  
     有关详细信息，请参阅 [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)。  
  
2.  **确保 Service Broker 端点存在并已正确配置。**  
  
     在为可用性组承载可用性副本的每个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上，按如下方式配置 Service Broker 端点：  
  
    -   将 LISTENER_IP 设置为“ALL”。 此设置启用绑定到可用性组侦听器的所有有效 IP 地址上的连接。  
  
    -   在所有主机服务器实例上，将 Service Broker PORT 设置为同一端口号。  
  
        > [!TIP]  
        >  若要查看给定服务器实例上的 Service Broker 断点的端口号，请查询 [sys.tcp_endpoints](/sql/relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql) 目录视图的“端口”列，其中 **type_desc** = 'SERVICE_BROKER'。  
  
     下面的示例创建经过 Windows 身份验证的 Service Broker 端点，该端点使用默认 Service Broker 端口 (4022) 并侦听所有有效的 IP 地址。  
  
    ```  
    CREATE ENDPOINT [SSBEndpoint]  
        STATE = STARTED  
        AS TCP  (LISTENER_PORT = 4022, LISTENER_IP = ALL )  
        FOR SERVICE_BROKER (AUTHENTICATION = WINDOWS)  
    ```  
  
     有关详细信息，请参阅 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)的信息。  
  
3.  **授予针对端点的 CONNECT 权限。**  
  
     向 PUBLIC 或某个登录名授予 Service Broker 端点的 CONNECT 权限。  
  
     下面的示例向 PUBLIC 授予名为 `broker_endpoint` 的 Service Broker 端点的连接权限。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[broker_endpoint] TO [PUBLIC]  
    ```  
  
     有关详细信息，请参阅 [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)的信息。  
  
4.  **确保 msdb 包含 AutoCreatedLocal 路由或指向特定服务的路由。**  
  
    > [!NOTE]  
    >  默认情况下，每个用户数据库（包括 **msdb**）都包含路由 **AutoCreatedLocal**。 此路由匹配任何的服务名称和 Broker 实例，并指定消息应在当前实例中传递。 相比显式指定与远程实例通信的特定服务的路由，**AutoCreatedLocal** 的优先级较低。  
  
     有关创建路由的信息，请参阅 [Service Broker 路由示例](https://msdn.microsoft.com/library/ms166090\(SQL.105\).aspx) （在 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 版的联机丛书中）和 [CREATE ROUTE (Transact SQL)](/sql/t-sql/statements/create-route-transact-sql)的信息。  
  
##  <a name="requirements-for-sending-messages-to-a-remote-service-in-an-availability-group"></a><a name="SendRemoteMessages"></a> 向可用性组中的远程服务发送消息的要求  
  
1.  **创建指向目标服务的路由。**  
  
     按如下方式配置路由：  
  
    -   将 ADDRESS 设置为承载服务数据库的可用性组的侦听器 IP 地址。  
  
    -   将 PORT 设置为您在每个远程 SQL Server 实例的 Service Broker 端点中指定的端口。  
  
     下面的示例为 `RouteToTargetService` 服务创建一个名为 `ISBNLookupRequestService` 的路由。 该路由的目标为可用性组侦听器 `MyAgListener`，它使用端口 4022。  
  
    ```  
    CREATE ROUTE [RouteToTargetService] WITH   
    SERVICE_NAME = 'ISBNLookupRequestService',   
    ADDRESS = 'TCP://MyAgListener:4022';  
  
    ```  
  
     有关详细信息，请参阅 [CREATE ROUTE (Transact SQL)](/sql/t-sql/statements/create-route-transact-sql)的信息。  
  
2.  **确保 msdb 包含 AutoCreatedLocal 路由或指向特定服务的路由。** （有关详细信息，请参阅本主题前面的 [可用性组中的服务接收远程消息的要求](#ReceiveRemoteMessages)。）  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
-   [CREATE ROUTE (Transact SQL)](/sql/t-sql/statements/create-route-transact-sql)  
  
-   [GRANT (Transact-SQL)](/sql/t-sql/statements/grant-transact-sql)  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)。  
  
-   [创建和配置可用性组 (SQL Server)](creation-and-configuration-of-availability-groups-sql-server.md)  
  
-   [设置用于数据库镜像或 AlwaysOn 可用性组 &#40;SQL Server 的登录帐户&#41;](../../database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [SQL Server Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
  
