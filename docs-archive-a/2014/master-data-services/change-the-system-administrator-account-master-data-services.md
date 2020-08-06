---
title: 更改系统管理员帐户 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1d13cdc19c70c9e16c92dfd290393739d7e4f5e9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690685"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>更改系统管理员帐户 (Master Data Services)
  你可以更改指定为系统管理员的用户帐户 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 。  
  
> [!WARNING]  
>  当您完成此过程后，将删除旧系统管理员用户帐户。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   必须将新管理员的用户名添加到[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]的“用户”列表中。 有关详细信息，请参阅[Add a User &#40;Master Data Services&#41;](add-a-user-master-data-services.md)。  
  
-   您必须有权查看 mdm.tblUser 和在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库中执行 mdm.udpSecurityMemberProcessRebuildModel 存储过程。 有关详细信息，请参阅[数据库对象安全性 (Master Data Services)](../../2014/master-data-services/database-object-security-master-data-services.md)。  
  
### <a name="to-change-the-administrator-account"></a>更改管理员帐户  
  
1.  打开 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 并连接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 数据库的 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 实例。  
  
2.  在 tblUser 中，找到要成为新管理员的用户，并复制列中的值 `SID` 。  
  
3.  创建新查询。  
  
4.  键入以下文本，将*DOMAIN \ user_name*替换为新管理员的用户名，将*SID*替换为在步骤2中复制的值。  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  运行查询。  
  
## <a name="see-also"></a>另请参阅  
 [管理员 (Master Data Services)](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
