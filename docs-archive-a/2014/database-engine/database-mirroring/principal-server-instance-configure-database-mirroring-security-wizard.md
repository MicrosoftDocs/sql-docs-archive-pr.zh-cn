---
title: 主题服务器实例（配置数据库镜像安全向导）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2632b5ffd5355065b4b5c1f905b3b6e5c5b6204d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690124"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>主体服务器实例（配置数据库镜像安全向导）
  使用此页可以指定有关主体数据库的服务器实例的信息。 主体数据库是开始镜像会话的数据库的副本。 会话开始后，主体数据库是接受用户更改的数据库副本。 （当发生故障转移时，主体和镜像角色交换；因此，初始的主体数据库可能不再是主体数据库。）  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动配置数据库镜像安全向导 (SQL Server Management Studio)](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>选项  
 **主体服务器实例**  
 因为 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的数据库镜像总是从主体服务器配置，所以当前的服务器实例总是为主体服务器实例。  
  
 **侦听程序端口**  
 此选项的行为取决于此服务器实例是否存在镜像端点，如下所示：  
  
-   如果此服务器实例不存在侦听器端口，则端口号 5022 将显示在 **“端口”** 文本框中。 可以使用任何可用的端口号，例如 7022。  
  
-   如果镜像端点已经存在，则会显示该端点的端口号。 如果需要更改端口，请使用 ALTER ENDPOINT 命令。 有关详细信息，请参阅 [ALTER ENDPOINT (Transact-SQL)](/sql/t-sql/statements/alter-endpoint-transact-sql)。  
  
> [!NOTE]  
>  端口号是必需的。  
  
 **终结点名称**  
 如果此服务器实例存在镜像端点，则端点名称将显示在此处。 如果端点不存在，则可以指定端点的名称。  
  
 **加密通过此端点发送的数据**  
 默认情况下，将启用加密。 如果启用，则要求（而不仅仅是支持）进行加密，并且所有加密选项都将使用默认值。 有关详细信息，请参阅 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)的信息。  
  
 若要禁用加密，请清除此复选框。 若要重新启用加密，请选中此复选框。  
  
## <a name="see-also"></a>另请参阅  
 [数据库镜像终结点 (SQL Server)](the-database-mirroring-endpoint-sql-server.md)   
 [数据库属性（“镜像”页）](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [启动数据库镜像监视器 (SQL Server Management Studio)](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [数据库镜像 (SQL Server)](database-mirroring-sql-server.md)  
  
  
