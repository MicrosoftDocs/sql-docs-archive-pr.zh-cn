---
title: 步骤 5：添加并配置平面文件源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 504cfb4bc722627eb8ee70ec1f2c562cef8f1f0f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586827"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>步骤 5：添加并配置平面文件源
  在此任务中，将向包中添加一个平面文件源并对其进行配置。 平面文件源是一个数据流组件，它使用平面文件连接管理器定义的元数据来指定转换过程要从此平面文件中提取的数据的格式和结构。 可以通过使用平面文件连接管理器提供的文件格式定义将平面文件源配置为从单个平面文件提取数据。  
  
 在本教程中，您将把平面文件源配置为使用 `Sample Flat File Source Data` 您之前创建的连接管理器。  
  
### <a name="to-add-a-flat-file-source-component"></a>添加平面文件源组件  
  
1.  通过双击**Data Flow**数据流 `Extract Sample Currency Data` 任务或单击 "数据流"**选项卡**，打开 "数据流设计器"。  
  
2.  在“SSIS 工具箱”**** 中，展开 **OtherSources**，然后将“平面文件源”**** 拖动到“数据流”**** 选项卡的设计图面上。  
  
3.  在 "**数据流" 设计图面**上，右键单击新添加的 "**平面文件源**"，单击 "**重命名**"，然后将名称更改为 `Extract Sample Currency Data` 。  
  
4.  双击此平面文件源，打开“平面文件源编辑器”对话框。  
  
5.  在 "**平面文件连接管理器**" 框中，选择 `Sample Flat File Source Data` 。  
  
6.  单击“列”**** 并验证列名是否正确。  
  
7.  单击“确定”  。  
  
8.  右键单击“平面文件源”并单击“属性”****。  
  
9. 在属性窗口中，验证 `LocaleID` 属性是否设置为**英语 (美国) **。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 6：添加并配置查找转换](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>另请参阅  
 [平面文件源](data-flow/flat-file-source.md)   
 [平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)  
  
  
