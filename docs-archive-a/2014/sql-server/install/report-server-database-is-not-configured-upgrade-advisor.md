---
title: " (升级顾问) ，未配置报表服务器数据库 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 072e689da3f43222396f071e607214a2ec494749
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577235"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>未配置报表服务器数据库（升级顾问）
  升级因报表服务器配置不完整而受阻。 未配置报表服务器数据库。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。|  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>说明  
 安装程序只能升级完全配置的报表服务器实例。 若要继续，必须配置 Report Server 数据库，或使用 Microsoft Windows **"控制面板**" 从安装中删除 Report Server 功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 删除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 后，便可升级其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。  
  
## <a name="corrective-action"></a>纠正措施  
 如果尚未配置报表服务器数据库，报表服务器将无法运行，应在升级前将其删除。  
  
 有关卸载的其他信息 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ，请参阅[卸载 Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\))。 此主题说明如何卸载特定版本，它涉及的步骤与以前版本所用的步骤相似。  
  
## <a name="see-also"></a>另请参阅  
 [升级顾问 &#40;Reporting Services 升级问题&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
