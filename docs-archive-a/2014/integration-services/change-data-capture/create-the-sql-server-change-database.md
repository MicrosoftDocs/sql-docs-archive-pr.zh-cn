---
title: 创建 SQL Server 更改数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0eaeb26d5bea4c9e50db29aaa45297ba763dbbfa
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693018"
---
# <a name="create-the-sql-server-change-database"></a>创建 SQL Server 更改数据库
  当您启动新建实例向导时，“创建 CDC 数据库”页将打开。 使用“创建 CDC 数据库”页可提供与新的 CDC 实例有关的信息并且创建新的更改数据库。  
  
 在您创建新的 CDC 数据库时，将为 SQL Server CDC 启用该数据库，并且此启用将要求作为 `sysadmin` 固定服务器角色的成员的登录名。  
  
 在启动“创建 Oracle CDC 实例”向导的用户不是 `sysadmin` 固定服务器角色的成员时，“连接到 SQL Server”对话框将打开，并且请求 sysadmin 角色成员的凭据以便执行“为 SQL Server CDC 启用数据库”任务。 在创建 CDC 数据库时， `sysadmin` 登录名将被放弃，并且使用在进入 Oracle 设计器控制台时使用的原始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名继续工作。  
  
> [!IMPORTANT]  
>  对于并非“为 SQL Server CDC 启用数据库”的其他任务，用于运行“新建实例向导”的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名必须具有 `dbcreator` 固定服务器角色，并且对 MSXDBCDC 数据库具有 UPDATE 权限。  
  
 有关在“连接到 SQL Server”对话框中输入数据的信息，请参阅 [SQL Server Connection for Instance Creation](sql-server-connection-for-instance-creation.md)。  
  
## <a name="options"></a>选项  
 **Oracle CDC 实例**  
 键入与您正创建的 CDC 实例有关的以下信息。  
  
-   **名称**：键入新服务的名称。 该名称将是新的更改数据库的名称。  
  
-   **说明**：为新实例键入用于帮助标识它的说明。 此为可选项。  
  
 **SQL Server 更改数据库**  
 此部分用于创建数据库。  
  
1.  **更改数据库**：新的更改数据库的名称。 该数据库的名称就是您向实例提供的名称。 此只读字段显示数据库的完整路径。  
  
2.  **创建数据库**：单击 **“创建数据库”** 可创建数据库。  
  
     若要创建数据库，该登录名必须具有 `sysasmin` 服务器角色。 有关详细信息，请参阅上面的安全说明。  
  
     创建数据库后，可以单击 **“下一步”** 以便 [Connect to an Oracle Source Database](connect-to-an-oracle-source-database.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何创建 SQL Server 更改数据库实例](how-to-create-the-sql-server-change-database-instance.md)   
 [Oracle CDC 服务](the-oracle-cdc-service.md)  
  
  
