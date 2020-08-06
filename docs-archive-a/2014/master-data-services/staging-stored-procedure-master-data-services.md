---
title: 临时存储过程 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9259352350a099db5d9b18411ad4da06dfb19819
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591444"
---
# <a name="staging-stored-procedure-master-data-services"></a>临时存储过程 (Master Data Services)
  从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]启动临时过程时，您使用三个存储过程之一。  
  
-   stg.udp_name_Leaf  
  
-   stg.udp_name_Consolidated  
  
-   stg.udp_name_Relationship  
  
 其中 name 是创建实体时指定的临时表的名称。  
  
## <a name="staging-process-stored-procedure-parameters"></a>临时过程存储过程参数  
 下表列出了这些存储过程的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|**VersionName**<br /><br /> 必需|版本的名称。 这可能区分大小写，也可能不区分，具体取决于您的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 排序规则设置。|  
|**LogFlag**<br /><br /> 必需|确定在临时过程中是否记录事务。 可能的值包括：<br /><br /> **0**：不记录事务。<br />**1**：记录事务。<br /><br /> <br /><br /> 有关事务的详细信息，请参阅[事务 (Master Data Services)](transactions-master-data-services.md)。|  
|**BatchTag**<br /><br /> 必需，但是 Web 服务除外|在临时表中指定 **BatchTag** 值。|  
|**Batch_ID**<br /><br /> 仅对 Web 服务为必需的|在临时表中指定的 **Batch_ID** 值。|  
  
### <a name="staging-process-stored-procedure-example"></a>临时过程存储过程示例  
 下面的示例说明了如何使用临时存储过程启动临时过程。  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [验证存储过程 &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md)   
 [通过使用临时过程在 Master Data Services 中加载或更新成员](add-update-and-delete-data-master-data-services.md)   
 [查看临时过程中发生的错误 &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)  
  
  
