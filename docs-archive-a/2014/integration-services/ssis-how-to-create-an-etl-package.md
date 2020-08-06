---
title: SSIS 教程：创建简单的 ETL 包 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 780b008052a2ff64aa75b2036aa7202128f95ae2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690733"
---
# <a name="ssis-tutorial-creating-a-simple-etl-package"></a>SSIS 教程：创建简单的 ETL 包
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 是一种用于构建高性能数据集成解决方案的平台，其中包括数据仓库的 ETL) 包的提取、转换和加载 (。 SSIS 包括生成并调试包的图形工具和向导；执行如 FTP 操作、执行 SQL 语句和发送电子邮件等工作流功能的任务；用于提取和加载数据的数据源和目标；用于清理、聚合、合并和复制数据的转换；管理服务，即用于管理包执行和存储的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务；以及用于对 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 对象模型编程的应用程序编程接口 (API)。  
  
 在本教程中，您将学习如何使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建一个简单的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包。 所创建的包将从平面文件提取数据，重新设置数据的格式，然后将已重新设置格式的数据插入到事实数据表中。 在下列课程中，将扩展包以阐释循环、包配置、日志记录和错误流。  
  
 在安装教程所用的示例数据的同时，也会安装将在教程的每一课中创建的完整的包版本。 使用完整的包，您可以按需要跳过前面几课而从后面的课程开始学习教程。 如果您是第一次使用包或新的开发环境，我们建议从第 1 课开始学习。  
  
## <a name="what-you-will-learn"></a>学习内容  
 熟悉中提供的新工具、控件和功能的最佳方式 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是使用它们。 本教程将引导您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器创建一个简单的 ETL 包，其中包含循环、配置、错误流逻辑和日志记录。  
  
## <a name="requirements"></a>要求  
 本教程适用于熟悉基本数据库操作，但对中可用的新功能有限制的用户 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
 若要使用本教程，系统中必须安装下列组件：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的 **数据库的** 。 为了增强安全性，默认情况下不会安装示例数据库。 要下载 **AdventureWorksDW2012** 数据库，请参阅 [Adventure Works for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=275026)。  
  
    > [!IMPORTANT]  
    >  附加数据库 (\*.mdf file) 时，默认情况下 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 将搜索 .ldf 文件。 在 **“附加数据库”** 对话框中单击“确定”前，您必须手动删除 .ldf 文件。  
    >   
    >  有关附加数据库的详细信息，请参阅 [Attach a Database](../relational-databases/databases/attach-a-database.md)。  
  
-   示例数据。 示例数据与 [!INCLUDE[ssIS](../includes/ssis-md.md)] 课程包一起提供。 要下载示例数据和课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 "**下载**" 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
 [第 1 课：创建项目和基本包](lesson-1-create-a-project-and-basic-package-with-ssis.md)  
 在本课中，将创建一个简单的 ETL 包，从单个平面文件中提取数据，再使用查找转换转换数据，最后将所得结果加载到目标事实数据表中。  
  
 [第 2 课：添加循环](lesson-2-adding-looping-with-ssis.md)  
 在本课中，将扩展第 1 课中创建的包，利用新增的循环功能，将多个平面文件提取到单个数据流进程中。  
  
 [第 3 课：添加日志记录](lesson-3-add-logging-with-ssis.md)  
 在本课中，将扩展第 2 课中创建的包，利用新增的日志记录功能。  
  
 [第 4 课：添加错误流重定向](lesson-4-add-error-flow-redirection-with-ssis.md)  
 在本课中，将扩展第 3 课中创建的包，以便利用新增的错误输出配置。  
  
 [第 5 课：添加包部署模型的包配置](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
 在本课中，将扩展第 4 课中创建的包，利用新增的包配置选项。  
  
 [第 6 课：对项目部署模型使用参数](lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
 在本课中，将扩展第 5 课中创建的包，以将新参数用于项目部署模型。  
  
  
