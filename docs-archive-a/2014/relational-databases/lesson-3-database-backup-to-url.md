---
title: 第4课：在 Azure 存储中创建数据库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 50fca85111d5897b738e577e7735049e0b055a03
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590783"
---
# <a name="lesson-4-create-a-database-in-azure-storage"></a>第 4 课：在 Azure 存储中创建数据库
  在本课中，您将学习如何使用 Azure 中的 SQL Server 数据文件功能创建数据库。 注意，开始学习本课之前，必须先学完第 1、2 和 3 课。 第3课是一个非常重要的步骤，因为你需要在第4课之前将有关 Azure 存储容器及其关联的策略名称和 SAS 密钥的信息存储在 SQL Server 凭据存储中。  
  
 对于数据或日志文件使用的每个存储容器，都必须创建一个 SQL Server 凭据，其名称与容器路径相同。 然后，你可以在 Azure 存储中创建新的数据库  
  
 本课假定您已完成以下步骤：  
  
-   你有 Azure 存储帐户。  
  
-   在 Azure 存储帐户下创建了容器。  
  
-   已在容器上创建了具有读取、写入和列表权限的策略。 还生成了 SAS 密钥。  
  
-   已在源计算机上创建了 SQL Server 凭据。  
  
 若要使用 "Azure 存储中的 SQL Server 数据文件" 功能在 Azure 中创建数据库，请执行以下步骤：  
  
1.  连接到 SQL Server Management Studio。  
  
2.  在对象资源管理器中，连接到所安装的数据库引擎实例。  
  
3.  在“标准”工具栏上，单击“新建查询”。  
  
4.  将以下示例复制并粘贴到查询窗口中，并根据需要进行修改。 注意，FILENAME 字段指代存储容器中数据库文件的 URI 路径，它必须以 https 开头。  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     向数据库添加一些数据。  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  若要查看本地 SQL Server 上的新 TestDB1，请在对象资源管理器中刷新数据库。  
  
6.  同样，若要查看在存储帐户中新建的数据库，请通过 SQL Server Management Studio (SSMS) 连接到存储帐户。 有关如何使用 SQL Server Management Studio 连接到 Azure 存储的信息，请执行以下步骤：  
  
    1.  首先，获取存储帐户信息。 登录到管理门户。 然后，单击 **“存储”** 并选择您的存储帐户。 选择存储帐户后，单击页面底部的 **“管理访问密钥”** 。 此操作将打开一个类似的对话框窗口：  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  将 "**存储帐户名称**" 和 "**主访问密钥**" 值复制到 SSMS 中的 "**连接到 Azure 存储**" 对话框窗口。 然后单击 **“连接”**。 此操作将有关存储帐户容器的信息提供给 SSMS，如下面的屏幕快照所示：  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 以下屏幕截图演示了在本地和 Azure 存储环境中新建的数据库。  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **注意：** 如果当前引用了容器中的任何数据文件，则尝试删除关联的 SQL Server 凭据总是会失败。 同样，如果在 blob 中的特定数据库文件上已有租约并且要删除它，则需要先中断 blob 上的租约。 若要中断租约，可以使用 [租约 Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx)。  
  
 可使用此项新功能配置 SQL Server，以使任何 CREATE DATABASE 语句都默认使用支持云的数据库。 换句话说，你可以在 SQL Server Management Studio 服务器实例属性中设置默认数据和日志位置，因此在创建数据库时，所有数据库文件 ( .mdf) 都作为页 blob 创建在 Azure 存储中。  
  
 若要使用 SQL Server Management Studio 用户界面在 Azure 存储中创建数据库，请执行以下步骤：  
  
1.  在对象资源管理器中，连接到一个 SQL Server 数据库引擎实例，然后展开该实例。  
  
2.  右键单击“数据库”，然后单击“新建数据库”。  
  
3.  在“新建数据库”对话框窗口中，键入数据库名称。  
  
4.  更改主数据文件和事务日志文件的默认值，在“数据库文件”网格中单击相应的单元格并输入新值。 此外，指定文件位置的路径。 在“路径”中，键入存储容器的 URL 路径，如 `https://teststorageaccnt.blob.core.windows.net/testcontainer/`。 在“文件名”中，键入数据库文件的物理文件名（.mdf、.ldf）。  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     有关详细信息，请参阅 [向数据库中添加数据文件或日志文件](databases/add-data-or-log-files-to-a-database.md)。  
  
5.  保留所有其他默认值。  
  
6.  单击“确定”。  
  
 若要查看本地 SQL Server 上的新 TestDB1，请在对象资源管理器中刷新数据库。 同样，若要查看在存储帐户中新建的数据库，请通过 SQL Server Management Studio (SSMS) 连接到存储帐户，如本课程前面所述。  
  
 **下一课：**  
  
 [第5课。&#40;可选&#41; 使用 TDE 加密数据库](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
