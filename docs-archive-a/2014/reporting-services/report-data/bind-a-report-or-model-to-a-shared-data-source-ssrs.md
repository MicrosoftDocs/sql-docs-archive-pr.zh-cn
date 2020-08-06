---
title: 将报表或模型绑定到共享数据源 (SSRS)| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 596caba042d476173b3c49d1ad18e79d0827fe89
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688603"
---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>将报表或模型绑定到共享数据源 (SSRS)
  在某些情况下，例如将报表或模型从测试服务器移到生产服务器时，最好将文件保存到本地计算机，然后将其上载到其他报表服务器。 将报表或模型上载到新服务器时，需要将其重新绑定到存储在新报表服务器上的共享数据源。 如果不重新绑定报表或模型，在从新报表服务器对其进行访问时，报表或模型将无法正常工作。  
  
> [!IMPORTANT]  
>  在将报表或模型重新绑定到共享数据源之前，报表服务器或 SharePoint 库中必须已经存在该数据源。 有关数据源的详细信息，请参阅[创建、修改和删除共享数据源 (SSRS)](create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>将报表或模型绑定到在本机模式下运行的报表服务器上的共享数据源  
  
1.  在 **报表管理器**中，单击已上载到服务器的报表或模型的名称。  
  
     将打开“属性”选项卡。  
  
2.  单击 **“数据源”**。  
  
3.  单击 **“浏览”**，然后导航到要绑定报表或模型的数据源。  
  
4.  选择数据源，然后单击 **“确定”**。  
  
5.  单击“应用”。  
  
     此时，报表或模型已绑定到您选择的数据源。  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>将报表或模型绑定到在 SharePoint 集成模式下运行的报表服务器上的共享数据源  
  
1.  如果尚未打开库，请在“快速启动”栏上单击其名称。 如果未显示库的名称，请单击 **“查看所有网站内容”**，然后单击库的名称。  
  
2.  指向报表或模型，然后单击向下箭头。  
  
3.  单击 **“管理数据源”**。  
  
4.  单击 **“dataSource1”**。  
  
5.  在 **“连接类型”** 区域中，确认已选中 **“共享数据源”** 。  
  
6.  在“数据源链接”区域中，单击省略号 (...) 按钮****。  
  
7.  找到要使用的数据源。  
  
8.  选择数据源并单击 **“确定”**。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 单击“关闭”。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器 &#40;上传文件或报表&#41;](../reports/upload-a-file-or-report-report-manager.md)   
 [在 SharePoint 模式下将文档上传到 SharePoint 库 &#40;Reporting Services&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [在 SharePoint 集成模式下创建和管理共享数据源 &#40;Reporting Services&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [创建、删除或修改共享数据源 &#40;报表管理器&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Reporting Services 中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
