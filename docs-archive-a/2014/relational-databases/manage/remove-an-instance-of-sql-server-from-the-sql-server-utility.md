---
title: 从 SQL Server 实用工具中删除 SQL Server 实例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6c09897fcd3ac6d82308288391cf54176eef49d9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591334"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>从 SQL Server 实用工具中删除 SQL Server 实例
  使用以下步骤从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。 此过程从 UCP 列表视图中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具数据收集将停止。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不卸载。  
  
> [!IMPORTANT]  
>  在您使用此过程从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例前，请确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 SQL Server 代理服务正在要删除的实例上运行。  
  
1.  从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的实用工具资源管理器中，单击 **“托管实例”** 。 观察实用工具资源管理器内容窗格中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的列表视图。  
  
2.  在该列表视图的 **“SQL Server 实例名称”** 列中，选择要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具删除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 右键单击要删除的实例，然后选择“删除托管实例…”。  
  
3.  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的管理员权限指定凭据：单击“连接...”，确认“连接到服务器”对话框中的信息，然后单击“连接”。   您将在 **“删除托管实例”** 对话框中看到登录信息。  
  
4.  若要确认该操作，请单击 **“确定”** 。 若要退出该操作，请单击 **“取消”** 。  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>手动从 SQL Server 实用工具中删除 SQL Server 的托管实例  
 此过程从 UCP 列表视图中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例并且停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具数据收集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不卸载。  
  
 使用 PowerShell 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。 此脚本执行以下操作：  
  
-   按服务器实例名称获取 UCP。  
  
-   从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
```powershell
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
务必 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 严格按照存储在中的实例名称进行引用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的区分大小写的实例上，必须使用与 @@SERVERNAME 返回的完全一致的大小写来指定实例名称。 

若要获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例的实例名称，请对该托管实例运行以下查询：  
  
```sql
select @@SERVERNAME AS instance_name  
```  
  
 此时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例将从 UCP 完全删除。 在您下次刷新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的数据时，该托管实例将从列表视图中消失。 此状态完全等同于用户成功在 SSMS 用户界面中完成删除托管实例操作。  
  
## <a name="see-also"></a>另请参阅  
 [使用实用工具资源管理器管理 SQL Server 实用工具](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server 实用工具故障排除](../../database-engine/troubleshoot-the-sql-server-utility.md)  
