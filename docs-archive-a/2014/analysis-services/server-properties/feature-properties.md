---
title: 功能属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQMSupportEnabled property
- ComUdfEnabled property
- LinkToOtherInstanceEnabled property
- ManagedCodeEnabled property
- ConnStringEncryptionEnabled property
- LinkFromOtherInstanceEnabled property
- LinkInsideInstanceEnabled property
- UseCachedPageAllocators property
ms.assetid: a34d046a-6562-4d98-b827-37cebc6d77b4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 08001a172c1b39fb912ef042ed85effd4f8ededa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694590"
---
# <a name="feature-properties"></a>功能属性
  功能属性与产品功能有关，大多数是高级属性，包括控制服务器实例之间的链接的属性。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的服务器属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)。  
  
 **适用于：** 仅限多维服务器模式  
  
## <a name="properties"></a>属性  
  
|属性|默认|说明|  
|--------------|-------------|-----------------|  
|`ManagedCodeEnabled`|1|布尔值属性，指示是否启用 CLR 存储过程。|  
|`LinkInsideInstanceEnabled`|1|布尔值属性，指示是否可在同一个服务器实例内创建链接对象。|  
|`LinkToOtherInstanceEnabled`|0|布尔值属性，指示是否可链接到远程服务器上的对象。|  
|`LinkFromOtherInstanceEnabled`|0|布尔值属性，指示是否可从其他服务器实例链接到对象。|  
|`ConnStringEncryptionEnabled`|1|布尔值属性，指示是否在服务器配置文件中对连接字符串加密。|  
|`UseCachedPageAllocators`|0|布尔值属性，指示是否启用缓存页分配器。|  
|`ComUdfEnabled`|0|布尔值属性，指示是否启用定义为 COM 对象的用户定义函数。|  
|`SQMSupportEnabled`|1|布尔值属性，指示是否自动将错误和功能使用情况报告发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。|  
|`ResourceMonitoringEnabled`|1|布尔值属性，指示是否启用内部资源监视计数器。 默认情况下启用此属性。 启用时，此属性允许计数器收集有关 CPU、内存和 I/O 活动的使用情况数据。<br /><br /> 动态管理视图 (DMV) 使用内部资源监视计数器来报告资源使用情况。 如果您禁用此属性，DMV 查询仍然会运行，但结果集将无效。 依赖于该属性的 DMV 包括以下各项：<br />**DISCOVER_OBJECT_ACTIVITY**<br />**DISCOVER_COMMAND_OBJECTS**<br />**DISCOVER_SESSIONS** （适用于 SESSION_READS、SESSION_WRITES、SESSION_CPU_TIME_MS）<br /><br /> <br /><br /> 在使用 NUMA 体系结构的多核系统上，禁用此属性可以提高查询性能，特别是对于较高的多用户工作负荷。 您将需要执行比较测试，以便确定查询性能是否由于更改此属性而得到改善。 有关执行比较测试的最佳做法，包括清除缓存和避免常见错误，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539)。|  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [使用动态管理视图 (DMV) 监视 Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
