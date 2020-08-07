---
title: 查找服务器（网络服务器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.browseservers.network.f1
ms.assetid: a59ffcd6-4b69-4c5c-9740-699ccb2183fb
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0ba5e4e5dd6d9a6541a98e0cb30229d7335bac24
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588071"
---
# <a name="browse-for-servers-network-servers"></a><span data-ttu-id="db3cf-102">查找服务器（网络服务器）</span><span class="sxs-lookup"><span data-stu-id="db3cf-102">Browse for Servers (Network Servers)</span></span>
  <span data-ttu-id="db3cf-103">如果要连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 组件但不知道 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的确切名称，请在“服务器名称”\*\*\*\* 框中单击“浏览更多”\*\*\*\*，以打开“查找服务器”\*\*\*\* 对话框。</span><span class="sxs-lookup"><span data-stu-id="db3cf-103">If you are connecting to a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] component and you do not know the exact name of the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance, click **Browse for more** in the **Server name** box to open the **Browse for Servers** dialog box.</span></span>  
  
 <span data-ttu-id="db3cf-104">将通过服务器计算机上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务填充此对话框。</span><span class="sxs-lookup"><span data-stu-id="db3cf-104">This dialog is populated by the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser service on the server computers.</span></span> <span data-ttu-id="db3cf-105">列表中未显示实例名称的原因有多种：</span><span class="sxs-lookup"><span data-stu-id="db3cf-105">There are several reasons why the name of an instance might not appear in the list:</span></span>  
  
-   <span data-ttu-id="db3cf-106">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服务可能未在运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="db3cf-106">The [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser service might not be running on the computer running [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].</span></span>  
  
-   <span data-ttu-id="db3cf-107">UDP 端口 1434 可能被防火墙阻塞。</span><span class="sxs-lookup"><span data-stu-id="db3cf-107">UDP port 1434 might be blocked by a firewall.</span></span>  
  
-   <span data-ttu-id="db3cf-108">可能设置了 **HideInstance** 标志。</span><span class="sxs-lookup"><span data-stu-id="db3cf-108">The **HideInstance** flag might be set.</span></span>  
  
 <span data-ttu-id="db3cf-109">若要连接到列表中未列出的实例，请键入该实例的完整连接字符串，其中包括 TCP/IP 端口号或 Named Pipes 管道名称。</span><span class="sxs-lookup"><span data-stu-id="db3cf-109">To connect to an instance that does not appear in the list, type a full connection string for the instance, including the TCP/IP port number or the named pipes pipe name.</span></span>  
  
## <a name="options"></a><span data-ttu-id="db3cf-110">选项</span><span class="sxs-lookup"><span data-stu-id="db3cf-110">Options</span></span>  
 <span data-ttu-id="db3cf-111">**在网络中选择要连接的 SQL Server 实例**</span><span class="sxs-lookup"><span data-stu-id="db3cf-111">**Select a SQL Server instance in the network for your connection**</span></span>  
 <span data-ttu-id="db3cf-112">单击树中显示的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例，指定要连接的服务器。</span><span class="sxs-lookup"><span data-stu-id="db3cf-112">Designate the server you want to connect to by clicking on the [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance displayed in the tree.</span></span> <span data-ttu-id="db3cf-113">您可以通过单击标有或符号的节点来显示或隐藏部分树视图 **+** **-** 。</span><span class="sxs-lookup"><span data-stu-id="db3cf-113">You can show or hide portions of the tree view by clicking on the nodes marked with a **+** or **-** symbol.</span></span>  
  
  
