---
title: Reporting Services WMI 提供程序库引用 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider Library
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a98ca22f9d34627e484a698dcf540b31808d07e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581084"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Reporting Services WMI 提供程序库引用 (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) 提供程序支持 WMI 操作，使用这些操作能够编写脚本和代码以修改报表服务器和报表管理器的设置。  
  
 例如，在报表服务器连接到报表服务器数据库时，如果想更改是否使用集成安全性，则可以创建一个 MSReportServer_ConfigurationSetting 类的实例，并使用该报表服务器实例的 DatabaseIntegratedSecurity 属性。 下表显示的类表示 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件。 这些类在 [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] 或 [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] 命名空间中进行定义。 每个类都支持读取和写入操作。 不支持创建操作。  
  
## <a name="classes"></a>类  
 [MSReportServer_Instance 类](msreportserver-instance-class.md)  
 为客户端提供连接到已安装的报表服务器所需的基本信息。  
  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
 表示报表服务器实例的安装和运行时参数。 这些参数存储在报表服务器的配置文件中。  
  
 有关 WMI 操作的详细信息，请参阅 SDK 附带的 WMI SDK 文档 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。  
  
## <a name="see-also"></a>另请参阅  
 [访问 Reporting Services WMI 提供程序](../tools/access-the-reporting-services-wmi-provider.md)   
 [技术参考 (SSRS)](../technical-reference-ssrs.md)  
  
  
