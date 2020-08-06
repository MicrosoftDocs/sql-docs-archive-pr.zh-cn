---
title: 将报表保存到 SharePoint 库（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 49878a0d7115a11e804382cb5139aa0ec7b3d254
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586474"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>将报表保存到 SharePoint 库（报表生成器）
  若要将报表保存到配置为 SharePoint 集成模式的报表服务器，必须找到 SharePoint 服务器并建立与报表服务器的连接。 在报表定义中，对与报表相关的项的所有引用都必须使用特定于 SharePoint 报表服务器的值。 相关项包括子报表、钻取报表和基于 Web 的图像等资源。 有关详细信息，请参阅[指定外部项的路径（报表生成器和 SSRS）](../report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 必须对 SharePoint 站点拥有 **“成员”** 或 **“所有者”** 权限，才能设置项目的属性。  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>将报表保存到 SharePoint 站点  
  
1.  从“报表生成器”按钮，单击 **“保存”**。 此时将打开 "**另存为**" _\<Report Item>_ 对话框。  
  
    > [!NOTE]  
    >  如果正在重新保存报表，会自动将其重新保存到以前的位置。 使用 **“另存为”** 选项可以更改位置。  
  
2.  或者，单击 **“最近使用的站点和服务器”** 以显示最近使用的报表服务器和 SharePoint 站点的列表。  
  
3.  找到 SharePoint 站点，然后单击 **“保存”**。  
  
    > [!NOTE]  
    >  如果超过 10 小时未对已更改的报表进行保存，则该报表将断开与服务器的连接，而且未保存。 如果发生这种情况，请在右下角的状态栏中单击“断开连接”，然后单击“连接”********。 最近的服务器将位于可用服务器列表中。 选择该服务器，并且报表将重新连接。  
  
## <a name="see-also"></a>另请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
