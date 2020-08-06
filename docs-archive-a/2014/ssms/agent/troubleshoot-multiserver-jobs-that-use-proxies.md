---
title: 排除使用代理的多服务器作业的故障 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19de975ef5e1f22c93cec72a5014a01da5b03dd8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689227"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>排除使用代理的多服务器作业的故障
  如果分布式作业的步骤与某个代理关联，则该作业将在目标服务器上该代理帐户的上下文中运行。 如果从主服务器下载使用代理帐户的作业步骤时失败，则请检查 **msdb** 数据库中 **sysdownloadlist** 表的 **error_message** 列是否存在下列错误消息：  
  
-   “该作业步骤需要代理帐户，但是目标服务器上禁用了代理匹配功能。”  
  
     若要解决此错误，请设置**\ HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\MSSQL.**_ \<n_> **\SQLServerAgent\AllowDownloadedJobsToMatchProxyName**注册表子项**设置为 1 () 为 true **。 默认情况下，此子项设置为**0** (`false`) 。 MSSQL 的值 **。**\<*n*> 是实例名称;例如， **mssql. 1**或**mssql. 3**。  
  
-   “找不到代理。”  
  
     若要解决此错误，请确保目标服务器上已存在与运行作业步骤的主服务器代理帐户同名的代理帐户。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [创建多服务器环境](create-a-multiserver-environment.md)  
  
  
