---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10061"
helpviewer_keywords:
- 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0c866bd8dce01f65036f1d508a94252a97613424
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691214"
---
# <a name="mssqlserver_10061"></a>MSSQLSERVER_10061
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10061|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在建立与服务器的连接时出错。  在连接到 SQL Server 时，在默认的设置下 SQL Server 不允许远程连接可能会导致此失败。 （提供程序：TCP 提供程序，错误:0 - 因目标计算机主动拒绝该连接而导致无法建立连接。) (Microsoft SQL Server，错误:10061)|  
  
## <a name="explanation"></a>说明  
 服务器未响应客户端请求。 发生此错误的原因可能是尚未启动服务器。  
  
## <a name="user-action"></a>用户操作  
 确保已启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [管理数据库引擎服务](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [网络协议和网络库](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
