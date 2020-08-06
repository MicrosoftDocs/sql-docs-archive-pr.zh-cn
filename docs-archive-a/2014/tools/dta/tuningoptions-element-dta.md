---
title: " (DTA) 的 TuningOptions 元素 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2fab1c55c9d036424142b2692e8335ea65c22340
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691436"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 元素 (DTA)
  包含用于特定优化会话的优化选项。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。 如果已使用，则每个 `DTAInput` 元素只能使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAInput 元素 (DTA)](dtainput-element-dta.md)|  
|**子元素**|`ReportSet` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `TuningLogTable` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `NumberOfEvents` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> [TuningTimeInMin 元素 (DTA)](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 元素 (DTA)](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `MaxColumnsInIndex` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `MinPercentageImprovement` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [TestServer 元素 (DTA)](server-element-dta.md)<br /><br /> [FeatureSet 元素 (DTA)](featureset-element-dta.md)<br /><br /> [分区元素 (DTA)](partitioning-element-dta.md)<br /><br /> [DropOnlyMode 元素 (DTA)](droponlymode-element-dta.md)<br /><br /> [KeepExisting 元素 (DTA)](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 元素 (DTA)](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 元素 (DTA)](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。<br /><br /> `RetainShellDB` 元素。 有关详细信息，请参阅 [数据库引擎优化顾问 XML 架构](https://go.microsoft.com/fwlink/?linkid=43100)。|  
  
## <a name="example"></a>示例  
 有关元素的示例 `TuningOptions` ，请参阅[&#40;DTA&#41;的 XML 输入文件示例](xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
