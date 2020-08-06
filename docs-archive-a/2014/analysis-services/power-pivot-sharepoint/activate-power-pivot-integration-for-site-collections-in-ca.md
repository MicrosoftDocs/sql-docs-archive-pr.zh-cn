---
title: 在管理中心中为网站集激活 PowerPivot 功能集成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 62a27e53-446a-42d7-b5db-c009e02d4904
author: minewiskan
ms.author: owend
ms.openlocfilehash: b565434cba197d04327e833d4ac6eab3caf96646
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689037"
---
# <a name="activate-powerpivot-feature-integration-for-site-collections-in-central-administration"></a>在管理中心中针对网站集激活 PowerPivot 功能集成
  如果您使用了“现有场”安装选项来安装 SQL Server PowerPivot for SharePoint，则需要为特定的网站集激活 PowerPivot 功能集成。 如果您使用“新服务器”选项安装 PowerPivot for SharePoint，则可以跳过此任务，因为 SQL Server 安装程序在配置您的部署时已经为根网站集激活了 PowerPivot 功能集成。  
  
 网站集级别的功能激活是使应用程序页和模板对您的站点可用所必需的，包括用于计划的数据刷新的配置页以及用于 PowerPivot 库和数据馈送库的应用程序页。  
  
 对于支持 PowerPivot 查询处理的每个网站集，您必须激活 PowerPivot 集成。  
  
## <a name="prerequisites"></a>先决条件  
 您必须是网站集管理员。  
  
## <a name="activate-powerpivot-features"></a>激活 PowerPivot 功能  
  
1.  在 SharePoint 站点上，单击 **“网站操作”**。  
  
     默认情况下，通过端口 80 访问 SharePoint Web 应用程序。 这意味着通常可通过输入 http:// 打开根网站集以访问 SharePoint 网站\<computer name>。  
  
2.  单击 **“网站设置”** 。  
  
3.  在“网站集管理”中，单击 **“网站集功能”**。  
  
4.  向下滚动页面，直至找到 " **PowerPivot 集成网站集功能**"。  
  
5.  单击“激活”  。  
  
6.  通过打开各站点并单击 **“网站操作”**，对于其他网站集重复上述操作。  
  
## <a name="see-also"></a>另请参阅  
 [管理中心中的 PowerPivot 服务器管理和配置](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [初始配置 &#40;PowerPivot for SharePoint&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot for SharePoint 2010 安装](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
