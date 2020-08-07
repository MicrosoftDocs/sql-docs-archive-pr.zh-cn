---
title: MHTML 设备信息设置 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- device information settings [Reporting Services], MHTML rendering
- MHTML [Reporting Services]
ms.assetid: 60b85dd8-b4fb-4ad9-be6a-e7c89ac076fe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 076a0179871775984799fc8ce5366a220f812867
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588943"
---
# <a name="mhtml-device-information-settings"></a>MHTML 设备信息设置
  下表列出的是以 Web 存档 (MHTML) 格式呈现报表时的设备信息设置。  
  
|设置|值|  
|-------------|-----------|  
|**JavaScript**|指示是否在所呈现报表中支持 JavaScript。|  
|**OutlookCompat**|指示是否呈现可改善报表在 Outlook 中的外观的额外元数据。 默认值为 `true`。|  
|**MHTML 片段**|指示是否创建一个 MHTML 片段以取代完整 MHTML 文档。 MHTML 片段包含 TABLE 元素中的报表内容，并忽略 HTML 和 BODY 元素。 默认值为 `false`。|  
|**DataVisualizationFitSizing**|指示 tablix 内数据可视化调整大小行为。 这包括图表、仪表和地图。<br /><br /> 可能的值包括 **“近似”** 和 **“精确”** 。<br /><br /> 默认值为 **“近似”** 。 如果从 **rsreportserver.config** 文件删除该设置，则默认行为为 **“精确”** 。<br /><br /> 启用 **“精确”** 可能会影响性能，因为确定精确大小所需的处理时间可能更长。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [将设备信息设置传递给呈现扩展插件](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [在 RSReportServer.Config 中自定义呈现扩展插件参数](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [技术参考 (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
