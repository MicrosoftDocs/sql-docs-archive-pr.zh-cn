---
title: 创建 Finance Name 策略 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 44ffff45f126d2ad9b73c5b8410b8f89ad2b0604
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578155"
---
# <a name="create-the-finance-name-policy"></a>创建 Finance Name 策略
  在本任务中，将创建一个名为 Finance 的数据库，然后创建一个要求所有表以字母 **fintbl**开头的条件。 然后，将创建一个策略和策略类别，强制 Finance 数据库中的表执行某一命名标准。  
  
### <a name="to-create-the-finance-database"></a>创建 Finance 数据库  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，打开查询窗口并执行以下语句：  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  在对象资源管理器中，单击“数据库”****，然后按 F5 键刷新数据库列表。  
  
### <a name="to-create-the-finance-tables-condition"></a>创建 Finance 表条件  
  
1.  在对象资源管理器中，依次展开“管理”**** 和“策略管理”****，右键单击“条件”****，然后单击“新建条件”****。  
  
2.  在“创建新条件”**** 对话框的“名称”**** 框中，键入 **Finance Tables**。  
  
3.  在“Facet”**** 列表中，选择“多部分名称”****。  
  
4.  在 "**表达式**" 区域中，在 "**字段**" 框中选择 " ** \@ 名称**"; 在 "**运算符**" 框中选择 "**与**"; 在 "**值**" 框中，键入 **"fintbl 开头%"** 以强制所有表名称以字母**fintbl 开头**开头。  
  
5.  在“说明”**** 页中，键入 **Finance table names must begin with fintbl**，然后单击“确定”**** 以创建条件。  
  
### <a name="to-create-the-finance-name-policy"></a>创建 Finance Name 策略  
  
1.  在对象资源管理器中，右键单击“策略”****，然后单击“新建策略”****。  
  
2.  在“新建新策略”**** 对话框的“名称”**** 框中，键入 **Finance Name**。  
  
3.  在“检查条件”**** 列表中，选择“Finance Tables”****。 它位于“多部分名称”**** 区域中。  
  
4.  在“针对”**** 区域中，将会看到可能应用了此策略的数据库对象的列表。 选中“每个表”**** 复选框。  
  
5.  在“每个数据库”**** 区域中，展开“每个”****，然后单击“新建条件”****。  
  
6.  在“创建新条件”**** 对话框的“名称”**** 框中，键入 **Finance Database**。  
  
7.  在 "**表达式**" 框中，完成表达式以包含** \@ Name = ' 财务 '**，然后单击 **"确定**" 关闭条件页。  
  
    > [!NOTE]  
    >  可能需要按 Tab 键移出“值”**** 框才能启用“确定”**** 按钮。  
  
8.  在“评估模式”**** 列表中，选择“更改时: 禁止”****。 这会对 Finance 数据库创建数据库触发器以强制实施策略。  
  
9. 选择“已启用”**** 列表。 （“已启用”**** 框不适用于“按需”**** 策略。）  
  
10. 在“服务器限制”**** 列表中，选择“无”****。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>创建 Finance 策略类别  
  
1.  在对象资源管理器中，展开“管理”****，右键单击“策略管理”****，然后单击“管理类别”****。  
  
2.  在 "**管理策略类别**" 对话框中的 "**名称**" 下，键入 `Finance` 空白框，然后清除 "托管**数据库订阅**"。 “托管数据库订阅”**** 将强制实例中的每个数据库订阅属于该策略类别的策略。 在本课中，只有 Finance 数据库应订阅 Finance Name 策略。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [订阅和检查 Finance Name 策略](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
