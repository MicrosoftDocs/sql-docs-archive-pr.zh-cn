---
title: 授予用户对报表服务器的访问权限 (报表管理器) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bceaa648827d756e2b301662ce281b37a76d6839
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688487"
---
# <a name="grant-user-access-to-a-report-server-report-manager"></a>授予用户对报表服务器的访问权限（报表管理器）
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用基于角色的安全性向用户授予对报表服务器的访问权限。 在新安装的报表服务器上，只有作为本地 Administrators 组的成员的用户具有对报表服务器内容和操作的权限。 若要使其他用户可以使用报表服务器，必须创建将用户帐户或组帐户映射到指定任务集合的预定义角色的角色分配。  
  
 **SharePoint 模式报表服务器：** 对于配置为 SharePoint 集成模式的报表服务器，使用 SharePoint 权限从 SharePoint 站点配置访问权限。 对 SharePoint 站点的权限级别确定对报表服务器内容和操作的访问权限。 您必须是站点管理员才能授予对 SharePoint 站点的权限。 有关详细信息，请参阅 [在 SharePoint 站点上授予对报表服务器项的权限](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)。  
  
 **本机模式报表服务器：** 本主题侧重于配置为本机模式的报表服务器以及使用报表管理器向角色分配用户。 有两种类型的角色：  
  
-   项级角色用于查看、添加和管理报表服务器内容、订阅、报表处理和报表历史记录。 可以对根节点（主文件夹）或位于该层次结构中的特定下级文件夹或项定义项级角色分配。  
  
-   系统级角色授予对不限于任何特定项的站点范围操作的访问权限。 例如，使用报表生成器和使用共享计划。  
  
     两种类型的角色互为补充，应结合使用。 因此，将用户添加到报表服务器的操作分为两个部分。 如果将用户分配到项级角色，则还应将该用户分配到系统级角色。 将用户分配到角色时，必须选择已定义的角色。 若要创建、修改或删除角色，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 有关详细信息，请参阅 [创建、删除或修改角色 (Management Studio)](role-definitions-create-delete-or-modify.md)。  
  
## <a name="before-you-start"></a>开始之前  
 在将用户添加到本机模式的报表服务器之前查看以下列表。  
  
-   您必须是报表服务器计算机上本地 Administrators 组的成员。 如果在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 Windows Server 2008 上部署 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] ，则需要进行额外配置，然后才能在本地管理报表服务器。 有关详细信息，请参阅 [为本地管理配置本机模式报表服务器 (SSRS)](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
-   若要将此任务委托给其他用户，请创建将用户帐户映射到“内容管理员”和“系统管理员”角色的角色分配。 具有“内容管理员”和“系统管理员”权限的用户可以将用户添加到报表服务器。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，查看“系统角色”和“用户角色”的预定义角色，以便熟悉每个角色中的各种任务。 由于报表管理器中不显示任务说明，因此需要在开始添加用户之前熟悉角色。  
  
-   根据需要自定义这两个角色或定义其他角色以包括所需的任务集合。 例如，如果计划对单独的项使用自定义安全设置，则可能希望创建新的角色定义以授予对文件夹的查看访问权限。  
  
### <a name="to-add-a-user-or-group-to-a-system-role"></a>向系统角色添加用户或组  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  单击 **“网站设置”** 。  
  
3.  单击 **“安全性”** 。  
  
4.  单击 **“新建角色分配”**。  
  
5.  在 "**组或用户名**" 中，按以下格式输入 Windows 域用户或组帐户： \<domain> \\<帐户 \> 。 如果使用窗体身份验证或自定义安全性，则以适用于您的部署的格式指定该用户帐户或组帐户。  
  
6.  选择一个系统角色，然后单击 **“确定”**。  
  
     角色是可累积的，因此如果同时选择了“系统管理员”和“系统用户”，则用户或组可以执行这两种角色的任务。  
  
7.  重复上述步骤，为其他用户或组创建分配。  
  
### <a name="to-add-a-user-or-group-to-an-item-role"></a>向项角色添加用户或组  
  
1.  启动 **“报表管理器”** 并找出您要为其添加用户或组的报表项。  
  
2.  悬停在该项之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击“安全性”****。  
  
4.  单击 **“新建角色分配”**。  
  
    > [!NOTE]  
    >   如果某项当前从父项继承安全性，则在工具栏中单击 **“编辑项安全设置”** 可以更改安全设置。 然后，单击 **“新建角色分配”**。  
  
5.  在 "**组或用户名**" 中，按以下格式输入 Windows 域用户或组帐户： \<domain> \\<帐户 \> 。 如果使用窗体身份验证或自定义安全性，则以适用于您的部署的格式指定该用户帐户或组帐户。  
  
6.  选择一个或多个角色定义（说明用户或组应如何访问该项），再单击 **“确定”**。  
  
7.  重复上述步骤，为其他用户或组创建分配。  
  
## <a name="see-also"></a>另请参阅  
  (create-and-manage-role-assignments.md)    
 [新建角色分配：编辑角色分配页 &#40;报表管理器&#41;](../new-role-assignment-edit-role-assignment-page-report-manager.md)   
 ["安全属性" 页，项 &#40;报表管理器&#41;](../security-properties-page-items-report-manager.md)   
 [角色分配](role-assignments.md)   
 [角色定义](role-definitions.md)  
  
  
