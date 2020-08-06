---
title: FILESTREAM 和 FileTable 与 AlwaysOn 可用性组 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], Availability Groups
- FILESTREAM [SQL Server], Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: fdceda9a-a9db-4d1d-8745-345992164a98
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e7de7b4d66890bb5f1fe49799844f666de81f4db
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87585975"
---
# <a name="filestream-and-filetable-with-alwayson-availability-groups-sql-server"></a>FILESTREAM 和 FileTable 与 AlwaysOn 可用性组 (SQL Server)
  本主题包含将 FILESTREAM 和 FileTable 功能与 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]一起使用有关的信息。  
  
 支持所有 FILESTREAM 功能。 故障转移后，FILESTREAM 数据在可读辅助副本和新的主副本上均可访问。  
  
 支持部分 FileTable 功能。 故障转移后，FileTable 数据在主副本上是可访问的，但是在可读辅助副本上不可访问。  
  
 **本主题内容：**  
  
-   [先决条件](#Prerequisites)  
  
-   [为 FILESTREAM 和 FileTable 访问使用虚拟网络名称 (VNN)](#vnn)  
  
-   [相关任务](#RelatedTasks)  
  
-   [相关内容](#RelatedContent)  
  
##  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   在将使用 FILESTREAM 的数据库（具有或不具有 FileTable）添加到某一可用性组之前，请确保在承载该可用性组的可用性副本的每个服务器实例上都启用 FILESTREAM。 有关详细信息，请参阅 [Enable and Configure FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)。  
  
##  <a name="using-virtual-network-names-vnns-for-filestream-and-filetable-access"></a><a name="vnn"></a>为 FILESTREAM 和 FileTable 访问使用虚拟网络名称 (Vnn)   
 当您在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例上启用 FILESTREAM 时，将创建实例级别共享以便提供对 FILESTREAM 数据的访问。 可通过按以下格式使用计算机名称来访问此共享：  
  
 `\\<computer_name>\<filestream_share_name>`  
  
 但在 AlwaysOn 可用性组中，通过使用虚拟网络名称 (VNN) 虚拟化计算机的名称。 在该计算机是某一可用性组中的主副本，并且该可用性组中的数据库包含 FILESTREAM 数据时，还创建 VNN 范围的共享以便提供对 FILESTREAM 数据的访问。 这并不影响对 FILESTREAM 数据的 Transact-SQL 访问。 但是，使用文件系统 API 的应用程序必须使用 VNN 范围的共享，它具有以下格式的路径：  
  
 `\\<VNN>\<filestream_share_name>`  
  
 在发生以下事件之一时将创建 VNN 范围的共享。  
  
-   您将包含 FILESTREAM 数据的数据库添加到主副本上的 AlwaysOn 可用性组。 在此情况下，共享 `\\<computer_name>\<filestream_share_name>` 已存在。 创建共享 `\\<VNN>\<filestream_share_name>` 。  
  
-   您对具有可用性组的主副本上的文件 i/o 流访问启用 FILESTREAM。 创建以下共享：  
  
    1.  `\\<computer_name>\<filestream_share_name>`  
  
    2.  `\\<VNN1>\<filestream_share_name>` 。  
  
    3.  `\\<VNN2>\<filestream_share_name>` 。  
  
 这些 VNN 范围的共享也传播到所有辅助副本。  
  
 在包含 FILESTREAM 或 FileTable 数据的数据库属于某一 AlwaysOn 可用性组时：  
  
-   FILESTREAM 和 FileTable 函数接受或返回虚拟网络名称 (VNN)，而非计算机名称。 有关这些函数的详细信息，请参阅 [Filestream 和 FileTable 函数 (Transact-SQL)](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)。  
  
-   通过文件系统 API 对 FILESTREAM 或 FileTable 数据进行的所有访问都应该使用 VNN，而非计算机名称。  
  
 在该数据库是某一可用性组的一部分时，如果您的应用程序尝试使用格式为 `\\<computer_name>\<filestream_share_name>` 的计算机名称访问该共享，将会引发错误。  
  
 在该数据库不是某一可用性组的一部分时，如果您的应用程序尝试使用 VNN 范围的路径访问该共享，则该请求可能会成功。 在此情况下，虚拟网络名称将解析为计算机名称。 但是，强烈不推荐这一用法，因为如果删除该可用性组，该 VNN 范围的路径将会停止。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [启用和配置 FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)  
  
-   [启用 FileTable 的先决条件](../../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相关内容  
 无。  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
