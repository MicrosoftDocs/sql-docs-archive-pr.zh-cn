---
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d3f56a104841c4825bba1f60b3588fadd63555c6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581275"
---
# <a name="mssqlserver_17194"></a>MSSQLSERVER_17194
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17194|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|服务器无法加载登录所需的 SSL 提供程序库；连接已关闭。 可以用 SSL 对登录序列或所有通信进行加密，具体取决于管理员配置服务器的方式。 有关错误消息 0xXXXX 的信息，请参阅联机丛书。 [客户端：11.11.11.11]|  
  
## <a name="explanation"></a>说明  
 此错误指示客户端已关闭连接。 因为连接超时时间已到，所以有可能发生此错误。 该错误消息将显示操作系统返回的值，说明错误的根本问题。  
  
## <a name="user-action"></a>用户操作  
 如果错误消息中的错误代码为 0x2746（十进制值 10054），则说明客户端重置了连接,通常是因为连接超时。若要纠正此错误，请延长客户端或调用程序连接超时时间。  
  
 若要为其他错误消息值确定可能的解决方案，请使用操作系统命令 **net helpmsg**，并指定错误代码的十进制值。  
  
 有关如何连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的详细信息，请参阅[服务器网络配置](../../database-engine/configure-windows/server-network-configuration.md)和[客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)。  
  
## <a name="internal-only"></a>仅内部  
  
