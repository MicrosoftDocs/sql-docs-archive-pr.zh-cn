---
title: 介绍 Reporting Services 中的异常处理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], exception handling
- errors [Reporting Services]
- exceptions [Reporting Services]
- Report Server Web service, exception handling
- XML Web service [Reporting Services], exception handling
ms.assetid: 54381870-ce67-482b-aa83-6a838cdbf9b9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 091b1f40d293515617e369b750a5f18dfe12951b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689284"
---
# <a name="introducing-exception-handling-in-reporting-services"></a>介绍 Reporting Services 中的异常处理
  如果您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 应用程序将某一请求发送到报表服务器 Web 服务但该服务无法处理该请求，则该服务会将一个 SOAP 异常返回到客户端。 处理报表服务器 Web 服务引发的异常是您开发的应用程序的重要一环，因为可以在错误发生时将有用信息返回给用户。  
  
 本节包含有关处理异常、防止无效用户输入和向用户返回有意义的错误信息的具体信息。 有关异常处理的常规信息，请参阅 SDK 文档中的 "处理和引发异常" [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[在 Reporting Services 中处理异常](handling-exceptions-in-reporting-services.md)|概述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的异常以及 SOAP 在从 Web 服务返回错误时的角色。|  
|[Reporting Services 异常处理的最佳实践](best-practices/best-practices-for-reporting-services-exception-handling.md)|就如何在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中处理异常提供建议。|  
|[Reporting Services SoapException 类](soapexception-class/reporting-services-soapexception-class.md)|介绍 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的 SoapException 类****。|  
  
## <a name="see-also"></a>另请参阅  
 [使用 Web 服务和 .NET Framework 生成应用程序](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
