---
title: " (基本数据挖掘教程) 创建数据源 |Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d8d5974c3685476f5d7a5751fb71bfa98384cf36
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580482"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>创建数据源（数据挖掘基础教程）
  *数据源*是在项目中保存和管理并部署到数据库的数据连接 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 除了其他所有必需的连接属性外，数据源还包含源数据所在的服务器和数据库的名称。  
  
> [!IMPORTANT]  
>  数据库的名称为 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。 如果尚未安装此数据库，请参阅[MICROSOFT SQL 示例数据库](https://go.microsoft.com/fwlink/?LinkId=88417)页。  
  
### <a name="to-create-a-data-source"></a>创建数据源  
  
1.  在**解决方案资源管理器**中，右键单击 "**数据源**" 文件夹，然后选择 "**新建数据源**"。  
  
2.  在“欢迎使用数据源向导”  页上，单击“下一步” 。  
  
3.  在 "**选择如何定义连接"** 页上，单击 "**新建**" 以添加到数据库的连接 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 。  
  
4.  在**连接管理器**的 "**提供程序**" 列表中，选择 "**本机 OLE DB\SQL Server native Client 11.0**"。  
  
5.  在 "**服务器名称**" 框中，键入或选择安装了的服务器的名称 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 。  
  
     例如，如果在本地服务器上承载该数据库，请键入**localhost** 。  
  
6.  在 "**登录到服务器**" 组中，选择 "**使用 Windows 身份验证**"。  
  
    > [!IMPORTANT]  
    >  实施者应尽可能使用 Windows 身份验证，因为它提供的身份验证方法比 SQL Server 身份验证更加安全。 而提供 SQL Server 身份验证只是为了向后兼容。 有关身份验证方法的详细信息，请参阅[数据库引擎配置-帐户设置](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md)。  
  
7.  在 "**选择或输入数据库名称**" 列表中，选择， [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 然后单击 **"确定"**。  
  
8.  单击“下一步”。  
  
9. 在 "**模拟信息**" 页上，单击 "**使用服务帐户**"，然后单击 "**下一步**"。  
  
     在 "**完成向导**" 页上，请注意，默认情况下，数据源名为 "艾德作品 DW 2012"。  
  
10. 单击“完成”。  
  
     新数据源（艾德公司 DW 2012）出现在解决方案资源管理器的 "**数据源**" 文件夹中。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [创建数据源视图 &#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>课程中的前一个任务  
 [&#40;数据挖掘基础教程创建 Analysis Services 项目&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 多维&#41;创建数据源](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [定义数据源](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [设置模拟选项（SSAS - 多维）](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
