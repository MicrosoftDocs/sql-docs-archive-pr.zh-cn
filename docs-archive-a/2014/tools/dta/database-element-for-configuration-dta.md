---
title: 用于配置 (DTA) 的数据库元素 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
ms.openlocfilehash: 69ce1a0ac9912907f6d22916dd6243621e0778db
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682537"
---
# <a name="database-element-for-configuration-dta"></a>用于配置的数据库元素 (DTA)
  指定要用数据库引擎优化顾问进行假设配置（由 `Configuration` 元素指定）评估的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|对于每个 `Server` 元素需要使用一次或多次。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[用于配置的服务器元素 (DTA)](server-element-for-configuration-dta.md)|  
|**子元素**|[数据库的名称元素 (DTA)](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素 (DTA)](schema-element-for-database-dta.md)<br /><br /> [建议元素 (DTA)](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseTypecomplexType** 。 不要将此 `Database` 元素与其根父为 `Server` 元素的元素（出现在 XML 输入文件的顶部）混淆。 有关详细信息，请参阅[服务器的数据库元素 (DTA)](database-element-for-server-dta.md)。  
  
## <a name="example"></a>示例  
 有关此元素的用法示例 `Database` ，请参阅[使用用户指定的配置 &#40;DTA&#41;的 XML 输入文件示例](xml-input-file-sample-with-user-specified-configuration-dta.md)。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
