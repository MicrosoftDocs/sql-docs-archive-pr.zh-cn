---
title: SMTP 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f3c090ab672790901baae01ae86f8d22e008b4ac
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693432"
---
# <a name="smtp-connection-manager"></a>SMTP 连接管理器
  SMTP 连接管理器使包可以连接到简单邮件传输协议 (SMTP) 服务器。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的发送邮件任务使用 SMTP 连接管理器。  
  
 如果将 Microsoft Exchange 用作 SMTP 服务器，则可能需要配置 SMTP 连接管理器才能使用 Windows 身份验证。 Exchange 服务器可以配置为不支持未经身份验证的 SMTP 连接。  
  
## <a name="configuration-the-smtp-connection-manager"></a>SMTP 连接管理器的配置  
 将 SMTP 连接管理器添加到包时，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时决定 SMTP 连接的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包的 `Connections` 集合。 该连接管理器的 `ConnectionManagerType` 属性设置为 `SMTP`。  
  
 可以使用下列方式配置 SMTP 连接管理器：  
  
-   提供一个连接字符串。  
  
-   指定 SMTP 服务器的名称。  
  
-   指定要使用的身份验证方法。  
  
    > [!IMPORTANT]  
    >  SMTP 连接管理器仅支持匿名身份验证和 Windows 身份验证， 而不支持基本身份验证。  
  
-   指定在发送电子邮件时是否使用安全套接字层 (SSL) 对通信进行加密。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [SMTP 连接管理器编辑器](../smtp-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
  
