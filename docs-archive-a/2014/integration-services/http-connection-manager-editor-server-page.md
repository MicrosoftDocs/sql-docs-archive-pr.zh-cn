---
title: HTTP 连接管理器编辑器 (服务器页面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2349766b11b28ff258496dc966d554d49c7657b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578317"
---
# <a name="http-connection-manager-editor-server-page"></a>HTTP 连接管理器编辑器（“服务器”页）
  使用 **“HTTP 连接管理器编辑器”** 对话框的 **“服务器”** 选项卡，可以通过指定 URL 和安全凭据等属性来配置 HTTP 连接管理器。 利用 HTTP 连接，包可以使用 HTTP 访问 Web 服务器以发送或接收文件。 配置 HTTP 连接管理器后，还可以测试该连接。  
  
> [!IMPORTANT]  
>  HTTP 连接管理器仅支持匿名身份验证和基本身份验证， 而不支持 Windows 身份验证。  
  
 若要了解有关 HTTP 连接管理器的详细信息，请参阅 [HTTP Connection Manager](connection-manager/http-connection-manager.md)。 若要了解有关 HTTP 连接管理器的常见使用方案的详细信息，请参阅 [Web Service Task](control-flow/web-service-task.md)。  
  
## <a name="options"></a>选项  
 **服务器 URL**  
 键入服务器的 URL。  
  
 如果您计划使用 **“Web 服务任务编辑器”** 的 **“常规”** 页上的 **“下载 WSDL”** 按钮来下载 WSDL 文件，请键入 WSDL 文件的 URL。 此 URL 要以“?wsdl”结尾。  
  
 **使用凭据**  
 指定是否希望 HTTP 连接管理器使用用户安全凭据进行身份验证。  
  
 **用户名**  
 如果 HTTP 连接管理器使用凭据，则必须指定用户名、密码和域。  
  
 **密码**  
 如果 HTTP 连接管理器使用凭据，则必须指定用户名、密码和域。  
  
 **Domain**  
 如果 HTTP 连接管理器使用凭据，则必须指定用户名、密码和域。  
  
 **使用客户端证书**  
 指定是否希望 HTTP 连接管理器使用客户端证书进行身份验证。  
  
 **证书**  
 使用“选择证书”对话框从列表中选择证书。**** 文本框显示与此证书关联的名称。  
  
 **超时值(秒)**  
 提供连接 Web 服务器时允许的超时值。 此属性的默认值为 30 秒。  
  
 **块区大小(KB)**  
 提供用于写入数据的块区大小。  
  
 **测试连接**  
 在配置 HTTP 连接管理器后，请通过单击“测试连接”确认该连接是否正常。****  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [HTTP 连接管理器编辑器（“代理”页）](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
