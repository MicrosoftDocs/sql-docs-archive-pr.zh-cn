---
title: 恢复可用性数据库 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.resumedatamove.f1
helpviewer_keywords:
- Availability Groups [SQL Server], resuming a database
- secondary databases [SQL Server], in availability group
- primary databases [SQL Server], in availability group
- Availability Groups [SQL Server], databases
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a2279940c2502a310e9dac4448bd6029b6e13dc
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693106"
---
# <a name="resume-an-availability-database-sql-server"></a>恢复可用性数据库 (SQL Server)
  您可以通过使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的 PowerShell，在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中恢复已挂起的可用性数据库。 恢复挂起的数据库会将数据库置于 SYNCHRONIZING 状态。 恢复主数据库还将恢复挂起主数据库时导致挂起的任何辅助数据库。 如果任何辅助数据库是从承载辅助副本的服务器实例中本地挂起的，则该辅助数据库必须进行本地恢复。 一旦给定的辅助数据库和相应的主数据库处于 SYNCHRONIZING 状态，则在辅助数据库上将恢复数据同步。  
  
> [!NOTE]  
>  暂停和恢复 AlwaysOn 辅助数据库并不直接影响主数据库的可用性。 但是，暂停某一辅助数据库可能会在恢复这个暂停的辅助数据库之前影响主数据库的冗余和故障转移功能。 这与数据库镜像相反，在数据库镜像中，在恢复镜像前镜像状态在镜像数据库和主数据库上都挂起。 挂起 AlwaysOn 主数据库将挂起所有相应辅助数据库上的数据移动，并且在恢复主数据库前针对该数据库的冗余和故障转移功能将停止。  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要恢复辅助数据库，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [相关任务](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
 RESUME 命令只要被承载目标数据库的副本接受后就返回，但是实际上继续数据库以异步方式发生。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   您必须连接到承载要恢复的数据库的服务器实例。  
  
-   可用性组必须联机。  
  
-   主数据库必须处于联机状态且可用。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 需要对数据库拥有 ALTER 权限。  
  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **恢复辅助数据库**  
  
1.  在对象资源管理器中，连接到承载要恢复的数据库所在的可用性副本的服务器实例，然后展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  展开该可用性组。  
  
4.  展开“可用性数据库”节点，右键单击该数据库，然后单击“恢复数据移动”。  
  
5.  在 **“恢复数据移动”** 对话框中，单击 **“确定”** 。  
  
> [!NOTE]  
>  若要恢复此副本位置上的其他数据库，请对每个数据库重复执行步骤 4 和 5。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **恢复本地挂起的辅助数据库**  
  
1.  连接到承载想要恢复其数据库的辅助副本的服务器实例。  
  
2.  通过使用下面的 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)语句恢复辅助数据库：  
  
     更改数据库*database_name*设置 HADR 简历  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-resume-a-secondary-database"></a>恢复辅助数据库
  
1.  将目录 (`cd`) 更改为承载要恢复的数据库所在副本的服务器实例。 有关详细信息，请参阅本主题前面的 [先决条件](#Prerequisites)。  
  
2.  使用 **Resume-SqlAvailabilityDatabase** cmdlet 恢复可用性组。  
  
     例如，下面的命令针对可用性组 `MyDb3` 中的可用性数据库 `MyAg`恢复数据同步。  
  
    ```powershell
    Resume-SqlAvailabilityDatabase -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [挂起可用性数据库 (SQL Server)](suspend-an-availability-database-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)  
