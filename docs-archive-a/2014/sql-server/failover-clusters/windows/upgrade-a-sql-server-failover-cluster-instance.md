---
title: 升级 SQL Server 故障转移群集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ca08e83c362e714f234a60ee358df3bcb03ade93
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586257"
---
# <a name="upgrade-a-sql-server-failover-cluster"></a>升级 SQL Server 故障转移群集
  在所有故障转移群集节点上，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 都支持[!INCLUDE[ssDE](../../../includes/ssde-md.md)]和 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 分别从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]  故障转移群集升级。  
  
 支持详细信息如下所示：  
  
-   既支持通过用户界面进行升级，也支持从命令提示符进行升级。 有关详细信息，请参阅[升级 SQL Server 故障转移群集实例（安装程序）](upgrade-a-sql-server-failover-cluster-instance-setup.md)和[从命令提示符安装 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
-   从升级 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] -可以从命令提示符在每个故障转移群集节点上运行升级，也可以使用安装程序 UI 来升级每个群集节点。 如果要升级的实例上不存在全文搜索和复制功能，则会自动安装它们，而不能选择忽略它们。  
  
-   Service Pack 安装 – 必须将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 和修补程序分别应用于所有节点上的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 故障转移群集。  
  
-   不支持以下方案：  
  
    -   不能从独立的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例迁移到故障转移群集。  
  
    -   向故障转移群集中添加功能。 例如，不能向现在仅 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 的故障转移群集中添加 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
    -   不能将故障转移群集节点降级为独立的实例。  
  
-   有关详细信息，请参阅 [AlwaysOn 故障转移群集实例 (SQL Server)](always-on-failover-cluster-instances-sql-server.md)。  
  
## <a name="upgrading-a-ssnoversion-multi-subnet-failover-cluster"></a>升级 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集  
 不能直接将非多子网 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集升级到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 多子网故障转移群集。 有关详细信息，请参阅[升级 SQL Server 故障转移群集实例（安装程序）](upgrade-a-sql-server-failover-cluster-instance-setup.md)。  
  
## <a name="see-also"></a>另请参阅  
 [支持的版本升级](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [&#40;安装程序升级 SQL Server 故障转移群集实例&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
  
