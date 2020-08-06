---
title: 默认情况下，功能 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9529edf-337e-4fdd-9a13-99cfe96b4fa1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 87752b8760ffc80e80c87ac1132cae36f2f151b4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689106"
---
# <a name="features-off-by-default-analysis-services"></a>默认情况下功能关闭 (Analysis Services)
  默认情况下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例在设计上是安全的。 因此，可能危及安全的功能默认处于禁用状态。 下列功能在安装后处于禁用状态，如果要使用它们，则必须专门进行启用。  
  
## <a name="feature-list"></a>功能列表  
 若要启用以下功能，请使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 右键单击实例名称，选择“方面”。**** 或者，可通过服务器属性来启用这些功能，如下一节所述。  
  
-   即席数据挖掘 (OpenRowset) 查询  
  
-   链接对象（目标）  
  
-   链接对象（来源）  
  
-   仅侦听本地连接  
  
-   用户定义的函数  
  
## <a name="server-properties"></a>服务器属性  
 可通过服务器属性启用默认情况下处于关闭状态的其他功能。 使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 连接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 右键单击实例名称，选择“属性”。**** 单击 **“常规”**，然后单击 **“显示高级”** ，以显示较大的属性列表。  
  
-   即席数据挖掘 (OpenRowset) 查询  
  
-   允许会话挖掘模型（数据挖掘）  
  
-   链接对象（目标）  
  
-   链接对象（来源）  
  
-   基于 COM 的用户定义函数  
  
-   网络流量记录器跟踪定义（模板）。  
  
-   查询日志记录  
  
-   仅侦听本地连接  
  
-   二进制 XML  
  
-   压缩  
  
-   组关联。 有关详细信息，请参阅 [Thread Pool Properties](../server-properties/thread-pool-properties.md) 。  
  
  
