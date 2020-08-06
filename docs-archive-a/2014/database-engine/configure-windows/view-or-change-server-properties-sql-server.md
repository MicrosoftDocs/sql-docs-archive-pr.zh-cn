---
title: 查看或更改服务器属性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 415d4e2d1aaa3166ae4df2dea53b34e064544e06
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688192"
---
# <a name="view-or-change-server-properties-sql-server"></a>查看或更改服务器属性 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 配置管理器查看或更改 [!INCLUDE[tsql](../../includes/tsql-md.md)]实例的属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要查看或更改服务器属性，请使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server 配置管理器](#PowerShellProcedure)  
  
-   **跟进：**  [更改服务器属性之后](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   使用 sp_configure 时，必须在设置配置选项之后运行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。 RECONFIGURE WITH OVERRIDE 语句通常专门用来设置那些使用起来应当十分小心的配置选项。 但是，RECONFIGURE WITH OVERRIDE 可用于所有的配置选项，并且可以用它代替 RECONFIGURE。  
  
    > [!NOTE]  
    >  RECONFIGURE 在事务内部执行。 如果任意重新配置选项失败，则所有重新配置操作都将失效。  
  
-   有些属性页会显示通过 Windows Management Instrumentation (WMI) 获得的信息。 若要显示这些页，WMI 必须安装在运行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的计算机上。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 有关详细信息，请参阅 [服务器级别角色](../../relational-databases/security/authentication-access/server-level-roles.md)。  
  
 `sp_configure`默认情况下，不带参数的执行权限或仅将第一个参数授予所有用户。 若要 `sp_configure` 使用这两个参数来更改配置选项或运行重新配置语句，必须向用户授予 ALTER SETTINGS 服务器级别权限。 ALTER SETTINGS 权限由 **sysadmin** 和 **serveradmin** 固定服务器角色隐式持有。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>查看或更改服务器属性  
  
1.  在“对象资源管理器”中，右键单击服务器，再单击“属性” 。  
  
2.  在 **“服务器属性”** 对话框中，单击某页以查看或更改有关该页的服务器信息。 某些属性是只读属性。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>通过使用 SERVERPROPERTY 内置函数查看服务器属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例在 [语句中使用](/sql/t-sql/functions/serverproperty-transact-sql) SERVERPROPERTY `SELECT` 内置函数，以返回有关当前服务器的信息。 如果基于 Windows 的服务器上安装了多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，而且客户端必须打开另一个到当前连接所使用的同一实例连接，则此方案很有用。  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>通过使用 sys.servers 目录视图查看服务器属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例查询 [sys.servers](/sql/relational-databases/system-catalog-views/sys-servers-transact-sql) 目录视图，以返回当前服务器的名称 (`name`) 和 ID (`server_id`)，以及用于连接到链接服务器的 OLE DB 访问接口 (`provider`) 的名称。  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysconfigurations-catalog-view"></a>通过使用 sys.configurations 目录视图查看服务器属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例查询 [sys.configurations](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql) 目录视图，以返回有关当前服务器上的各个服务器配置选项的信息。 该示例返回选项的名称 (`name`) 和说明 (`description`)，以及该选项是否为高级选项 (`is_advanced`)。  
  
    ```sql
    USE AdventureWorks2012;
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;
    GO
    ```  
  
#### <a name="to-change-a-server-property-by-using-sp_configure"></a>通过使用 sp_configure 更改服务器属性  
  
1.  连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”** 。  
  
3.  将以下示例复制并粘贴到查询窗口中，然后单击“执行” 。 此示例显示如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 更改服务器属性。 本示例将 `fill factor` 选项的值更改为 `100`。 必须重新启动服务器，更改才会生效。  
  
```sql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 有关详细信息，请参阅 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)版本的组合自动配置的最大工作线程数。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="PowerShellProcedure"></a> 使用 SQL Server 配置管理器  
 可以通过使用 SQL Server 配置管理器查看或更改某些服务器属性。 例如，您可以查看 SQL Server 实例的版本，或更改存储错误日志文件的位置。 也可以通过查询 [服务器相关的动态管理视图和函数](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql)来查看这些属性。  
  
#### <a name="to-view-or-change-server-properties"></a>查看或更改服务器属性  
  
1.  在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
2.  在 **“SQL Server 配置管理器”** 中，单击 **“SQL Server 服务”** 。  
  
3.  在“详细信息”窗格中，右键单击“SQL Server (\<***instancename***>)”，再单击“属性” 。  
  
4.  在“SQL Server (\<***instancename***>) 属性”对话框中，更改“服务”选项卡或“高级”选项卡上的服务器属性，再单击“确定”   。  
  
##  <a name="follow-up-after-you-change-server-properties"></a><a name="FollowUp"></a>跟进：更改服务器属性之后  
 对于某些属性，可能必须重新启动服务器，才能使更改生效。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [SET 语句 (Transact-SQL)](/sql/t-sql/statements/set-statements-transact-sql)   
 [SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql)   
 [在 SQL Server 工具中将 WMI 配置为显示服务器状态](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [SQL Server 配置管理器](../../relational-databases/sql-server-configuration-manager.md)   
 [配置函数 (Transact-SQL)](/sql/t-sql/functions/configuration-functions-transact-sql)   
 [与服务器相关的动态管理视图和函数 (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql)  
