---
title: 教程：准备用于复制的服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1f036ff2a111ee6b5f97655b9bebaf34391a436
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591230"
---
# <a name="tutorial-preparing-the-server-for-replication"></a>教程：准备用于复制的服务器
  在配置复制拓扑之前，制定安全计划是非常重要的。 本教程向您介绍如何更好地保护复制拓扑以及如何配置分发，这是复制数据的第一步。 开始其他教程之前，必须先完成本教程。  
  
> [!NOTE]  
>  若要在服务器之间安全地复制数据，你应该实施 [复制安全最佳实践](security/replication-security-best-practices.md)中提出的所有建议。  
  
## <a name="what-you-will-learn"></a>学习内容  
 在本教程中，您将了解如何准备服务器以便用最少的特权安全地运行复制。 第一课介绍如何创建用于运行复制代理的 Windows 服务帐户。 第二课介绍如何配置用于生成和存储发布快照的文件夹。 第三课介绍如何配置分发以及如何设置权限。  
  
## <a name="requirements"></a>要求  
 本教程适用于熟悉基本数据库操作，但对复制认识有限的用户。  
  
 若要使用本教程，系统中必须安装下列组件：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 数据库的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 。 为了增强安全性，默认情况下不会安装示例数据库。  
  
 **本教程的估计完成时间：30分钟。**  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
  
-   [第 1 课：为复制创建 Windows 帐户](lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [第 2 课：准备快照文件夹](lesson-2-preparing-the-snapshot-folder.md)  
  
-   [第 3 课：配置分发](lesson-3-configuring-distribution.md)  
  
 [开始教程](lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>另请参阅  
 [“配置分发”](configure-distribution.md)   
 [SQL Server 复制安全性](security/view-and-modify-replication-security-settings.md)  
  
  
