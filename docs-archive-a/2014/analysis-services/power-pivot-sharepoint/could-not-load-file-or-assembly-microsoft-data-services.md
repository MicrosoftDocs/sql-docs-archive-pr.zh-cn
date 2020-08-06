---
title: 未能加载文件或程序集 &#39;Microsoft.analysisservices.sharepoint.integration.dll&#39; |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
author: minewiskan
ms.author: owend
ms.openlocfilehash: b7ba75bdbd8e25f98d11d822c22fa7881352ad88
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589284"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>未能加载文件或程序集 &#39;Microsoft.analysisservices.sharepoint.integration.dll&#39;
  在具有 PowerPivot for SharePoint 的 SharePoint 2010 环境中，如果用于 PowerPivot 的应用程序级别的解决方案未正确部署，将发生此错误。  
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|适用于|PowerPivot for SharePoint|  
|产品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|Powerpivotwebapp 解决方案未部署或者未正确部署。|  
|消息正文|无法加载文件或程序集“Microsoft.AnalysisServices.SharePoint.Integration”|  
  
## <a name="explanation"></a>说明  
 PowerPivot for SharePoint 使用解决方案包在 SharePoint 服务器上部署其功能。 解决方案之一未正确部署。 因此，只要您尝试在 SharePoint 站点上打开 PowerPivot 库或者其他 PowerPivot 应用程序页，就会出现此错误。  
  
## <a name="user-action"></a>用户操作  
 部署解决方案包。  
  
1.  在管理中心的“系统设置”中，单击 **“管理场解决方案”**。  
  
2.  单击 **“Powerpivotwebapp”**。  
  
3.  单击 **“部署解决方案”**。  
  
4.  选择发生了此错误的 Web 应用程序。 如果存在多个 Web 应用程序，则为所有这些应用程序都重新部署解决方案。  
  
5.  单击“确定”。  
  
## <a name="see-also"></a>另请参阅  
 [将 PowerPivot 解决方案部署到 SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
