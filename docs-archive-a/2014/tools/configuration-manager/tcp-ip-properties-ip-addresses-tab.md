---
title: TCP-IP 属性 (IP 地址 "选项卡) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: stevestein
ms.author: sstein
ms.openlocfilehash: af157a5826d98b31cb98a2a9e203f847ed37df10
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577987"
---
# <a name="tcp-ip-properties-ip-addresses-tab"></a>TCP-IP 属性 (IP 地址 "选项卡) 
  使用 **“TCP/IP 属性（‘IP 地址’选项卡）”** 对话框，可以配置特定 IP 地址的 TCP/IP 协议选项。 只有选中 **“IP All”** ，才能一次配置所有地址的 **“TCP 动态端口”** 和 **“TCP 端口”** 。  
  
 当 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新启动时，更改将生效。 有关启动和停止 SQL Server Browser 服务的信息，请参阅联机丛书中的“如何：启动和停止 SQL Server Browser 服务”。  
  
## <a name="static-vs-dynamic-ports"></a>静态端口与动态端口  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例侦听端口 1433 上传入的连接。 可以出于安全原因或客户端应用程序要求更改此端口。 默认情况下，命名实例（包含 SQL Server Express）被配置为侦听动态端口。 若要配置静态端口，请将 **“TCP 动态端口”** 框保留为空，并在 **“TCP 端口”** 框中提供一个可用的端口号。 有关打开防火墙中的端口的详细信息，请参阅联机丛书中的“配置 Windows 防火墙以允许 SQL Server 访问”。  
  
## <a name="dynamic-ports"></a>动态端口  
 如果某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例已配置为侦听动态端口，则在启动时，该实例将检查操作系统中的可用端口，并为该端口打开一个端点。 传入连接必须指定要连接的端口号。 由于每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时端口号都可能会改变，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务监视端口，并将传入连接指向该实例的当前端口。 使用动态端口会增加通过防火墙连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的复杂性，因为重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时端口号可能会改变，从而需要更改防火墙设置。 若要避免通过防火墙连接的问题，请将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为使用静态端口。  
  
## <a name="options"></a>选项  
 **活动**  
 指示该 IP 地址在计算机上处于活动状态。 不适用于 **“IPAll”** 。  
  
 **已启用**  
 如果 **“TCP/IP 属性(‘协议’选项卡)”** 上的 **“全部侦听”** 属性设为 **“否”** ，则该属性指示 SQL Server 是否侦听 IP 地址。 如果 **“TCP/IP 属性(‘协议’选项卡)”** 上的 **“全部侦听”** 属性设为 **“是”** ，则表示忽略该属性。 不适用于 **“IPAll”** 。  
  
 **IP 地址**  
 查看或更改此连接使用的 IP 地址。 列出计算机使用的 IP 地址以及 IP 环回地址 127.0.0.1。 不适用于 **“IPAll”** 。 该 IP 地址可以为 IPv4 格式或 IPv6 格式。  
  
 **“IP All”**  
 如果未启用动态端口，则为空。 若要使用动态端口，请设置为 0。  
  
 对于 **“IPAll”** ，将显示所用动态端口的端口号。  
  
 **“TCP 动态端口”**  
 查看或更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听的端口。 默认情况下， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的默认实例侦听端口 1433。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]可以侦听同一 IP 地址的多个端口，端口以逗号分隔的格式列出：1433,1500,1501。 此字段最多允许 2047 个字符。  
  
 若要配置单个 IP 地址以侦听多个端口，还必须将“TCP/IP 属性”对话框的“协议”选项卡上的“全部侦听”参数设置为“否”     。 有关详细信息，请参阅“如何：将数据库引擎配置为侦听多个 TCP 端口”（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中）。  
  
## <a name="adding-or-removing-ip-addresses"></a>添加或删除 IP 地址  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器显示安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时可用的 IP 地址。 如果发生以下情况，可用的 IP 地址也会随之改变：添加或删除网卡、动态分配的 IP 地址过期、重新配置网络结构或计算机的物理位置发生改变（例如便携式计算机在另一座大楼连接到网络）。 若要更改 IP 地址，可以编辑 **“IP 地址”** 框，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用 TCP IP 创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [SQL Server Browser 服务](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
