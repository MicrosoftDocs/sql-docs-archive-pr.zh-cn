---
title: 定义维度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 112696db-3838-4b50-91bd-d2ce5fa04ee5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2eb7a695ffc2c0588396a4a9ea655983c26cc719
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577026"
---
# <a name="defining-a-dimension"></a>定义维度
  在以下任务中，将使用维度向导生成“日期”维度。  
  
> [!NOTE]  
>  本课要求您已完成课程 1 中的所有课程。  
  
### <a name="to-define-a-dimension"></a>定义维度  
  
1.  在解决方案资源管理器中（在 Microsoft Visual Studio 的右侧），右键单击“维度”**** 文件夹，然后单击“新建维度”****。 将显示维度向导。  
  
2.  在“欢迎使用维度向导”**** 页上，单击“下一步”****。  
  
3.  在“选择创建方法”**** 页上，确保选中“使用现有表”**** 选项，然后单击“下一步”****。  
  
4.  在“指定源信息”**** 页上，确保选中“Adventure Works DW 2012”**** 数据源视图。  
  
5.  在“主表”**** 列表中，选择“日期”****。  
  
6.  单击“下一步”。  
  
7.  在“选择维度属性”**** 页上，选中下列属性旁的复选框：  
  
    -   **日期键**  
  
    -   **完整日期备用键**  
  
    -   **英文月份名称**  
  
    -   **日历季度**  
  
    -   **日历年**  
  
    -   **Calendar Semester**  
  
8.  将“完整日期备用键”**** 属性的“属性类型”**** 列的设置从“常规”**** 更改为“日期”****。 为此，请单击“属性类型”**** 列中的“常规”****。 然后单击箭头展开选项。 接下来，单击 "**日期**  >  **日历**  >  **日期**"。 单击“确定”。 重复这些步骤，更改属性的属性类型，具体如下所示：  
  
    -   “英文月份名称”**** 更改为“月份”****  
  
    -   “日历季度”**** 更改为“季度”****  
  
    -   “日历年”**** 更改为“年”****  
  
    -   “日历半期”**** 更改为“半年”****  
  
9. 单击“下一步”。  
  
10. 在“完成向导”**** 页的“预览”窗格中，可以看到“日期”**** 维度及其属性。  
  
11. 单击 **“完成”** 以完成向导。  
  
     在解决方案资源管理器的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 项目中，“日期”维度将在“维度”**** 文件夹中显示。 在开发环境的中央，维度设计器显示“日期”维度。  
  
12. 在“文件”菜单上，单击“全部保存”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [定义多维数据集](lesson-2-2-defining-a-cube.md)  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)   
 [使用现有表创建维度](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [使用维度向导创建维度](multidimensional-models/create-a-dimension-using-the-dimension-wizard.md)  
  
  
