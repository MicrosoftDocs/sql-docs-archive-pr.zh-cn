---
title: 授予数据库权限 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], full control
- full control permissions [Analysis Services]
ms.assetid: be7e5f64-af43-47d6-84a5-c5c1c277d644
author: minewiskan
ms.author: owend
ms.openlocfilehash: be8c10539e785517ff94153e7696e9d5f708a71b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87682412"
---
# <a name="grant-database-permissions-analysis-services"></a>授予数据库权限 (Analysis Services)
  如果你在介绍关系数据库中具有后台的 Analysis Services 数据库管理，则需要理解的首要事项为在数据访问方面，数据库不是 Analysis Services 中的主要安全对象。

 Analysis Services 中的主要查询结构为多维数据集（或表格模型），且这些特定对象设置了用户权限。 与相关的数据库引擎（数据库从此登录并且在此对数据库自身设置用户权限（通常是 `db_datareader`））比较，Analysis Services 数据库主要用作数据模型中的主要查询对象的容器。 如果你的近期目标是为多维数据集或表格模型启用数据访问，那么你现在可以不使用数据库权限，请直接进入此主题：[授予多维数据集或模型权限 (Analysis Services)](grant-cube-or-model-permissions-analysis-services.md)。

 Analysis Services 中的数据库权限启用了管理功能；如果你在委派处理操作，“完全控制”数据库权限的情况会同样如此或者风格会更为精细。 如以下插图和描述所示，在“创建角色” **** 对话框的“常规” **** 窗格上可指定 Analysis Services 数据库权限级别。

 Analysis Services 中没有登录名。 可以简单地在“成员身份” **** 窗格中创建角色并分配 Windows 帐户。 所有用户（包括管理员）使用 Windows 帐户连接到 Analysis Services。

 ![创建显示数据库权限的角色对话框](../media/ssas-permsdbrole.png "创建显示数据库权限的角色对话框")

 在数据库级别可指定三种类型的权限。

 “完全控制（管理员）”- 完全控制是一种包罗万象的权限，它通过 Analysis Services 数据库传达了广泛的功能，比如：在数据库内查询或处理任何对象的功能以及管理角色安全的功能。**** 完全控制与数据库管理员状态同义。 当选择 `Full Control` 时，`Process Database` 和 `Read Definition` 权限也被选择，并且不能被移除。

> [!NOTE]
>  服务器管理员（服务器管理员角色成员）对服务器上的每个数据库也具有隐式完全控制。

 `Process Database`─该权限用于在数据库级别委派处理。 作为管理员，你可通过创建一个角色来卸载此任务，该角色允许其他人员或服务对数据库中的任何对象调用处理操作。 或者，你也可以创建在特定对象上启用处理的角色。 有关详细信息，请参阅 [授予处理权限 (Analysis Services)](grant-process-permissions-analysis-services.md) 。

 `Read Definition`─该权限授予读取对象元数据的功能，但不能查看关联的数据。 一般地，该权限被用于为专用处理而创建的角色中，添加使用工具（例如： [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ）的功能来交互地处理数据库。 如果没有 `Read Definition`，则 `Process Database` 权限就仅在编写了脚本的方案中有效。 如果你计划或许通过 SSIS 或其他计划程序使处理自动化，你可能想在没有 `Process Database` 的情况下，创建带有 `Read Definition` 的角色。 否则，请考虑将这两个属性组合在同一角色中，以通过在用户界面中能形象化数据模型的 SQL Server 工具支持无人参与的以及交互式的处理。

## <a name="full-control-administrator-permissions"></a>完全控制（管理员）权限
 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，数据库管理员是被分配到包括完全控制（管理员）权限的角色的任何 Windows 用户标识。 数据库管理员可以在数据库中执行任何任务，其中包括：

-   处理对象

-   读取数据库中的所有对象的数据和元数据，其中包括多维数据集、维度、度量值组、透视和数据挖掘模型

-   通过添加用户或权限（包括添加用户到具有完全控制权限的角色）来创建或修改数据库角色

-   删除数据库角色或角色成员身份

-   为数据库注册程序集（或存储过程）。

 请注意，数据库管理员不能在服务器上添加或删除数据库，或是授予权限给相同服务器上的其它数据库。 该特权仅属于服务器管理员。 有关此权限级别的详细信息，请参阅[授予服务器管理员权限 &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 。

 由于所有角色都是用户定义的，我们建议你创建专用于此目的的角色（例如：名为“dbadmin”的角色），然后相应地分配 Windows 用户和组帐户。

#### <a name="create-roles-in-ssms"></a>在 SSMS 中创建角色

1.  在中 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，连接到实例 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，打开 "**数据库**" 文件夹，选择数据库，然后右键单击 "**角色**" "  |  **新建角色**"。

2.  在“常规” **** 窗格中，输入名称（例如：DBAdmin）。

3.  为多维数据集选择“完全控制(管理员)”复选框。**** 请注意，`Process Database` 和 `Read Definition` 被自动选择。 这些权限始终包含在包括了 `Full Control` 的角色中。

4.  在“成员身份” **** 窗格中，输入使用此角色连接到 Analysis Services 的 Windows 用户和组帐户。

5.  单击“确定” **** ，完成角色创建。

## <a name="process-database"></a>Process Database
 定义授予数据库权限的角色时，可以跳过 `Full Control` 并选择 "只是" `Process Database` 。 在数据库级别设置的该权限允许对数据库内的所有对象进行处理。 有关详细信息，请参阅 [授予处理权限 (Analysis Services)](grant-process-permissions-analysis-services.md)

## <a name="read-definition"></a>Read Definition
 与一样 `Process Database` ， `Read Definition` 在数据库级别设置权限会对数据库中的其他对象产生级联影响。 如果想在更为精细的级别上设置“读取定义”权限，则必须清除“常规”窗格中作为数据库属性的“读取定义”。 有关详细信息，请参阅[授予对象元数据的读取定义权限 (Analysis Services)](grant-read-definition-permissions-on-object-metadata-analysis-services.md)。

## <a name="see-also"></a>另请参阅
 [授予服务器管理员权限 &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) [授予过程权限 &#40;Analysis Services](grant-process-permissions-analysis-services.md)&#41;


