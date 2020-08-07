---
title: 使用 SQL Server Native Client 连接到 Azure SQL 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: rothja
ms.author: jroth
ms.openlocfilehash: 177c655f97e32f2044460e87c6cd775cdf8fcde9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587774"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>使用 SQL Server Native Client 连接到 Azure SQL 数据库
  有关演示如何使用 Native Client 连接到的示例 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请参阅[开发： (Azure SQL 数据库) 的操作指南主题](https://msdn.microsoft.com/library/ee621787.aspx)。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>连接到 SQL Database 时的已知问题  
 以下是使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client 连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时的一些已知问题：  
  
-   如果分阶段使用 `SQLBrowseConnect`，则使用 `SQLBrowseConnect` 建立的连接可能被拒绝。  例如，如果在第一次调用中发送驱动程序名称，在第二次调用中发送服务器和凭据（用户名和密码），建立连接，然后在第三次调用中发送数据库名称和语言。  第三次调用将导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 发出 USE 语句来更改数据库。 但是，在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 中不支持 USE 语句，因此生成以下错误：  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Native Client 生成应用程序](building-applications-with-sql-server-native-client.md)  
  
  
