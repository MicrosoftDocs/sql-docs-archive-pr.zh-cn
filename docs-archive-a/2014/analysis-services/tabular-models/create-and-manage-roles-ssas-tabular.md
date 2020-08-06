---
title: " (SSAS 表格) 创建和管理角色 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.rolemanager.f1
- sql12.asvs.bidtoolset.roledb.f1
ms.assetid: e23d27a8-e968-4082-9dbe-963fc724b5d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 335e0e311d97ea452449cd0c5d6550f6dbcca4f4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578489"
---
# <a name="create-and-manage-roles-ssas-tabular"></a>创建和管理角色（SSAS 表格）
  在表格模型中，角色定义模型的成员权限。 可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“角色管理器”对话框为模型项目定义角色。 在部署模型时，数据库管理员可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]管理角色。  
  
 本主题中的任务说明如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“角色管理器”对话框在模型创作期间创建和管理角色。 有关在部署的模型数据库中管理角色的信息，请参阅[表格模型角色（SSAS 表格）](roles-ssas-tabular.md)。  
  
## <a name="tasks"></a>任务  
 若要创建、编辑、复制和删除角色，可使用 **“角色管理器”** 对话框。 若要查看 **“角色管理器”** 对话框，请在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“角色管理器”**。  
  
###  <a name="to-create-a-new-role"></a><a name="bkmk_new_role"></a>创建新角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“角色管理器”**。  
  
2.  在 **“角色管理器”** 对话框中，单击 **“新建”**。  
  
     一个新的突出显示的角色会添加到“角色”列表中。  
  
3.  在 **“角色”** 列表的 **“名称”** 字段中，键入角色的名称。  
  
     默认情况下，对于每个新建角色，默认角色的名称将为递增式编号。 建议您键入明确标识成员类型的名称，例如财务经理或人力资源专员。  
  
4.  在 **“权限”** 字段中，单击向下箭头，然后选择以下权限类型之一：  
  
    |权限|说明|  
    |----------------|-----------------|  
    |**无**|成员无法对模型架构进行任何修改，也无法查询数据。|  
    |**读取**|允许成员查询数据（基于行筛选器），但不能对模型架构进行任何更改。|  
    |**读取和处理**|允许成员查询数据（基于行级别筛选器）并运行“处理”和“全部处理”操作，但无法对模型架构进行任何更改。|  
    |**处理**|成员可以运行“处理”和“全部处理”操作。 无法修改模型架构，也无法查询数据。|  
    |**管理员**|成员可以对模型架构进行修改并可以查询所有数据。|  
  
5.  若要输入角色的说明，请单击 **“说明”** 字段，然后键入说明。  
  
6.  如果您创建的角色已具有“读取”或者“读取和处理”权限，则您可以使用 DAX 公式添加行筛选器。 若要添加行筛选器，请单击 **“行筛选器”** 选项卡，选择某个表，然后单击 **“DAX 筛选器”** 字段，再键入 DAX 公式。  
  
7.  若要向角色添加成员，请单击 **“成员”** 选项卡，然后单击 **“添加”**。  
  
    > [!NOTE]  
    >  也可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]将角色成员添加到已部署的模型中。 有关详细信息，请参阅[使用 SSMS 管理角色（SSAS 表格）](manage-roles-by-using-ssms-ssas-tabular.md)。  
  
8.  在 **“选择用户或组”** 对话框中，将 Windows 用户或 Windows 组对象作为成员输入。  
  
9. 单击“确定” 。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的角色](roles-ssas-tabular.md)   
 [SSAS 表格&#41;&#40;透视](perspectives-ssas-tabular.md)   
 [在 Excel 中分析 &#40;SSAS 表格&#41;](analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函数 &#40;DAX&#41;](/dax/username-function-dax)   
 [&#40;DAX&#41;的 CUSTOMDATA 函数](/dax/customdata-function-dax)  
  
  
