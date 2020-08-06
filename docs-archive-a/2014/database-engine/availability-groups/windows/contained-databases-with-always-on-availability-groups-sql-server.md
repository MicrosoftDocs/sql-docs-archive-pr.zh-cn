---
title: 包含的数据库与 AlwaysOn 可用性组 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- contained database [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: cacce3ae-e940-4566-8298-6607c4268e74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 74c8a0b41ee7224dad83fb41691a4898c15b7b38
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577854"
---
# <a name="contained-databases-with-always-on-availability-groups-sql-server"></a>包含的数据库与 Always On 可用性组 (SQL Server)
  本主题包含将包含数据库用于 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的相关信息。  
  
 **本主题内容：**  
  
-   [先决条件](#Prerequisites)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   在将包含数据库添加到某一可用性组之前，请确保在承载该可用性组的可用性副本的每个服务器实例上 `contained database authentication` 服务器选项都设置为 `1`。 有关详细信息，请参阅 [contained database authentication 服务器配置选项](../../configure-windows/contained-database-authentication-server-configuration-option.md) 和 [服务器配置选项 (SQL Server)](../../configure-windows/server-configuration-options-sql-server.md)的相关信息。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [服务器配置选项 (SQL Server)](../../configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [包含的数据库](../../../relational-databases/databases/contained-databases.md)  
  
  
