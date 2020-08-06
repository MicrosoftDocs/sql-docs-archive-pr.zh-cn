---
title: 在 SharePoint 模式下将文档上载到 SharePoint 库 (Reporting Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- SharePoint integration [Reporting Services], content management
- uploading reports [Reporting Services]
ms.assetid: 93bd1b19-061b-409f-8dc2-ec416b2f4b39
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 74b39f90cd90dc8a92a5f10168d98f165c211c51
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692207"
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>将文档上载到 SharePoint 库（SharePoint 模式下的 Reporting Services）
  您可以将报表定义和报表模型上载到 SharePoint 库。 上载报表服务器项时，您必须选择一个库或库中的一个文件夹。 不能将报表服务器项上载到某个列表或页。  
  
 不能上载数据源 (.rds) 文件。 但是，可以从设计工具（如报表设计器）中向 SharePoint 库发布 .rds 文件。 在发布期间，将根据解决方案中的原始 .rds 文件创建一个新的 .rsds 文件。 您也可以在 SharePoint 库中创建一个新的 .rsds 文件，然后在上载的报表和模型中设置数据源连接属性以使用新的连接。  
  
> [!NOTE]  
>  报表服务器必须配置为使用 SharePoint 模式，且 SharePoint 产品的实例必须安装了 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 外接程序，此外接程序提供了从 SharePoint 站点中存储和访问报表服务器项的程序文件。  
  
 若要将文档上载到库中，您必须拥有站点级别的“添加项”权限。 如果您使用的是默认安全设置，将对拥有“完全控制”级别权限的“所有者” **** 组成员和拥有“参与讨论”级别权限的“成员” **** 组授予该权限。  
  
### <a name="to-add-a-report-definition-or-report-model-to-a-library"></a>向库中添加报表定义或报表模型  
  
1.  打开库或库中的某个文件夹。 如果库尚未打开，请在“快速启动”上单击其名称。 如果未显示库的名称，请单击 **“查看所有网站内容”**，然后单击库的名称。  
  
2.  在 **“上载”** 菜单中，单击 **“上载文档”**。  
  
3.  若要上传单个报表或报表模型文件，请选择报表定义 (.rdl) 或报表模型 (.smdl) 文件，然后单击“确定”****。  
  
     如果报表定义使用共享数据源 (.rsds) 文件存储与外部数据源的连接信息，则可以同时上载 .rdl 和 .rsds 文件。 为此，请单击 **“上载多个文档”**，指定这两个文件，然后单击 **“确定”**。  
  
 如果您上载的报表包含对共享数据源、报表模型或子报表的引用，则文件上载后这些引用将会断开。 有关如何重置引用的详细信息，请参阅[创建和管理共享数据源（SharePoint 集成模式下的 Reporting Services）](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)。  
  
 上载报表后，它将在打开时按需运行，并从数据源检索实时数据。 您可以将报表配置为按计划检索数据或使用缓存数据。 有关详细信息，请参阅[设置处理选项（SharePoint 集成模式下的 Reporting Services）](../../2014/reporting-services/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)。  
  
 报表可以包含参数以便用户能够筛选数据。 您可以将参数配置为使用特定值或更改参数对用户的显示方式。 有关详细信息，请参阅[在已发布报表上设置参数（SharePoint 集成模式下的 Reporting Services）](report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
## <a name="see-also"></a>另请参阅  
 [将报表发布到 SharePoint 库](reports/publish-a-report-to-a-sharepoint-library.md)   
 [将共享数据源发布到 SharePoint 库](reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
