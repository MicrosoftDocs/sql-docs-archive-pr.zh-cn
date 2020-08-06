---
title: 使用从 RDL 架构生成的类更新报表 (SSRS 教程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f3972b8e1af6d50ccc6f5188c8f671fe333ebce8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578557"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>使用从 RDL 架构生成的类更新报表（SSRS 教程）
  本教程演示了如何使用 XML 架构定义工具 ( # A0) 来生成类，这些类可用于将报表定义文件 ( .rdl 和 .rdlc) 与类进行序列化和反序列化 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer> 。  
  
## <a name="what-you-will-learn"></a>学习内容  
 在本教程的课程中，您将完成下列活动：  
  
-   使用 " [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 控制台应用程序" 项目模板创建应用程序。  
  
-   使用**xsd**工具从报表定义语言 (RDL) 架构生成类。  
  
-   连接到报表服务器并检索报表定义。  
  
-   编写用于更新报表定义文件的代码。  
  
-   将更新的报表定义保存回报表服务器。  
  
-   运行 RDL 架构应用程序 (VB/C#)。  
  
> [!NOTE]  
>  对于没有说明的报表，在本教程中提供的代码示例可能会失败。 失败的原因在于：说明属性对于未指定说明的报表不存在。  
  
## <a name="requirements"></a>要求  
 若要完成本教程，您必须满足下列要求：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)].  
  
-   拥有足够的权限，能够访问报表服务器所在计算机中的报表服务器 Web 服务并向该服务发布报表。  
  
-   已将 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 示例数据库安装到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的实例中。  
  
-   报表服务器上已安装了报表。 本教程使用示例报表 Company Sales 2012。 有关示例报表的详细信息，请参阅[SQL Server Reporting Services 产品示例](https://go.microsoft.com/fwlink/?LinkId=177889)。  
  
> [!NOTE]  
>  安装过程中不会自动安装示例，但是您可以随时安装这些示例。 有关示例的信息，请参阅[SQL Server 产品示例](https://go.microsoft.com/fwlink/?LinkId=182887)。  
  
 **完成本教程的估计时间：** 30 分钟  
  
## <a name="tasks"></a>任务  
 [第 1 课：创建 RDL 架构 Visual Studio 项目](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [第 2 课：使用 XSD 工具从 RDL 架构生成类](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [第 3 课：从报表服务器加载报表定义](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [第 4 课：以编程方式更新报表定义](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [第 5 课：将报表定义发布到报表服务器](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [第6课：运行 RDL 架构应用程序 &#40;VB-C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>另请参阅  
 [报表定义语言 (SSRS)](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
