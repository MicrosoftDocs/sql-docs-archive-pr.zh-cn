---
title: 步骤 2：添加并配置日志记录 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0f2cdce6f34a19e22830d357d20f5d99cff8c14f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689515"
---
# <a name="step-2-adding-and-configuring-logging"></a>步骤 2：添加并配置日志记录
  在本任务中，将为 Lesson 3.dtsx 包中的数据流启用日志记录。 然后，将配置一个文本文件日志提供程序，以记录 PipelineExecutionPlan 和 PipelineExecuteTrees 事件。 该文本文件日志提供程序可以创建便于查看并可轻松传输的日志。 由于便于使用，因此，这些日志文件在包的基本测试阶段非常有用。 您也可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的“日志事件”窗口中查看日志条目。  
  
### <a name="to-add-logging-to-the-package"></a>向包中添加日志记录  
  
1.  在 **SSIS** 菜单上，单击 **“日志记录”** 。  
  
2.  在“配置 SSIS 日志”**** 对话框的“容器”**** 窗格中，确保选中了最前面的代表第 3 课包的对象。  
  
3.  在“提供程序和日志”**** 选项卡的“提供程序类型”**** 框中，选择“用于文本文件的 SSIS 日志提供程序”****，然后单击“添加”****。  
  
     Integration Services 将新的文本文件日志提供程序添加到具有默认名称的**文本文件的 SSIS 日志提供**程序的包中。 现在便可对新的日志提供程序进行配置。  
  
4.  在 "**名称**" 列中，键入 `Lesson 3 Log File` 。  
  
5.  也可以修改“说明”  。  
  
6.  在“配置”**** 列中，单击 **\<New Connection>**，以指定用于写入日志信息的目标位置。  
  
     在“文件连接管理器编辑器”**** 对话框中，对“使用类型”**** 选择“创建文件”****，然后单击“浏览”****。 默认情况下，“选择文件”**** 对话框将打开项目文件夹，但你可以将日志信息保存到任何位置。  
  
7.  在 "**选择文件**" 对话框的 "文件名 **" 框中**，键入 `TutorialLog.log` ，并单击 "**打开**"。  
  
8.  单击“确定”**** 关闭“文件连接管理器编辑器”**** 对话框。  
  
9. 在“容器”  窗格中，展开包容器层次结构中的所有节点，然后清除包括 **Extract Sample Currency Data** 复选框在内的所有复选框。 现在选中“Extract Sample Currency Data”  复选框以仅获取有关此节点的事件。  
  
    > [!IMPORTANT]  
    >  如果“Extract Sample Currency Data”**** 复选框显示为灰色而并非选中状态，则该任务将使用父容器的日志设置，无法启用任务特定的日志事件。  
  
10. 在“详细信息”  选项卡的“事件”  列中，选择“PipelineExecutionPlan”  和“PipelineExecutionTrees”  事件。  
  
11. 单击“高级”**** 可查看日志提供程序将为每个事件写入日志的详细信息。 默认情况下，将为您指定的事件自动选择所有信息类别。  
  
12. 单击“基本”**** 隐藏信息类别。  
  
13. 在 "**提供程序和日志**" 选项卡上的 "**名称**" 列中，选择 `Lesson 3 Log File` 。 为包创建日志提供程序后，可以选择取消选择它以临时关闭日志记录，而不必删除后再重新创建日志提供程序。  
  
14. 单击“确定”  。  
  
## <a name="next-steps"></a>后续步骤  
 [步骤 3：测试第 3 课教程包](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
