---
title: 使用 sqlcmd 连接到数据库引擎
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd utility, Database Engine connections
- Named Pipes [SQL Server], sqlcmd utility
- TCP/IP [SQL Server], client protocols
- network protocols [SQL Server], sqlcmd utility
- protocols [SQL Server], sqlcmd utility
- VIA
- client protocols [SQL Server]
ms.assetid: 74b0fb71-7f8e-4171-9431-d07528532524
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b409683b651e3e6508baced5eb3bc9fcc631e2c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578784"
---
# <a name="connect-to-the-database-engine-with-sqlcmd"></a>使用 sqlcmd 连接到数据库引擎
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持客户端使用 TCP/IP 网络协议（默认）和命名管道协议进行通信。 如果客户端正在连接到同一计算机上的[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，则还可使用 Shared Memory 协议。 通常有三种选择协议的方法。 **sqlcmd** 实用工具使用的协议按下列顺序确定：  
  
-   **sqlcmd** 使用为连接字符串中指定的协议，如下所述。  
  
-   如果连接字符串中未指定任何协议，则 **sqlcmd** 将使用连接到的别名中定义的协议。 若要将 **sqlcmd**配置为通过创建别名使用特定网络协议，请参阅[创建或删除供客户端使用的服务器别名 (SQL Server 配置管理器)](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)。  
  
-   如果未通过其他方法指定协议， **sqlcmd** 将使用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中的协议顺序确定的网络协议。  
  
 下面的示例显示连接到 1433 端口上默认的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例以及假定侦听 1691 端口的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 命名实例的各种方法。 其中一些示例使用环回适配器的 IP 地址 (127.0.0.1)。 请使用您的计算机网络接口卡的 IP 地址进行测试。  
  
 通过指定实例名连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S ComputerA  
sqlcmd -S ComputerA\instanceB  
```  
  
 通过指定 IP 地址连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S 127.0.0.1  
sqlcmd -S 127.0.0.1\instanceB  
```  
  
 通过指定 TCP\IP 端口号连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] ：  
  
```  
sqlcmd -S ComputerA,1433  
sqlcmd -S ComputerA,1691  
sqlcmd -S 127.0.0.1,1433  
sqlcmd -S 127.0.0.1,1691  
```  
  
### <a name="to-connect-using-tcpip"></a>使用 TCP/IP 进行连接  
  
-   使用以下常规语法进行连接：  
  
    ```  
    sqlcmd -S tcp:<computer name>,<port number>  
    ```  
  
-   连接到默认实例：  
  
    ```  
    sqlcmd -S tcp:ComputerA,1433  
    sqlcmd -S tcp:127.0.0.1,1433  
    ```  
  
-   连接到命名实例：  
  
    ```  
    sqlcmd -S tcp:ComputerA,1691  
    sqlcmd -S tcp:127.0.0.1,1691  
    ```  
  
### <a name="to-connect-using-named-pipes"></a>使用命名管道进行连接  
  
-   使用下列常规语法之一进行连接：  
  
    ```  
    sqlcmd -S np:\\<computer name>\<pipe name>  
    ```  
  
-   连接到默认实例：  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\sql\query  
    ```  
  
-   连接到命名实例：  
  
    ```  
    sqlcmd -S np:\\ComputerA\pipe\MSSQL$<instancename>\sql\query  
    sqlcmd -S np:\\127.0.0.1\pipe\MSSQL$<instancename>\sql\query  
    ```  
  
### <a name="to-connect-using-shared-memory-a-local-procedure-call-from-a-client-on-the-server"></a>在服务器上从客户端使用共享内存（本地过程调用）进行连接  
  
-   使用下列常规语法之一进行连接：  
  
    ```  
    sqlcmd -S lpc:<computer name>  
    ```  
  
-   连接到默认实例：  
  
    ```  
    sqlcmd -S lpc:ComputerA  
    ```  
  
-   连接到命名实例：  
  
    ```  
    sqlcmd -S lpc:ComputerA\<instancename>  
    ```  
  
  
