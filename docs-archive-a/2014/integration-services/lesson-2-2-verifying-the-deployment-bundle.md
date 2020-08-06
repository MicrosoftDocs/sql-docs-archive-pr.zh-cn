---
title: 步骤 2：验证部署捆绑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f452a87154175ac05a050761d8f12b6bfe61cd8b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578309"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>步骤 2：验证部署捆绑
  在第 1 课中，创建了 Deployment Tutorial 项目，并向该项目添加了包和辅助文件；在上一任务中，您为项目生成了部署实用工具。  
  
 在此任务中，您将验证部署捆绑的内容。 部署捆绑是将复制到目标计算机并用来安装包的文件夹。 如果将默认值 bin\Deployment 用作部署实用工具的位置，则在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中部署捆绑是 Deployment Tutorial 文件夹中的 Bin\Deployment 文件夹。  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>验证部署捆绑的内容  
  
1.  找到计算机上的 bin\Deployment 文件夹。  
  
2.  验证是否存在下列文件：  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  右键单击“Deployment Tutorial.SSISDeploymentManifest”，指向“打开方式”  ，再单击“Internet Explorer”  。 也可以在文本编辑器（如记事本）中打开该文件。 文件的 XML 代码应该如下所示：  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  验证特性的值是否为 `AllowConfigurationChanges` **true** ，并且 XML 是否包含两个 `Package` 包中的每个包的元素、 `MiscellaneousFile` 四个非包文件中每个文件的元素以及 `ConfigurationFile` 两个 XML 配置文件中每个文件的元素。  
  
5.  退出 Internet Explorer 或文本编辑器。  
  
## <a name="next-lesson"></a>下一课  
 [第 3 课：安装包](../integration-services/lesson-3-install-ssis-package.md)  
  
![Integration Services 图标 (小型) ](media/dts-16.gif "集成服务图标（小）")  **随时保持最新 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
