---
title: 步骤 5：测试更新的包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a075af2e030c8257d01abf5eba7d330b1cc8efe7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586826"
---
# <a name="step-5-testing-the-updated-packages"></a>步骤 5：测试更新的包
  继续学习下一课（在该课中，您将创建用来在目标计算机上安装教程包的部署捆绑）之前，您应该测试包。 在此任务中，您将运行已添加到 Deployment Tutorial 项目中再用配置进行扩展的包 DataTransfer.dtsx 和 LoadXMLData。  
  
 当包运行时，随着它成功完成，包中的每个可执行文件都将变为绿色。 当所有可执行文件都为绿色时，包已成功完成。 还可以在“进度”  选项卡上查看包的执行进度。  
  
 如果包未成功运行，则您必须先修复它们，再继续学习下一课。  
  
### <a name="to-run-the-datatransfer-package"></a>运行 DataTransfer 包  
  
1.  在解决方案资源管理器中，单击 DataTransfer.dtsx。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”** 。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”** 。  
  
### <a name="to-run-the-loadxmldata-package"></a>运行 LoadXMLData 包  
  
1.  在解决方案资源管理器中，单击 LoadXMLData.dtsx。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”** 。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”** 。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：创建部署捆绑](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
![Integration Services 图标 (小型) ](media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
