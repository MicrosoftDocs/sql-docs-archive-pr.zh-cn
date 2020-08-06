---
title: 通过 Internet 复制 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web publishing [SQL Server replication], about Web publishing
- Web publishing [SQL Server replication]
- Internet [SQL Server replication]
- Internet [SQL Server replication], publishing
ms.assetid: 04e7f4ed-e244-4bbe-ba12-09c33abea09e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 46c61f8a5383c87d46fa0dbda18876b43ffb7739
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577519"
---
# <a name="replication-over-the-internet"></a>通过 Internet 复制
  通过 Internet 复制数据，可以使断开连接的远程用户在需要时使用到 Internet 的连接访问数据。 使用以下方式在 Internet 上复制数据：  
  
-   虚拟专用网络 (VPN)。 有关详细信息，请参阅[使用 VPN 通过 Internet 发布数据](publish-data-over-the-internet-using-vpn.md)。  
  
-   对于合并复制，使用 Web 同步选项。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)。  
  
 所有类型的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制都可以通过 VPN 来复制数据。但如果使用的是合并复制，应考虑使用 Web 同步。  
  
  
