---
title: 使用 Shared Memory 协议创建有效的连接字符串 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], shared memory
- aliases [SQL Server], shared memory
ms.assetid: 5fff42e8-377f-4b40-b0c8-b02393f8a1af
author: stevestein
ms.author: sstein
ms.openlocfilehash: ca97332a09a33fcfc15a3dbb2599af27dbe0e1db
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682558"
---
# <a name="creating-a-valid-connection-string-using-shared-memory-protocol"></a>使用 Shared Memory 协议创建有效的连接字符串
  从运行在同一台计算机上的客户端到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接使用 shared memory 协议。 共享内存没有可配置的属性。 始终会先尝试使用共享内存，无法将其从 **“客户端协议属性”** 列表中 **“启用的协议”** 列表的顶部位置移开。 可以禁用 shared memory 协议，在排除其他某个协议的故障时，这样做很有用。  
  
 不能使用 shared memory 协议来创建别名，但是如果启用了共享内存，然后通过名称连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ，就可以创建共享内存连接。 共享内存连接字符串的格式为 `lpc:<servername>[\instancename]`。  
  
## <a name="connecting-to-the-local-server"></a>连接到本地服务器  
 当连接到与客户端运行在同一台计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，可以使用“(本地)”  作为服务器名称。 由于上述方法不明确，因此不建议使用，但是当客户端运行在已知的计算机上时，该方法还是有用的。 例如，当为断开连接的移动用户（如销售人员，其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在便携式计算机上运行并存储相应的项目数据）创建应用程序时，连接到“(本地)”  的客户端就可以始终与运行在便携式计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保持连接。 可以使用词语“本地主机”  或句点 ( **.** ) 来取代“(本地)”  。  
  
## <a name="verifying-your-connection-protocol"></a>验证连接协议  
 以下查询将返回当前连接所使用的协议。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>示例：  
 如果已启用 shared memory 协议，下列名称将使用该协议连接到本地计算机：  
  
 `<servername>`  
  
 `<servername>\<instancename>`  
  
 `(local)`  
  
 `localhost`  
  
 不能为共享内存连接创建别名。  
  
> [!NOTE]  
>  在“服务器”框中指定 IP 地址将产生 TCP/IP 连接。   
  
## <a name="see-also"></a>另请参阅  
 [使用 TCP IP 创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [使用命名管道创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
