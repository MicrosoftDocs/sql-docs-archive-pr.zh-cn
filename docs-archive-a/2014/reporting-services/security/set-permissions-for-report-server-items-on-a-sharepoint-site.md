---
title: 为 sharepoint 站点上的报表服务器项设置权限) SharePoint 集成模式下的 (Reporting Services |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
ms.assetid: 2467c657-a3bf-4ec3-a88c-8877df19823d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f38497843ca99342f13952153d7fed957564e006
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688480"
---
# <a name="set-permissions-for-report-server-items-on-a-sharepoint-site-reporting-services-in-sharepoint-integrated-mode"></a>在 SharePoint 站点上为报表服务器项设置权限（SharePoint 集成模式下的 Reporting Services）
  如果默认安全设置未提供您需要的访问权限级别，则可以创建新的权限级别以提供对特定报表服务器项或操作的访问权限。 如果希望限制对特定报表的访问权限，则自定义安全设置非常有用。  
  
 您必须是站点所有者才能创建权限级别和组。 权限级别通用于整个站点。 如果您创建新的权限级别，其他站点所有者也将可以使用它。  
  
 大多数权限都继承自父站点。 如果您对特定库或项分配权限，则会中断权限继承并引发额外开销，即如何管理站点层次结构中该分支的权限。  
  
 可以对报表定义 (.rdl)、模型 (.smdl) 和共享数据源 (.rsds) 文件设置权限。 无法在同一个项目上结合使用继承的权限和托管的权限。 如果选择直接管理权限，则继承的权限将不会对当前项产生任何影响。 如果希望以后恢复权限继承，则可以选择 **“操作”** 菜单中的 **“继承权限”** 。  
  
 若要设置对模型中的实体和透视的权限，您必须拥有该模型的“完全控制”级权限。 “完全控制”包括“管理权限”，后者是授予站点所有者和其他拥有“完全控制”级权限的 SharePoint 组的站点级权限。 如果希望使特定用户能够设置模型项安全性，则必须中断权限继承并授予用户或组对该模型文件的提升权限（如“完全控制”）。 授予对某项（如库中的文件）的“完全控制”权限时，权限的作用域将仅限于该项，不会扩展到父项或同一库中的其他项。 用户拥有模型的“管理权限”权限后，便可以通过 SharePoint 站点或模型设计器设置模型项安全性。  
  
### <a name="to-set-permissions-on-an-individual-report-model-or-data-source"></a>对单个报表、模型或数据源设置权限  
  
1.  如果库尚未打开，请在“快速启动”上单击其名称。 如果未显示库的名称，请单击 **“查看所有网站内容”** ，然后单击库的名称。  
  
2.  指向报表、报表模型或共享数据源文件。  
  
3.  单击向下箭头，并在菜单上单击 **“管理权限”** 。  
  
4.  在 **“操作”** 菜单上，单击 **“编辑权限”** ，然后单击 **“确定”** 以确认此操作。  
  
5.  若要为尚未拥有文件使用权限的用户或组授予权限，请单击 **“新建”** ，然后单击 **“添加用户”** 。  
  
6.  若要删除或修改现有用户或组的权限，请单击用户或组旁边的复选框，单击 **“操作”** ，然后单击 **“删除用户权限”** 或 **“编辑用户权限”** 。  
  
### <a name="to-set-permissions-that-enable-model-item-security"></a>设置启用模型项安全性的权限  
  
1.  使用拥有 SharePoint 站点的“管理权限”权限的帐户登录该站点。  
  
2.  打开包含模型的库。  
  
3.  指向模型。  
  
4.  单击该模型旁边的向下箭头，并单击 **“管理权限”** 。  
  
5.  单击 **“操作”** 。  
  
6.  单击 **“编辑权限”** 。 单击“确定”。   
  
7.  单击 **“新建”** 。  
  
8.  单击“添加用户”。   
  
9. 在“用户/组”中输入用户帐户。  
  
10. 选择 **“直接授予用户权限”** 。  
  
11. 单击 **“完全控制”** 。  
  
12. 单击“确定”。  用户具备管理特定模型权限的能力后，便可以打开模型并在模型内编辑权限。  
  
## <a name="see-also"></a>另请参阅  
 [将 Windows SharePoint Services 中的内置安全性用于报表服务器项](use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)   
 [在 SharePoint Web 应用程序中设置报表服务器操作的权限](set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Reporting Services 中的角色和任务与 SharePoint 组和权限的比较](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [报表服务器项的 SharePoint 站点和列表权限参考](sharepoint-site-and-list-permission-reference-for-report-server-items.md)   
 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
