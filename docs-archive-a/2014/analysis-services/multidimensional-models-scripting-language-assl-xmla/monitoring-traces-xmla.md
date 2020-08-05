---
title: " (XMLA) 监视跟踪 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, traces
- XMLA, traces
- monitoring traces [XMLA]
- traces [Analysis Services]
ms.assetid: cdbfb984-18bd-4c4e-8fb7-d64ce298ed35
author: minewiskan
ms.author: owend
ms.openlocfilehash: a2ca181b7c194fdd3909875f881d1030a77ae039
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580955"
---
# <a name="monitoring-traces-xmla"></a>监视跟踪 (XMLA)
  您可以使用 XML for Analysis (XMLA) 中的 "[订阅](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla)" 命令来监视在的实例上定义的现有跟踪 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 `Subscribe` 命令将跟踪的结果作为行集返回。  
  
## <a name="specifying-a-trace"></a>指定跟踪  
 命令的[object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)属性 `Subscribe` 必须包含对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或对实例的跟踪的对象引用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 如果未指定 `Object` 属性，或者未在 `Object` 属性中指定跟踪标识符，则 `Subscribe` 命令将监视该命令的 SOAP 标头中指定的显式会话的默认会话跟踪。  
  
## <a name="returning-results"></a>返回结果  
 `Subscribe` 命令会返回包含由指定跟踪捕获的跟踪事件的行集。 `Subscribe`命令将返回跟踪结果，直到[取消](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)命令取消该命令。  
  
 下表列出了该行集包含的列。  
  
|列|数据类型|说明|  
|------------|---------------|-----------------|  
|EventClass|Integer|跟踪所接收的事件的事件类。|  
|EventSubclass|Long integer|跟踪所接收的事件的事件子类。|  
|CurrentTime|datetime|事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|StartTime|datetime|事件（如果有）的开始时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。|  
|EndTime|datetime|事件（如果有的话）的结束时间。 为了便于筛选，采用的格式为“YYYY-MM-DD”和“YYYY-MM-DD HH:MM:SS”。<br /><br /> 对于描述进程或操作启动的事件类，不填充此列。|  
|持续时间|Long integer|事件所用的总时间（毫秒）。|  
|CPUTime|Long integer|事件所用的处理器时间（毫秒）。|  
|作业 ID|Long integer|进程的作业标识符。|  
|SessionID|String|发生事件的会话的标识符。|  
|SessionType|String|发生事件的会话的类型。|  
|ProgressTotal|Long integer|事件所报告的进度总数。|  
|IntegerData|Long integer|与事件关联的整数数据。 此列的内容取决于事件的事件类和子类。|  
|ObjectID|String|发生事件的对象的标识符。|  
|ObjectType|String|ObjectName 中指定的对象的类型。|  
|ObjectName|String|发生事件的对象的名称。|  
|ObjectPath|String|发生事件的对象的分层路径。 对于 ObjectName 中所指定的对象的父级，该路径表示为以逗号分隔的对象标识符字符串。|  
|ObjectReference|String|ObjectName 中所指定对象的对象引用的 XML 表示形式。|  
|NestLevel|Integer|发生事件的事务的级别。|  
|NumSegments|Long integer|发生事件的命令所影响或访问的数据段数量。|  
|严重性|Integer|事件异常的严重级别。 此列可包含下列值之一：<br /><br /> 值： 0 = 成功<br /><br /> 值： 1 = 信息<br /><br /> 值： 2 = 警告<br /><br /> 值： 3 = 错误|  
|Success|Boolean|指示命令成功还是失败。|  
|错误|Long integer|事件的错误号（如果适用）。|  
|ConnectionID|String|发生事件的连接的标识符。|  
|DatabaseName|String|发生事件的数据库的名称。|  
|NTUserName|String|与事件关联的用户的 Windows 用户名。|  
|NTDomainName|String|与事件关联的用户的 Windows 域。|  
|ClientHostName|String|正在运行客户端应用程序的计算机的名称。 此列由该客户端应用程序传递的值填充。|  
|ClientProcessID|Long integer|客户端应用程序的进程标识符。|  
|ApplicationName|String|客户端应用程序的名称，该客户端应用程序创建了到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的连接。 此列由客户端应用程序传递的值填充，而不是由所显示的程序名填充。|  
|NTCanonicalUserName|String|与事件关联的用户的 Windows 规范用户名。|  
|SPID|String|发生事件的会话的服务器进程 ID (SPID)。 此列的值直接对应于发生事件的 XMLA 消息的 SOAP 标头中指定的会话 ID。|  
|TextData|String|与事件关联的文本数据。 此列的内容取决于事件的事件类和子类。|  
|ServerName|String|发生事件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。|  
|RequestParameters|String|发生事件的参数化查询或 XMLA 命令的参数。|  
|RequestProperties|String|发生事件的 XMLA 方法的属性。|  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
