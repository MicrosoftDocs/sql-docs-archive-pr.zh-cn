---
title: 第 1 课：创建报表服务器项目 (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a708e5114344e87edd620ef58bc50594a9b9ef8d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694295"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>第 1 课：创建报表服务器项目 (Reporting Services)
  若要在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中创建报表，必须先创建报表服务器项目以用于保存报表定义 (.rdl) 文件和报表所需的其他所有资源文件。 然后，您将创建实际的报表定义文件、定义报表的数据源、定义数据集并定义报表布局。 运行报表时，将检索实际数据并将其与布局相结合，然后呈现在屏幕上，以便执行导出、打印或保存操作。  
  
 在本课中，您将学习如何在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中创建报表服务器项目。 报表服务器项目用于创建在报表服务器中运行的报表。  
  
### <a name="to-create-a-report-server-project"></a>创建报表服务器项目  
  
1.  单击 "**开始**"，指向 "**所有程序**"，指向 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] ""，然后单击 " **SQL Server Data Tools**"。 如果这是你首次打开 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ，请单击 "默认环境设置" 的 "**商业智能设置**"。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。  
  
3.  在“已安装的模板”**** 列表中，单击“商业智能”****。  
  
4.  单击 "**报表服务器项目**"。  
  
5.  在 "**名称**" 中键入 "**教程**"。  
  
6.  单击“确定”以创建该项目  。  
  
     解决方案资源管理器中将显示 Tutorial 项目。  
  
### <a name="to-create-a-new-report-definition-file"></a>创建新的报表定义文件  
  
1.  在解决方案资源管理器中，右键单击 "**报表**"，指向 "**添加**"，然后单击 "**新建项**"。  
  
    > [!NOTE]  
    >  如果“解决方案资源管理器”**** 窗口不可见，请单击“视图”**** 菜单中的“解决方案资源管理器”****。  
  
2.  在 "**添加新项**" 对话框中的 "**模板**" 下，单击 "**报表**"。  
  
3.  在“名称” **** 中，键入 **Sales Orders.rdl** ，再单击“添加” ****。  
  
     此时报表设计器将打开，并在“设计”视图中显示新的 .rdl 文件。  
  
 报表设计器是在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中运行的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]组件。 它包含两个视图：“设计” **** 和“预览” ****。 单击各个选项卡可更改视图。  
  
 在“报表数据” **** 窗格中定义数据。 在“设计” **** 视图中定义报表布局。 可以在“预览” **** 视图中运行报表并查看其外观。  
  
## <a name="next-task"></a>下一个任务  
 您已经成功创建了名为“Tutorial”的报表项目，并向该报表项目添加了报表定义 (.rdl) 文件。 接下来，您将指定要用于报表的数据源。 请参阅[第 2 课：指定连接信息 (Reporting Services)](lesson-2-specifying-connection-information-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建基本表报表（SSRS 教程）](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
