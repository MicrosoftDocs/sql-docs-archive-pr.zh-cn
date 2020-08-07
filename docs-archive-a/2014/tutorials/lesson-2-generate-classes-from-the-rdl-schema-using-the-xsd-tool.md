---
title: 第2课：使用 xsd 工具从 RDL 架构生成类 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a81c87f1-7977-4b30-b6ac-b38b3e2b6398
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2c5db118ad8f94afc72cea44b9a2489f2b4fd7f4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690925"
---
# <a name="lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool"></a>第 2 课：使用 XSD 工具从 RDL 架构生成类
  创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目后，下一步是检索报表定义架构的本地副本和运行 XML 架构定义工具 (Xsd.exe)。  
  
### <a name="to-generate-the-rdl-classes"></a>生成 RDL 类  
  
1.  打开 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer (或等效 Web 浏览器的实例) 并导航到以下 URL：  
  
    ```  
    https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition/ReportDefinition.xsd  
    ```  
  
2.  在浏览器中打开 RDL 架构后，浏览到 "**文件**" 菜单，然后选择 "**另存为**"。  
  
3.  浏览到您创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 项目的位置，使用文件名 ReportDefinition.xsd 保存该架构。  
  
4.  保存文件后，打开 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 命令提示符的实例。 若要打开命令提示符的实例，请单击 "开始" 菜单，依次指向 "**所有程序**"、 **Microsoft Visual Studio 2010**"，然后依次指向" **Visual Studio Tools** "和" **Visual Studio 命令提示符 (2010) **"。  
  
5.  将当前路径更改为 ReportDefinition.xsd 文件的保存位置：  
  
     `CD\<ReportDefinition.xsd Path>`  
  
6.  用以下命令生成包含 RDL 架构的类的 ReportDefinition.cs 文件：  
  
     `xsd /c /n:SampleRDLSchema ReportDefinition.xsd`  
  
     若要生成 ReportDefinition.vb 文件，请使用以下命令：  
  
     `xsd /c /l:VB /n:SampleRDLSchema ReportDefinition.xsd`  
  
7.  向您的项目添加 ReportDefinition.xsd。 从 "**项目**" 菜单中，单击 "**添加现有项**"。 浏览到 Reportdefinition.xsd 文件的位置，选择 Reportdefinition.xsd，然后单击 "**添加**"。  
  
    > [!NOTE]  
    >  将 Reportdefinition.xsd 文件添加到项目后，你会注意到**解决方案资源管理器**ReportDefinition.cs ( .vb) 文件不在该项目中。 若要显示该文件，请单击 ReportDefinition.xsd 文件旁边的展开/折叠按钮。  
  
## <a name="next-lesson"></a>下一课  
 在下一课中，您将使用从 RDL 架构生成的类编写用于从报表服务器加载报表定义的代码。 请参阅[第3课：从报表服务器加载报表定义](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用从 RDL 架构生成的类更新报表 &#40;SSRS 教程&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
