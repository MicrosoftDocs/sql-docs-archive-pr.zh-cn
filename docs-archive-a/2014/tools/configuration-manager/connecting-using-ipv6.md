---
title: 使用 IPv6 进行连接 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f2ecd605f67446fade262cfe795f344dfb165c0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691451"
---
# <a name="connecting-using-ipv6"></a>使用 IPv6 进行连接
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 完全支持 Internet 协议版本 4 (IPv4) 和 Internet 协议版本 6 (IPv6)。 将 Windows 配置为使用 IPv6 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，各组件会自动识别 IPv6 的存在。 不必采用特殊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置。  
  
 支持包括但不限于下列各项：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和其他服务器组件可以同时侦听 IPv4 和 IPv6 地址。 如果同时存在 IPv4 和 IPv6，则可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器来配置 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，以便只侦听 IPv4 地址或只侦听 IPv6 地址。  
  
-   根据 IPv4 地址对运行于支持 IPv4 和 IPv6 的计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务进行查询时，该服务会对 IPv4 地址及其列表中的第一个 IPv4 TCP 端口做出响应。 根据 IPv6 地址进行查询时，该服务会对 IPv6 地址及其列表中的第一个 IPv6 TCP 端口做出响应。 为了避免出现不一致，建议将 IPv4 和 IPv6 侦听器配置为侦听相同的端口。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器等工具都接受 IPv4 和 IPv6 格式的 IP 地址。 在大多数情况下，如果 \<*computer_name*> \\ < 使用服务器主机名或完全限定的域名 (FQDN) 指定*instance_name*>，则无需修改连接字符串。 如果服务器安装有 IPv4 和 IPv6，则其主机名或 FQDN 将会解析到多个 IP 地址，其中至少包括一个 IPv4 地址和多个 IPv6 地址。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 会按照从 TCP/IP 接收这些 IP 地址时的顺序尝试使用它们来建立连接，并使用第一个成功建立的连接。 由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 无法预测顺序，因此，应将顺序视为随机顺序。 如果同时存在 IPv4 地址和 IPv6 地址，则首先尝试使用 IPv4 地址。 这一逻辑对于 ODBC、OLE DB 或 ADO.NET 的用户是透明的。  
  
    > [!NOTE]  
    >  如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 未侦听 IPv4，则尝试进行 IPv4 连接之后，必须等待超时期限过后再尝试使用 IPv6 地址。 为了避免出现这种情况，请直接连接到 IPv6 IP 地址或使用 IPv6 地址配置客户端的别名。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)  
  
  
