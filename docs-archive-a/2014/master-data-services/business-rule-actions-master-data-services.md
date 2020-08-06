---
title: 业务规则操作 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cdc4daca-3dff-46d8-b7f0-57f7826dd61a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e5722eca9ed5c9fad7a4712b77366d34b8bab328
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689508"
---
# <a name="business-rule-actions-master-data-services"></a>业务规则操作 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，业务规则操作是业务规则条件计算的结果。 如果条件为 true，则将启动操作。  
  
> [!NOTE]  
>  对于默认值和更改值操作，如果生成的值超过属性的最大长度，将截断生成的值。  
  
## <a name="default-value-actions"></a>默认值操作  
 **“默认值”** 操作设置指定属性的默认值。 拥有权限的用户可以更改这些默认值。  
  
|值名称|说明|  
|----------------|-----------------|  
|**默认为**|所选属性 **默认为** 特定属性、特定属性值或者为空。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**默认为生成的值**|所选属性 **默认为生成的值** ，是通过输入起始值和增量值来确定的。<br /><br /> 此操作对文本和数字值有效。|  
|**默认为串联的值**|所选属性 **“默认为串联的值”** ，此值是通过指定多个属性来确定的。<br /><br /> 此操作对文本和链接值有效。|  
  
## <a name="change-value-actions"></a>更改值操作  
 **“更改值”** 操作可以更新指定的属性或属性值的值。 仅当新值导致操作为 true 时，用户才可以更改这些值。  
  
|值名称|说明|  
|----------------|-----------------|  
|**等于**|所选属性更改为已定义属性值、另一个属性或者为空。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**等于串联的值**|所选属性更改为串联的值，后者是通过指定多个属性来确定的。<br /><br /> 此操作对文本和链接值有效。|  
  
## <a name="validation-actions"></a>验证操作  
 **“验证”** 操作，当它们的计算结果不为 true 时，向指定的用户或组发送电子邮件。 若要提交版本，所有验证操作的计算结果都必须为 true。  
  
 唯一的例外是 **必需** 和 **无效** 操作。 这些操作必须与更改值操作相结合，以便数据能够成功验证，版本能够提交。  
  
|验证名称|说明|  
|---------------------|-----------------|  
|**是必需的**|所选属性是 **“必需”** 的，这意味着它不能为 Null 或为空。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**无效**|所选属性 **“无效”**。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**必须包含模式**|所选属性 **必须包含指定的模式** 。 使用 .NET Framework 正则表达式可以指定模式。<br /><br /> 有关正则表达式的详细信息，请参阅 MSDN Library 中的[正则表达式语言元素](https://go.microsoft.com/fwlink/?LinkId=164401)。<br /><br /> 此操作对文本和链接值有效。|  
|**必须是唯一的**|所选属性 **“必须是唯一的”** ，无论它们是独立的，还是与其他定义属性组合。<br /><br /> **最佳实践：** 将此操作与必需条件相结合，以确保订阅系统中索引字段的有效性。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**必须具有以下值之一**|所选属性 **“必须具有以下值之一”** ，它是在列表中指定的。<br /><br /> 此操作对文本值有效。|  
|**必须大于**|所选属性 **“必须大于”** 特定属性、特定属性值或者为空。<br /><br /> 此操作对文本、数字和日期值有效。|  
|**必须等于**|所选属性 **“必须等于”** 已定义的属性值、另一个属性或者为空。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
|**必须大于或等于**|所选属性 **“必须大于或等于”** 特定属性、特定属性值或者为空。<br /><br /> 此操作对文本、数字和日期值有效。|  
|**必须小于**|所选属性 **“必须小于”** 特定属性、特定属性值或者为空。<br /><br /> 此操作对文本、数字和日期值有效。|  
|**必须小于或等于**|所选属性 **“必须小于或等于”** 特定属性、特定属性值或者为空。<br /><br /> 此操作对文本、数字和日期值有效。|  
|**必须介于**|所选属性 **“必须介于”** 两个特定属性或属性值之间。<br /><br /> 此操作对文本、数字和日期值有效。|  
|**必须具有最小长度为**|所选属性 **“必须具有最小长度为”** 指定值。<br /><br /> 此操作对文本和链接值有效。|  
|**必须具有最大长度为**|所选属性 **“必须具有最大长度为”** 指定值。<br /><br /> 此操作对文本和链接值有效。|  
  
## <a name="external-action"></a>外部操作  
 **“外部”** 操作与 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]之外的应用程序交互。  
  
|操作名称|说明|  
|-----------------|-----------------|  
|**启动工作流**|启动外部工作流。 导致此操作发生的数据传递到工作流。 有关详细信息，请参阅 [SharePoint Workflow Integration with Master Data Services](https://msdn.microsoft.com/library/gg690195.aspx)（SharePoint 工作流与 Master Data Services 集成）。<br /><br /> 此操作对文本、数字、日期和链接值有效。|  
  
## <a name="see-also"></a>另请参阅  
 [业务规则条件 &#40;Master Data Services&#41;](business-rule-conditions-master-data-services.md)   
 [业务规则 &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [创建和发布业务规则 (Master Data Services)](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
