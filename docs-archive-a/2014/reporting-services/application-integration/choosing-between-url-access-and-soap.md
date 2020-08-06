---
title: 在 URL 访问和 SOAP 之间选择 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], vs. URL access
- Report Server Web service, application integration
- URL access [Reporting Services], vs. SOAP
- Web service [Reporting Services], application integration
ms.assetid: bccdc243-4366-4ce5-8e63-3dd6c463fa52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8075d92c51960c36d52d1a6ed5dc742a943177ff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577419"
---
# <a name="choosing-between-url-access-and-soap"></a>在 URL 访问与 SOAP 之间选择
  将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义应用程序的过程可能充满挑战。 然而，这样的挑战并不在于编程模型或 API 有多么复杂，而在于如何从众多可能的集成方法中选择一种合适的方法。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 最初的设计就是一个开发平台，因此在构建时考虑了编程的灵活性。 在满足灵活性要求后，接下来需要决定如何将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 报表导航和管理功能集成到现有业务应用程序中。

 ![Reporting Services 编程方案](../../../2014/reporting-services/media/bk-ext-04.gif "Reporting Services 编程方案")Reporting Services 编程支持多种方案。

 可以通过两种方法将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义应用程序中：URL 访问和 Reporting Services SOAP API。 具体使用哪种方法取决于若干因素。 在某些情况下，将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到自定义业务应用程序要求您同时使用 URL 访问和 SOAP。 您应提出以下问题：

-   您或您的最终用户需要哪种企业报表功能？ 您是需要一种简单的方法来启动和导航报表，还是需要由自定义业务解决方案提供更高级的报表服务器管理功能？

-   您的用户通常在哪种环境下运行？ 您的业务应用程序是 Web 应用程序还是 Windows 应用程序？ 您的最终用户从 Win32 环境切换到 Web 环境有多容易？ 您需要对在其中运行和管理报表的环境具有哪种控制权？

 一旦您回答了前面的问题，您就可以决定如何将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 集成到您的 IT 基础结构中。 通常，若要查看和导航单独的报表，将首选 URL 访问。 借助于 URL 访问，您可以顺畅、快速地导航报表，而没有 Web 服务的开销。 此外，URL 访问目前是使用完整的 HTML 查看器（其中包含报表工具栏）进行报表导航的唯一编程技术。 此外，由于 URL 访问绕过了针对进出服务器的 SOAP 请求进行封送处理的过程，因此，其性能高于 SOAP。 在要求使用内置工具进行查看和导航以轻松快捷地访问报表的集成方案中，URL 访问是更好的选择。

> [!NOTE]
>  报表服务器 URL 访问支持 HTML 查看器以及报表工具栏的扩展功能。 SOAP API 不支持这一类型的呈现的报表。 如果您使用 SOAP 呈现报表，则需要设计和开发自己的报表工具栏。

 有关报表工具栏的详细信息，请参阅 [HTML 查看器和报表工具栏](../html-viewer-and-the-report-toolbar.md)。

 有关 URL 访问的详细信息，请参阅[Url 访问 &#40;SSRS&#41;](../url-access-ssrs.md)。

 URL 访问可用于查看报表，但它不提供报表和命名空间管理功能，而这一功能对于任何企业报表方案是必不可少的。 在这种情况下，建议使用 Reporting Services SOAP API 的广泛和丰富的功能。 通过 SOAP API，您可以管理和部署报表、创建计划、配置服务器属性、管理报表服务器命名空间、创建订阅等等。 SOAP API 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中公开一组完整的管理功能。 借助于 SOAP API，还可以通过 API 的 <xref:ReportExecution2005.ReportExecutionService.Render%2A> 方法查看和导航报表。 然而，通过 SOAP API 查看报表并不启用报表工具栏的内置查看功能，也不自动处理 URL 访问提供的报表交互性。

 有关 Reporting Services SOAP API 的详细信息，请参阅[报表服务器 Web 服务](../report-server-web-service/report-server-web-service.md)。

 在绝大多数情况下，要求同时使用 URL 访问和 SOAP 调用以满足您的报表需要。 最初连接到报表服务器数据库并在用户界面中提供可用的报表列表时，将使用 SOAP；而 URL 访问用于实际访问和导航单独的报表。

 有关组合 URL 访问和 Web 服务来提供集成报表功能的示例，请参阅 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)（SQL Server Reporting Services 产品示例）。

## <a name="see-also"></a>另请参阅
 将[Reporting Services 集成到应用程序](../../../2014/reporting-services/application-integration/integrating-reporting-services-into-applications.md)[集成 Reporting Services 使用 SOAP](../application-integration/integrating-reporting-services-using-soap.md) [集成 Reporting Services 使用 URL 访问](../application-integration/integrating-reporting-services-using-url-access.md)[技术参考 &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)


