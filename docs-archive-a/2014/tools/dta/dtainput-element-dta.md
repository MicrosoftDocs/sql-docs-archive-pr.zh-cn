---
title: " (DTA) 的 DTAInput 元素 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
author: stevestein
ms.author: sstein
ms.openlocfilehash: e7d2ff380a4ae1595e50aae472efc5fb4ac72efe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687399"
---
# <a name="dtainput-element-dta"></a>DTAInput 元素 (DTA)
  包含用于数据库引擎优化顾问的 XML 输入的定义。  
  
## <a name="syntax"></a>语法  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|---------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|可选。对于每个 **DTAXML** 元素可以使用一次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[DTAXML 元素 (DTA)](dtaxml-element-dta.md)|  
|**子元素**|[服务器元素 (DTA)](server-element-dta.md)<br /><br /> [工作负荷元素 (DTA)](workload-element-dta.md)<br /><br /> [TuningOptions 元素 (DTA)](tuningoptions-element-dta.md)<br /><br /> [配置元素 (DTA)](configuration-element-dta.md)|  
  
## <a name="remarks"></a>备注  
 此元素是数据库引擎优化顾问输入架构层次结构的根元素。 数据库引擎优化顾问的输入可以是各种参数，这些参数指定了要优化其数据库的服务器、工作负荷、优化选项或用户指定配置。  
  
## <a name="example"></a>示例  
 有关 **DTAInput** 元素的使用示例，请参阅[简单 XML 输入文件示例 (DTA)](simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
