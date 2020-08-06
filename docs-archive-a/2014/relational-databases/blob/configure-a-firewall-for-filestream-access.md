---
title: 将防火墙配置为允许 FILESTREAM 访问 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8b787403fefdd336dd82bf7ccb93cdf21fe5a90d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589723"
---
# <a name="configure-a-firewall-for-filestream-access"></a>将防火墙配置为进行 FILESTREAM 访问
  若要在防火墙保护的环境中使用 FILESTREAM，客户端和服务器都必须能够将 DNS 名称解析为包含 FILESTREAM 文件的服务器。 FILESTREAM 要求 Windows 文件共享端口 139 和 445 处于打开状态。  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>在运行 Windows 7 的计算机上打开 Windows 文件共享端口  
  
1.  在“控制面板”中，打开 **“Windows 防火墙”** 。  
  
2.  在左窗格中，单击 **“高级设置”** 。 如果系统提示需要管理员密码或确认，请键入密码或进行确认。  
  
3.  在 **“高级安全 Windows 防火墙”** 对话框的左窗格中，单击 **“入站规则”** ，然后在右窗格中单击 **“新建规则”** 。  
  
4.  按照“新建入站规则”向导中的说明添加 TCP 端口 139。  
  
5.  重复上述步骤添加 TCP 端口 445。  
  
6.  关闭 **“高级安全 Windows 防火墙”** 对话框。  
  
  
