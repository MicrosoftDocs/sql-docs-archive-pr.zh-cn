---
title: 工作负荷的数据库元素 (DTA) | Microsoft Docs
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
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2774bc7ed981c84c966a394c95347208cbc6d656
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682538"
---
# <a name="database-element-for-workload-dta"></a>工作负荷的数据库元素 (DTA)
  指定工作负荷跟踪表所在的数据库。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|**数据类型和长度**|无。|  
|**默认值**|无。|  
|**出现次数**|如果未指定其他类型的工作负荷，则必须使用一次。 必须为父元素 `EventString` 指定子元素 `File`、`Database` 或 `Workload`，但只能使用一种类型。 例如，如果使用 `Database` 元素指定了工作负荷，则不可以在同一 XML 输入文件中使用 `File` 元素指定工作负荷。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|--------------|  
|**父元素**|[工作负荷元素 (DTA)](workload-element-dta.md)|  
|**子元素**|[数据库的名称元素 (DTA)](name-element-for-database-dta.md)<br /><br /> [数据库的架构元素 (DTA)](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>备注  
 在数据库引擎优化顾问 XML 架构中，此元素的名称为 **DatabaseDetailsTypecomplexType** 。 请不要将此 `Database` 元素与根级父元素为 `Configuration` 元素的元素相混淆。 （请参阅[用于配置的数据库元素 (DTA)](database-element-for-configuration-dta.md)。）  
  
## <a name="example"></a>示例  
 有关此元素的用法示例 `Database` ，请参阅[工作负荷元素](workload-element-dta.md)中的代码示例 &#40;DTA&#41;。  
  
## <a name="see-also"></a>另请参阅  
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
