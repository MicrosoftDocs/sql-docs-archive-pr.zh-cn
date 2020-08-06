---
title: 使用 SSMS (SSAS 表格) 管理角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4ee34d5e75d5d4ce3679d46d29af3215852d2bbe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87683112"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>使用 SSMS 管理角色（SSAS 表格）
  对于部署的表格模型，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建、编辑和管理角色。  
  
 本主题中的任务：  
  
-   [创建新角色](#bkmk_new_role)  
  
-   [复制角色](#bkmk_copy_role)  
  
-   [编辑角色](#bkmk_edit_role)  
  
-   [删除角色](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中通过角色管理器使用已定义的角色重新部署表格模型项目，将覆盖已部署的表格模型中定义的角色。  
  
> [!CAUTION]  
>  如果在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开模型项目时使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 来管理表格模型工作区数据库，可能会导致 Model.bim 文件损坏。 在创建和管理表格模型工作区数据库的角色时，请使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的角色管理器。  
  
###  <a name="to-create-a-new-role"></a><a name="bkmk_new_role"></a>创建新角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开要为其创建新角色的表格模型数据库，右键单击 **“角色”**，然后单击 **“新建角色”**。  
  
2.  在 **“创建角色”** 对话框的“选择页”窗口中，单击 **“常规”**。  
  
3.  在常规设置窗口的 **“名称”** 字段中，键入角色的名称。  
  
     默认情况下，对于每个新建角色，默认角色的名称将为递增式编号。 建议您键入明确标识成员类型的名称，例如财务经理或人力资源专员。  
  
4.  在 **“为此角色设置数据库权限”** 中，选择以下权限选项之一：  
  
    |权限|说明|  
    |----------------|-----------------|  
    |**完全控制（管理员）**|成员可以对模型架构进行修改并可以查看所有数据。|  
    |**处理数据库**|成员可以运行“处理”和“全部处理”操作。 不能修改模型架构且不能查看数据。|  
    |**读取**|允许成员查看数据（基于行筛选器），但不能对模型架构进行任何更改。|  
  
5.  在 **“创建角色”** 对话框的“选择页”窗口中，单击 **“成员身份”**。  
  
6.  在“成员身份设置”窗口中单击 **“添加”**，然后在 **“选择用户或组”** 对话框中，添加要作为成员添加的 Windows 用户或组。  
  
7.  如果您创建的角色已具有“读取”权限，则可以使用 DAX 公式为任意表添加行筛选器。 若要添加行筛选器，请在 "**角色属性- \<rolename> ** " 对话框的 "**选择页**" 中，单击 "**行筛选器**"。  
  
8.  在 "行筛选器" 窗口中，选择一个表，然后单击 " **Dax 筛选器**" 字段，然后在 " ** \<tablename> dax 筛选器**" 字段中键入 dax 公式。  
  
    > [!NOTE]  
    >  DAX 筛选器 \<tablename> 字段不包含自动完成查询编辑器或插入函数功能。 若要在写入 DAX 公式时使用自动完成功能，必须在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 DAX 公式编辑器。  
  
9. 单击 **“确定”** 保存角色。  
  
###  <a name="to-copy-a-role"></a><a name="bkmk_copy_role"></a>复制角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要复制的角色的表格模型数据库，展开 **“角色”**，右键单击该角色，然后单击 **“复制”**。  
  
###  <a name="to-edit-a-role"></a><a name="bkmk_edit_role"></a>编辑角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要编辑的角色的表格模型数据库，展开 **“角色”**，右键单击该角色，然后单击 **“属性”**。  
  
     在 "**角色属性**" \<rolename> 对话框中，您可以更改权限、添加或删除成员，以及添加/编辑行筛选器。  
  
###  <a name="to-delete-a-role"></a><a name="bkmk_deletet_role"></a>删除角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要删除的角色的表格模型数据库，展开 **“角色”**，右键单击该角色，然后单击 **“删除”**。  
  
## <a name="see-also"></a>另请参阅  
 [角色（SSAS 表格）](roles-ssas-tabular.md)  
  
  
