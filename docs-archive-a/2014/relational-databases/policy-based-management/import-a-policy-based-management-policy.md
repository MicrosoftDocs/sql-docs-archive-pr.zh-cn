---
title: 导入基于策略的管理策略 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d83ed589e147c61b1692447aacb17535f18a5c9e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578174"
---
# <a name="import-a-policy-based-management-policy"></a>导入基于策略的管理策略
  本主题介绍如何通过使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中导入基于策略的管理策略实例。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要导入策略实例，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 附带可用于监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的策略。 默认情况下，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中未安装这些策略；不过，可以从默认安装位置 C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 导入这些策略。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 要求具有 msdb 数据库中 PolicyAdministratorRole 角色的成员身份。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-import-a-policy-instance"></a>导入策略实例  
  
1.  在“对象资源管理器”  中，单击加号以展开新导入的策略实例要存储到的服务器。  
  
2.  单击加号以便展开 **“管理”** 文件夹。  
  
3.  单击加号以便展开 **“策略管理”** 。  
  
4.  右键单击“策略”  文件夹，然后选择“导入策略”  。  
  
5.  在“导入”  对话框中，键入该文件的路径和名称；或者使用“浏览”按钮 ( **...** ) 查找包含策略的 XML 文件，然后选择该文件。 有关 **“导入”** 对话框中可用选项的详细信息，请参阅 [Import Policies Dialog Box](import-policies-dialog-box.md)。  
  
6.  完成后，单击 **“确定”** 。  
  
  
