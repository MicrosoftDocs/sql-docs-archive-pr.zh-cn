---
title: 步骤 1：生成部署实用工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3d32dcbf4bfcf9758dfe58803b75094d1807aa90
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586811"
---
# <a name="step-1-building-the-deployment-utility"></a>步骤 1：生成部署实用工具
  在此任务中，将为 Deployment Tutorial 项目配置和生成部署实用工具。  
  
 必须先修改 Deployment Tutorial 项目的属性，才能生成部署实用工具。 使用“Deployment Tutorial 属性页”对话框配置这些属性。  在此对话框中，您必须允许在部署期间更新配置，并指定生成进程将生成部署实用工具。 在设置属性后，将生成项目。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供了一组窗口，可以使用它们来调试包。 您可以查看错误、警告和信息性消息，在运行时跟踪包的状态，或查看生成进程的进度和结果。 在本课中，将使用“输出”窗口查看生成部署实用工具的进度和结果。  
  
### <a name="to-set-the-deployment-utility-properties"></a>设置部署实用工具的属性  
  
1.  如果 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 尚未打开，请单击“开始”，依次指向“所有程序”和“Microsoft SQL Server”，再单击“Business Intelligence Development Studio”。      
  
2.  在“文件”  菜单上，依次单击“打开”  、“项目/解决方案”  、“Deployment Tutorial”  文件夹，然后再次单击“打开”  ，最后双击“Deployment Tutorial.sln”  。  
  
3.  在解决方案资源管理器中，右键单击“Deployment Tutorial”，再单击“属性”。   
  
4.  在“Deployment Tutorial 属性页”  对话框中，展开“配置属性”，再单击“部署实用工具”。  
  
5.  在 "**部署教程属性页**" 对话框的右窗格中，验证 `AllowConfigurationChanges` 是否将设置为 `true` ，将设置 `CreateDeploymentUtility` 为 `true` ，并选择性地更新的默认值 `DeploymentOutputPath` 。  
  
6.  单击“确定”。   
  
### <a name="to-build-the-deployment-utility"></a>生成部署实用工具  
  
1.  在解决方案资源管理器中，单击“Deployment Tutorial”  。  
  
2.  在“视图”  菜单上，单击“输出”  。 默认情况下，“输出”窗口位于 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的左下角。  
  
3.  在“生成”  菜单上，单击“生成 Deployment Tutorial”  。  
  
4.  在“输出”窗口中，验证以下信息：  
  
     已启动生成: SQL Integration Services 项目: 增量 ...  
  
     正在创建部署实用工具...  
  
     已创建部署实用工具。  
  
     生成完成 -- 0 个错误，0 个警告  
  
     ========== 生成: 0 已成功，0 已失败，1 最新，0 已跳过 ==========  
  
5.  在 **“文件”** 菜单中，单击 **“退出”** 。 如果提示保存对 Deployment Tutorial 的各项所做的更改，请单击“是”  。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 2：验证部署捆绑](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
![Integration Services 图标 (小型) ](media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
## <a name="see-also"></a>另请参阅  
 [创建部署实用工具](../../2014/integration-services/create-a-deployment-utility.md)  
  
  
