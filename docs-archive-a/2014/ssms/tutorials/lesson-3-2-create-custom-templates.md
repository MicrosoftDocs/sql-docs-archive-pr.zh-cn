---
title: 创建自定义模板 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tql
- templates [Transact-SQL], creating
- templates [Transact-SQL]
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 771547b9c47672d2c075b5e7215d78744fe5f18e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690275"
---
# <a name="create-custom-templates"></a>创建自定义模板
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 附带用于许多常见任务的模板，但模板的真正作用在于它能为必须频繁创建的复杂脚本创建自定义模板。 在本练习中，您将创建带有较少参数的简单脚本，但是模板也适用于较长的重复脚本。  
  
## <a name="using-custom-templates"></a>使用自定义模板  
  
#### <a name="to-create-a-custom-template"></a>创建自定义模板  
  
1.  在模板资源管理器中，展开“SQL Server 模板”****，右键单击“存储过程”****，指向“新建”****，然后单击“文件夹”****。  
  
2.  键入 **Custom** 作为新模板文件夹的名称，然后按 Enter。  
  
3.  右键单击“Custom”****，指向“新建”****，然后单击“模板”****。  
  
4.  键入 **WorkOrdersProc** 作为新模板的名称，然后按 **Enter**。  
  
5.  右键单击“WorkOrdersProc”****，然后单击“编辑”****。  
  
6.  在“连接到数据库引擎”**** 对话框中，验证连接信息，然后单击“连接”****。  
  
7.  在查询编辑器中，键入以下脚本以创建用于查找特定部分（在此事例中是 Blade）顺序的存储过程。 （您可以从“教程”窗口中复制和粘贴代码。）  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  按 F5 执行此脚本，创建 **WorkOrdersForBlade** 过程。  
  
9. 在对象资源管理器中，右键单击服务器，然后单击“新建查询”****。 系统将打开新的“查询编辑器”窗口。  
  
10. 在查询编辑器中，键入 **EXECUTE dbo.WorkOrdersForBlade**，然后按 F5 执行查询。 确认“结果”**** 窗格返回 Blade 的工作订单列表。  
  
11.  (步骤 7) 中的脚本编辑模板脚本，将 "产品名称" 边栏选项卡替换为参数<strong> *<* product_name</strong>， `nvarchar(50)` ， <strong> *>* 名称</strong>，在四个位置。  
  
    > [!NOTE]  
    >  参数需要三个元素：要替换的参数的名称、该参数的数据类型以及该参数的默认值。  
  
12. 现在脚本应该如下所示：  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. 在“文件”**** 菜单中，单击“保存 WorkOrdersProc.sql”**** 以保存模板。  
  
#### <a name="to-test-the-custom-template"></a>测试自定义模板  
  
1.  在模板资源管理器中，依次展开“存储过程”**** 和“Custom”****，然后双击“WorkOrderProc”****。  
  
2.  在“连接到数据库引擎”**** 对话框中，填写连接信息，然后单击“连接”****。 系统将打开新的“查询编辑器”窗口，其中包含“WorkOrderProc”**** 模板的内容。  
  
3.  在 **“查询”** 菜单上，单击 **“指定模板参数的值”** 。  
  
4.  在 "**替换模板参数**" 对话框中， `product_name` 键入 " **FreeWheel** (覆盖默认内容") ，然后单击 **"确定"** 以关闭 "**替换模板参数**" 对话框，并在查询编辑器中修改脚本。  
  
5.  按 F5 键执行查询，并创建过程。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [将脚本另存为项目或解决方案](lesson-3-3-save-scripts-as-projects-or-solutions.md)  
  
  
