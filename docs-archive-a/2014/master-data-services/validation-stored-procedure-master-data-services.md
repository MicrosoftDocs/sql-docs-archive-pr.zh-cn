---
title: 验证存储过程 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 8fa6b01d950c87768d10b0252c1ccbab2b932fe1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586764"
---
# <a name="validation-stored-procedure-master-data-services"></a>验证存储过程 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，对某一版本进行验证以便将业务规则应用于该模型版本中的所有成员。  
  
 本主题说明如何使用 **mdm.udpValidateModel** 存储过程来验证数据。 如果您是 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序的管理员，可以在 UI 中进行验证。 有关详细信息，请参阅 [针对业务规则验证版本 (Master Data Services)](validate-a-version-against-business-rules-master-data-services.md)。  
  
> [!NOTE]  
>  如果在临时过程完成前调用验证，将不验证未完成暂存的成员。  
  
## <a name="example"></a>示例  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>参数  
 此过程的参数如下所示：  
  
|参数|说明|  
|---------------|-----------------|  
|UserID|用户 ID。|  
|Model_ID|模型 ID。|  
|Version_ID|版本 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [数据导入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [针对业务规则验证版本 (Master Data Services)](validate-a-version-against-business-rules-master-data-services.md)  
  
  
