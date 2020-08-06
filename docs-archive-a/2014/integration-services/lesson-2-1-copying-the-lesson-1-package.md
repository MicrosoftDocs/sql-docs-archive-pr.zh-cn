---
title: 步骤 1：复制第 1 课包 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f1616c2-2b4e-4010-be50-27d7b897403a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 43e117d82983bdaca8959fe7af8940d248ded97b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586808"
---
# <a name="step-1-copying-the-lesson-1-package"></a>步骤 1：复制 Lesson 1 包
  在本任务中，将为第 1 课中创建的 Lesson 1.dtsx 包创建一个副本。 如果未完成第 1 课的学习，则可以向项目添加本教程中附带的已完成 Lesson 1 包，然后再对其进行复制。 将使用这一新副本来完成第 2 课剩余部分。  
  
### <a name="to-create-the-lesson-2-package"></a>创建 Lesson 2 包  
  
1.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 尚未打开，请单击“开始”****，依次指向“所有程序”**** 和“Microsoft SQL Server 2012”****，然后单击“SQL Server Data Tools”****。  
  
2.  在“文件”**** 菜单中，依次单击“打开”****、“项目/解决方案”****、“SSIS Tutorial”**** 文件夹，然后再次单击“打开”****，最后双击“SSIS Tutorial.sln”****。  
  
3.  在解决方案资源管理器中，右键单击“Lesson 1.dtsx”****，然后单击“复制”****。  
  
4.  在解决方案资源管理器中，右键单击 " **SSIS 包**"，然后单击 "**粘贴**"。  
  
     默认情况下，复制的包将命名为 Lesson 2.dtsx。  
  
5.  在解决方案资源管理器中，双击 " **.dtsx** " 以打开包  
  
6.  右键单击“控制流”**** 设计图面背景的任意位置，再单击“属性”****。  
  
7.  在属性窗口中，将 `Name` 属性更新为 `Lesson 2` 。  
  
8.  依次单击“ID”**** 属性框和下拉箭头，然后单击“\<Generate New ID>”****。  
  
### <a name="to-add-the-completed-lesson-1-package"></a>添加已完成的 Lesson 1 包  
  
1.  依次打开 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 和 SSIS Tutorial 项目。  
  
2.  在解决方案资源管理器中，右键单击 " **SSIS 包**"，然后单击 "**添加现有包**"。  
  
3.  在“添加现有包的副本”  对话框的“包位置”  中，选择“文件系统”  。  
  
4.  单击“浏览(…)”按钮，导航到计算机上的“Lesson 1.dtsx”，然后单击“打开”************。  
  
     要下载此教程的所有课程包，请执行以下操作：  
  
    1.  导航到 [Integration Services 产品示例](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  单击 "**下载**" 选项卡。  
  
    3.  单击 SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip 文件。  
  
5.  按先前过程中的步骤 3-8 中所述，复制并粘贴 Lesson 1 包。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 2：添加和配置 Foreach 循环容器](lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
  
