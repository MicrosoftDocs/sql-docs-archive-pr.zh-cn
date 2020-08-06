---
title: “添加 IP 地址”对话框 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygrouplistener.addipaddress.f1
ms.assetid: 98c9ad3b-ff3c-4c1d-b344-59a72fca137c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5192e6414b34bee6de09d45a7284f25404235dc7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578452"
---
# <a name="add-ip-address-dialog-box-sql-server-management-studio"></a>“添加 IP 地址”对话框 (SQL Server Management Studio)
  本 F1 帮助主题介绍“添加 IP 地址”对话框中的选项****。 可通过 **“新的可用性组侦听器”** 对话框和 **** 或 **的** “指定副本” [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 页的 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] “侦听器” [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]选项卡访问此对话框。  
  
## <a name="prerequisites"></a>先决条件  
 开始向可用性组侦听器添加子网之前，确保了解每个子网的 IP 地址以及子网掩码（对于 IPv4 地址）。  
  
##  <a name="add-ip-address-options"></a><a name="PageOptions"></a>添加 IP 地址选项  
 **子网**  
 使用下拉列表选择要添加到可用性组侦听器的子网地址。 默认情况下，一个子网同时具有 IPv4 地址和 IPv6 地址。 首次使用 **“添加 IP 地址”** 对话框时， **“子网”** 下拉列表将显示承载可用性组副本的每个子网的这两种子网地址。 若要向侦听器添加给定子网，请选择它的子网地址之一。  
  
 完成 **“添加 IP 地址”** 对话框的操作并单击 **“确定”** 后，可以将所选子网地址添加到该侦听器， **“子网”** 下拉列表会筛选出该子网地址。 所有未选定的子网地址仍保留在下拉列表中。 确保为每个子网向侦听器仅添加一个子网地址，否则侦听器创建将失败。  
  
 **地址**  
 使用此字段可为所选子网地址输入一个静态 IP 地址。 请与您的网络管理员联系以获取此 IP 地址。 确保您为所选子网地址输入一个有效的地址，否则侦听器创建将失败。  
  
 **IPv4 地址**  
 如果您选择了子网的 IPv4 子网地址，请在此输入有效的 IPv4 静态地址。  
  
 **子网掩码**  
 对于 IPv4 地址，此只读字段显示所选子网的子网掩码。  
  
 **IPv6 地址**  
 如果您选择了子网的 IPv6 子网地址，请在此输入有效的 IPv6 静态地址。  
  
 **确定**  
 单击以添加已选定其地址的子网，同时添加您指定的静态 IP 地址。 包含这些值的行将添加到 **“新的可用性组侦听器”** 或 **“指定副本”** 对话框的子网网格中。  
  
> [!IMPORTANT]  
>  **“添加 IP 地址”** 对话框并不验证该 IP 地址。 该对话框也不会阻止您为已经添加到可用性组侦听器的子网继续添加其他子网地址。  
  
 **取消**  
 单击以取消所做选择，并返回“新的可用性组侦听程序”**** 对话框或“侦听程序”**** 选项卡，不为任何子网添加静态 IP 地址。  
  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用“将副本添加到可用性组向导”(SQL Server Management Studio)](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 客户端连接 (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
