---
title: 表达式中的内置集合（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 55ceebd69d98506bb461cf4fc55b4d395453b652
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587204"
---
# <a name="built-in-collections-in-expressions-report-builder-and-ssrs"></a>表达式中的内置集合（报表生成器和 SSRS）
  在报表的表达式中，可以包含对以下内置集合的引用：ReportItems、Parameters、Fields、DataSets、DataSources、Variables 和全局信息的内置字段（如报表名称）。 并非所有集合都显示在 **“表达式”** 对话框中。 DataSets 和 DataSources 集合只有在运行时报表将发布到报表服务器之后才可用。 ReportItems 集合是报表区域中的文本框集合，例如页面或页眉中的文本框。  
  
 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-built-in-collections"></a><a name="Collections"></a> 了解内置集合  
 下表列出了在您撰写表达式时可用的内置集合。 无论是否能够使用“表达式”对话框以交互方式添加对集合、示例和包含可用的初始化集合值的说明的引用，每行都包括集合的区分大小写编程名称。  
  
|内置集合|“表达式”对话框中的类别|示例|说明|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|`Globals`|内置字段|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|表示对报表有用的全集变量，如报表名称或页码。 始终可用。<br /><br /> 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|`User`|内置字段|`=User.UserID`<br /><br /> - 或 -<br /><br /> `=User.Language`|表示与运行报表的用户有关的数据的集合，如语言设置或用户 ID。 始终可用。<br /><br /> 有关详细信息，请参阅[内置的全局和用户引用（报表生成器和 SSRS）](built-in-collections-built-in-globals-and-users-references-report-builder.md)。|  
|`Parameters`|参数|`=Parameters("ReportMonth").Value`<br /><br /> - 或 -<br /><br /> `=Parameters!ReportYear.Value`|表示报表参数的集合，每个参数都可为单值或多值参数。 直到处理初始化完成之后才可用。 有关详细信息，请参阅[集合引用（报表生成器和 SSRS）](built-in-collections-parameters-collection-references-report-builder.md)。|  
|`Fields(` *\<Dataset>* `)`|字段|`=Fields!Sales.Value`|表示可用于报表的数据集的字段集合。 将数据从数据源检索到数据集中之后可用。 有关详细信息，请参阅[数据集字段集合引用（报表生成器和 SSRS）](built-in-collections-dataset-fields-collection-references-report-builder.md)。|  
|`DataSets`|不显示|`=DataSets("TopEmployees").CommandText`|表示从报表定义的主体中引用的数据集的集合。 不包括仅在页眉或页脚中使用的数据源。 无法在本地预览中使用。 有关详细信息，请参阅 [DataSources 和 DataSets 集合引用（报表生成器和 SSRS）](built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|`DataSources`|不显示|`=DataSources("AdventureWorks2012").Type`|表示从报表的主体中引用的数据源集合。 不包括仅在页眉或页脚中使用的数据源。 无法在本地预览中使用。 有关详细信息，请参阅 [DataSources 和 DataSets 集合引用（报表生成器和 SSRS）](built-in-collections-datasources-and-datasets-references-report-builder.md)。|  
|`Variables`|`Variables`|`=Variables!CustomTimeStamp.Value`|表示报表变量和组变量的集合。 有关详细信息，请参阅[报表和组变量集合引用（报表生成器和 SSRS）](built-in-collections-report-and-group-variables-references-report-builder.md)。|  
|`ReportItems`|不显示|`=ReportItems("Textbox1").Value`|表示报表项中的文本框集合。 此集合可以用于汇总页面中的项，包括页眉或页脚。 有关详细信息，请参阅 [ReportItems 集合引用（报表生成器和 SSRS）](built-in-collections-reportitems-collection-references-report-builder.md)。|  
  
##  <a name="using-collection-syntax-in-an-expression"></a><a name="Syntax"></a> 在表达式中使用集合语法  
 若要引用表达式中的集合，请将标准 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 语法用于集合中的项。 下表显示集合语法的示例。  
  
|语法|示例|  
|------------|-------------|  
|*集合!ObjectName. 属性*|`=Fields!Sales.Value`|  
|*集合!ObjectName ( "属性" ) *|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*集合. 成员*|`=User.Language`|  
  
## <a name="see-also"></a>另请参阅  
 [添加表达式 &#40;报表生成器和 SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)  
  
  
