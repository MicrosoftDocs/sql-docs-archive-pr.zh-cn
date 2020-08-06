---
title: 授予对数据挖掘结构和模型的权限 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0db849551bdb38615f280b123c98f0e9d3053d6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690828"
---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>授予数据挖掘结构和模型的权限 (Analysis Services)
  在默认情况下，仅 Analysis Services 服务器管理员有权限查看数据库中的数据挖掘结构或挖掘模型。 请遵循以下说明，以向非管理员用户授予权限。  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>设置访问挖掘结构的权限  
  
1.  在 SSMS 中，连接到 Analysis Services。 如果需要此步骤的帮助，请参阅[从客户端应用程序进行连接 (Analysis Services)](../instances/connect-from-client-applications-analysis-services.md)。  
  
2.  打开“数据库” **** 文件夹，并在对象资源管理器中选择一个数据库。  
  
3.  右键单击“角色”，然后选择“新角色”。********  
  
4.  在“常规页”中输入名称，并且（可选）输入描述。 此页面也包含多个数据库权限，如完全控制、处理数据库和读取定义。 数据挖掘访问不需要这些权限。 有关数据库权限的详细信息，请参阅[授予数据库权限 (Analysis Services)](grant-database-permissions-analysis-services.md)。  
  
5.  在“挖掘结构”**** 窗格中，为每个数据挖掘结构选择“读取”或“读/写”********。  
  
6.  在“成员身份” **** 窗格中，输入使用此角色连接到 Analysis Services 的 Windows 用户和组帐户。  
  
7.  单击“确定” **** ，完成角色创建。  
  
## <a name="set-permissions-to-access-a-mining-model"></a>设置访问挖掘模型的权限  
 对于数据挖掘模型，角色可具有“读取”或“读/写”权限，以及允许查看和浏览基础数据的“钻取”和“读取定义”权限****************。  
  
 **注意** 如果对挖掘结构和挖掘模型都启用了钻取，作为拥有挖掘模型和挖掘结构钻取权限的角色成员的任何用户也可以查看挖掘结构中的列，即使那些列并未包括在挖掘模型中。 因此，若要保护敏感信息，应设置数据源视图来屏蔽个人信息，并且仅在需要时才允许对挖掘结构进行钻取访问。  
  
 若要向数据库角色授予读取或读/写权限，用户必须为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器角色的成员或为拥有完全控制（管理员）权限的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库角色的成员。  
  
1.  在中 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，连接到实例 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，在对象资源管理器中展开相应数据库的 "**角色**"，然后单击 "数据库角色" (或 "创建新的数据库角色) "。  
  
2.  在“挖掘结构”窗格中的“挖掘模型”列表中找到“挖掘模型”，然后为此挖掘模型选择“读取”、“读/写”、“钻取”或“浏览”************************。  
  
3.  在“成员身份” **** 窗格中，输入使用此角色连接到 Analysis Services 的 Windows 用户和组帐户。  
  
4.  单击“确定” **** ，完成角色创建。  
  
 若要在使用数据挖掘扩展插件 (DMX) OPENQUERY 子句的钻取查询中使用数据源，则数据库角色还需要具有读/写相应的数据源对象的权限。 有关详细信息，请参阅[授予数据源对象的权限 (Analysis Services)](grant-permissions-on-a-data-source-object-analysis-services.md) 和 [OPENQUERY (DMX)](/sql/dmx/source-data-query-openquery)。  
  
> [!NOTE]  
>  默认情况下，将禁用使用 OPENROWSET 提交 DMX 查询。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Analysis Services 授予服务器管理员权限&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [&#40;Analysis Services 授予多维数据集或模型权限&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [授予对维度数据的自定义访问 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [授予单元数据的自定义访问权限 (Analysis Services)](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
