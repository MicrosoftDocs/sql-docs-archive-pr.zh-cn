---
title: 隐藏 SQL Server 数据库引擎的实例 | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], hiding instances
- hiding instances of Database Engine
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d2b3287c5d4d747ccb3511461341d5aed8ff765d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688228"
---
# <a name="hide-an-instance-of-sql-server-database-engine"></a>隐藏 SQL Server 数据库引擎的实例
  本主题说明如何使用 SQL Server 配置管理器在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中隐藏 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 实例。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浏览器服务来枚举安装在计算机上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。 这使客户端应用程序可以浏览服务器，并帮助客户端区别同一台计算机上的多个 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例。 您可以使用以下过程防止 SQL Server Browser 服务向尝试通过使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] “浏览” **按钮来查找实例的客户端计算机公开** 实例。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-hide-an-instance-of-the-sql-server-database-engine"></a>隐藏 SQL Server 数据库引擎实例  
  
1.  在“SQL Server 配置管理器”中，展开“SQL Server 网络配置”，右键单击“\<server instance> 的协议”，然后选择“属性”。    
  
2.  在 **“标志”** 选项卡的 **“隐藏实例”** 框中，选择 **“是”** ，然后单击 **“确定”** 关闭对话框。 对于新连接，更改会立即生效。  
  
## <a name="remarks"></a>备注  
 如果你隐藏命名实例，你将需要在连接字符串中提供端口号才能连接到隐藏的实例，即使浏览器服务正在运行也是如此。 对于命名隐藏实例，我们建议你使用静态端口而不是动态端口。  
  有关详细信息，请参阅[将服务器配置为侦听特定 TCP 端口（SQL Sever 配置管理器）](configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
### <a name="clustering"></a>群集  
 如果你隐藏群集命名实例，则群集服务可能无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这将导致群集实例的**IsAlive**检查失败，并 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将脱机。 我们建议在群集实例的所有节点中创建别名，以反映你为该实例配置的静态端口。  
 有关详细信息，请参阅[创建或删除供客户端使用的服务器别名（SQL Server 配置管理器）](create-or-delete-a-server-alias-for-use-by-a-client.md)。  
  
 如果隐藏群集命名实例，当 **LastConnect** 注册表项 (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) 具有的端口与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在侦听的端口不同时，群集服务可能无法连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果群集服务无法建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的连接，则你可能会看到类似于以下内容的错误：  
**事件 ID：1001：事件名称：故障转移群集资源死锁。**  
  
## <a name="see-also"></a>另请参阅  
 [服务器网络配置](server-network-configuration.md)   
 [SQL 虚拟服务器客户端连接的说明](https://support.microsoft.com/kb/273673)   
 [如何将静态端口分配到 SQL Server 命名实例并避免常见缺陷](https://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  
