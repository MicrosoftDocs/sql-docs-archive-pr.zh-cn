---
title: 步骤 2：启用和配置包配置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a804efcd84ebe563a13f61443fe19096788ca809
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579630"
---
# <a name="step-2-enabling-and-configuring-package-configurations"></a>步骤 2：启用和配置包配置
  在此任务中，您将项目转换为包部署模型并使用包配置向导配置包。 您将使用该向导生成 XML 配置文件，该文件包含 Foreach 循环容器的 `Directory` 属性的配置设置。 Directory 属性的值由新的包级别变量在运行时提供，您可以更新该变量。 另外，将填充要在测试期间使用的新的示例数据文件夹。  
  
### <a name="to-create-a-new-package-level-variable-mapped-to-the-directory-property"></a>创建映射到 Directory 属性的新的包级别变量  
  
1.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击“控制流”**** 选项卡的背景。 这会将要创建的变量的作用域设置为包。  
  
2.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 菜单中，选择“变量”  。  
  
3.  在 **“变量”** 窗口中，单击 “添加变量” 图标。  
  
4.  在“名称”**** 框中，键入 **varFolderName**。  
  
    > [!IMPORTANT]  
    >  变量名称区分大小写。  
  
5.  验证 "**作用域**" 框是否显示包的名称，第5课。  
  
6.  将 `varFolderName` 变量的“数据类型”  框的值设置为“字符串”  。  
  
7.  返回到“控制流”  选项卡，然后双击“文件夹中的 Foreach 文件”  容器。  
  
8.  在 " **Foreach 循环编辑器**" 的 "**集合**" 页上，单击 "**表达式**"，然后单击省略号按钮 " ** ( ..." ) **。  
  
9. 在 "**属性表达式编辑器**" 中，单击**属性**列表，然后选择 `Directory` 。  
  
10. 在 "**表达式**" 框中，单击省略号按钮 " ** ( ..." ) **。  
  
11. 在“表达式生成器”**** 中，展开“变量”文件夹，然后将变量 **User::varFolderName** 拖到“表达式”**** 框中。  
  
12. 单击“确定”**** 退出“表达式生成器”****。  
  
13. 单击“确定”**** 退出“属性表达式编辑器”****。  
  
14. 单击“确定”**** 退出“Foreach 循环编辑器”****。  
  
### <a name="to-enable-package-configurations"></a>启用包配置  
  
1.  在 "**项目" 菜单**上，单击 "**转换为包部署模型**"。  
  
2.  出现警告提示时单击“确定”****，转换完成后，在“转换为包部署模型”**** 对话框中单击“确定”****。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击“控制流”**** 选项卡的背景。  
  
4.  在 **SSIS** 菜单上，单击 **“包配置”** 。  
  
5.  在“包配置组织程序”**** 对话框中，选择“启用包配置”****，然后单击“添加”****。  
  
6.  在包配置向导的欢迎页中，单击“下一步”****。  
  
7.  在“选择配置类型”  页上，确认“配置类型”  已设置为“XML 配置文件”  。  
  
8.  在“选择配置类型”**** 页上，单击“浏览”****。  
  
9. 默认情况下，“选择配置文件位置”**** 对话框将打开至项目文件夹。  
  
10. 在“选择配置文件位置”**** 对话框的“文件名”**** 中，键入 **SSISTutorial**，然后单击“保存”****。  
  
11. 在 "**选择配置类型**" 页上，单击 "**下一步"。**  
  
12. 在 "**选择要导出的属性**" 页上的 "**对象**" 窗格中，展开 "**变量**"，展开 " **varFolderName**"，展开 "**属性**"，然后选择 "**值**"。  
  
13. 在“选择要导出的属性”**** 页上，单击“下一步”****。  
  
14. 在“完成向导”**** 页上，键入该配置的配置名称，例如 **SSIS Tutorial Directory configuration**。 这是显示在“包配置组织程序”**** 对话框中的配置名称。  
  
15. 单击“完成”。  
  
16. 单击 **“关闭”** 。  
  
17. 向导将创建一个名为 Ssistutorial.dtsconfig. Datatransferconfig.dtsconfig 的配置文件，该配置文件包含变量的配置设置，后者 `value` 又设置了 `Directory` 枚举器的属性。  
  
    > [!NOTE]  
    >  配置文件通常包含有关包属性的复杂信息，但对于本教程，唯一的配置信息应当是  
    > <Configuration ConfiguredType="Property"  
    > Path = "\Package.Variables [User：： varFolderName]。Properties [值] "ValueType =" String "\>  
    >  \<ConfiguredValue>\</ConfiguredValue>  
    > \</Configuration>.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>创建并填充新的示例数据文件夹  
  
1.  在 Windows 资源管理器中，在驱动器的根级别 (例如，C： \\) ，请创建名为的新文件夹 `New Sample Data` 。  
  
2.  找到计算机上的示例文件并从文件夹复制其中的三个文件。  
  
3.  在该 `New Sample Data` 文件夹中，粘贴复制的文件。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 3：修改目录属性配置值](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
  
