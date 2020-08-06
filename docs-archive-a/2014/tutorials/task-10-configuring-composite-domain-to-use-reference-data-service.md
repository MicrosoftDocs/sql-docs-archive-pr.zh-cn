---
title: 任务10：配置复合域以使用引用数据服务 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d70966b4cde110540bf5008eda4e3151fe32f28d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694191"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>任务 10：配置复合域以使用引用数据服务
  在此任务中，将 "**地址验证**" 复合域配置为使用**Melissa 数据地址检查**服务。 在运行时，在清理活动期间，DQS 将“地址验证”域中各域的值传递给此服务以进行清理。 有关更多详细信息，请参阅[将域/复合域映射到引用数据](https://msdn.microsoft.com/library/hh213030.aspx)。  
  
1.  在**DQS 客户端**的主页中，单击 "**最新知识库**" 下的 "**供应商 (域管理) **以启动"**域管理**"页。  
  
2.  在**域列表**中选择 "**地址验证**" 复合域。  
  
3.  在右侧窗格中，切换到 "**引用数据**" 选项卡。  
  
     ![“引用数据”选项卡](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "“引用数据”选项卡")  
  
4.  单击工具栏上的 "**浏览**" 按钮。  
  
5.  在 "**联机引用数据提供程序目录**" 对话框中，选中 " **Melissa 数据-地址检查**" 旁边的**复选框**。  
  
     ![选择 Melissa 数据 - 地址检查](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "选择 Melissa 数据 - 地址检查")  
  
6.  在右窗格的 "**架构**" 部分中，使用下拉列表将**地址行**域映射到**地址行 (M) ** Schema item。  
  
     ![将 RDS 架构项映射到域](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "将 RDS 架构项映射到域")  
  
7.  单击工具栏上的 "**添加架构项" ("+) ** " 按钮，在列表中创建一个条目。  
  
     ![“添加架构项”工具栏按钮](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "“添加架构项”工具栏按钮")  
  
8.  通过使用下图中所示的下拉列表，映射以下 DQS 域。  
  
     ![将 RDS 架构项映射到域](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "将 RDS 架构项映射到域")  
  
9. 单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 11：发布知识库](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
