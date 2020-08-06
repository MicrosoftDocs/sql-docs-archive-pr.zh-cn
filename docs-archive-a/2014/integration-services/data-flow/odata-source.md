---
title: OData 源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 98b14ef034597f6098f70386ca41c1b90be86500
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693407"
---
# <a name="odata-source"></a>OData 源
  可在 SSIS 包中使用 OData 源组件，以使用来自开放式数据协议 (OData) 服务的数据。 该组件支持 OData v2 和 v3 协议以及 ATOM 和 JSON 数据格式。  
  
> [!NOTE]  
>  OData 源可用于从 SharePoint 列表读取。 若要查看 SharePoint 服务器上的所有列表，请使用以下 URL： http:// \<server> /_vti_bin/listdata.svc。 有关 SharePoint URL 约定的详细信息，请参阅 [SharePoint Foundation REST 接口](https://msdn.microsoft.com/library/ff521587.aspx)。  
  
## <a name="odata-format"></a>OData 格式  
 大多数 OData 服务采用多种格式返回结果。 可以使用 $format 查询选项指定结果集的格式。 传输大量数据时，JSON 和 JSON 轻型这类格式比 ATOM/XML 更高效，可以提供更佳性能。 下表提供来自示例测试的结果。 可以看到，从 ATOM 切换为 JSON 时，性能提高 30-53%，从 ATOM 切换为新的 JSON 轻型格式（WCF Data Services 5.1 中提供）时，性能提高 67%。  
  
|||||  
|-|-|-|-|  
|“行”|ATOM|JSON|JSON（轻型）|  
|10000|113 秒|74 秒|68 秒|  
|1000000|1110 秒|853 秒|665 秒|  
  
> [!NOTE]  
>  SSIS OData 源使用 ODataLib 5.5.0 分析 OData 馈送，可以读取此库支持的所有格式。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [安装和卸载 OData 源组件](../install-and-uninstall-odata-source-component.md)  
  
-   [教程：使用 OData 源 &#91;SSIS&#93;](tutorial-using-the-odata-source.md)  
  
-   [在运行时修改 OData 源查询](modify-odata-source-query-at-runtime.md)  
  
-   [OData 源编辑器（“连接”页）](../odata-source-editor-connection-page.md)  
  
-   [OData 源编辑器（“列”页）](../odata-source-editor-columns-page.md)  
  
-   [OData 源编辑器（“错误输出”页）](../odata-source-editor-error-output-page.md)  
  
-   [OData 源属性](odata-source-properties.md)  
  
## <a name="see-also"></a>另请参阅  
 [OData 连接管理器](../connection-manager/odata-connection-manager.md)  
  
  
