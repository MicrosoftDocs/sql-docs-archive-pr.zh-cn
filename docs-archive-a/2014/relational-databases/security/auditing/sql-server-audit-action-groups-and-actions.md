---
title: SQL Server 审核操作组和操作 | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d388256f8c536724e0819704c268aaad379d85e8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578768"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>SQL Server 审核操作组和操作
  使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit 功能，你可以对服务器级别和数据库级别事件组以及各个事件进行审核。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](sql-server-audit-database-engine.md)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 审核包括零个或多个审核操作项目。 这些审核操作项目可以是一组操作，例如 Server_Object_Change_Group，也可以是单个操作，例如对表的 SELECT 操作。  
  
> [!NOTE]  
>  Server_Object_Change_Group 包括对任何服务器对象（数据库或端点）的 CREATE、ALTER 和 DROP 操作。  
  
 审核可以有以下类别的操作：  
  
-   服务器级别。 这些操作包括服务器操作，例如管理更改以及登录和注销操作。  
  
-   数据库级别。 这些操作包括数据操作语言 (DML) 和数据定义语言 (DDL) 操作。  
  
-   审核级别。 这些操作包括审核过程中的操作。  
  
 针对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 审核组件执行的某些操作本质上是在特定审核中进行审核的，在这些情况下，由于事件发生在父对象上，因此将自动发生审核事件。  
  
 本质上将对下列操作进行审核：  
  
-   服务器审核状态更改（将状态设置为 ON 或 OFF）  
  
 本质上将不对下列事件进行审核：  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 最初创建时会禁用所有审核。  
  
## <a name="server-level-audit-action-groups"></a>服务器级别审核操作组  
 服务器级别审核操作组是类似于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全审核事件类的操作。 有关详细信息，请参阅 [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md)。  
  
 下表介绍了服务器级审核操作组，并提供了适用的等效 SQL Server 事件类。  
  
|操作组名称|说明|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|更改应用程序角色的密码时将引发此事件。 等效于 [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md)。|  
|AUDIT_CHANGE_GROUP|创建、修改或删除任何审核时，均将引发此事件。 创建、修改或删除任何审核规范时，均将引发此事件。 任何针对某审核的更改均将在该审核中审核。 等效于 [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md)。|  
|BACKUP_RESTORE_GROUP|发出备份或还原命令时，将引发此事件。 等效于 [审核备份和还原事件类](../../event-classes/audit-backup-and-restore-event-class.md)。|  
|BROKER_LOGIN_GROUP|引发此事件的目的是为了报告与 Service Broker 传输安全性相关的审核消息。 等效于 [Audit Broker Login Event Class](../../event-classes/audit-broker-login-event-class.md)。|  
|DATABASE_CHANGE_GROUP|创建、更改或删除数据库时将引发此事件。 创建、更改或删除任何数据库时均将引发此事件。 等效于 [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md)。|  
|DATABASE_LOGOUT_GROUP|在包含数据库用户注销某一数据库时，会引发此事件。 等效于 Audit Database Logout 事件类。|  
|DATABASE_MIRRORING_LOGIN_GROUP|引发此事件的目的是为了报告与数据库镜像传输安全性相关的审核消息。 等效于 [Audit Database Mirroring Login Event Class](../../event-classes/audit-database-mirroring-login-event-class.md)。|  
|DATABASE_OBJECT_ACCESS_GROUP|访问数据库对象（如消息类型、程序集和协定）时将引发此事件。<br /><br /> 此事件由对任何数据库的任何访问而引发。 **注意：** 这可能会导致大型审核记录。 <br /><br /> 等效于 [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md)。|  
|DATABASE_OBJECT_CHANGE_GROUP|针对数据库对象（如架构）执行 CREATE、ALTER 或 DROP 语句时将引发此事件。 创建、更改或删除任何数据库对象时均将引发此事件。 **注意：** 这可能会导致大量的审核记录。 <br /><br /> 等效于 [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md)。|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|在数据库范围内更改对象所有者时，将引发此事件。 服务器上任意数据库的任意对象所有权发生更改时，均将引发此事件。 等效于 [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md)。|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|针对数据库对象（例如，程序集和架构）发出 GRANT、REVOKE 或 DENY 语句时将引发此事件。 服务器上任意数据库的任意对象权限发生更改时，均将引发此事件。 等效于 [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md)。|  
|DATABASE_OPERATION_GROUP|数据库中发生操作（如检查点或订阅查询通知）时将引发此事件。 对于任何数据库的任何操作都将引发此事件。 等效于 [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md)。|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|使用 ALTER AUTHORIZATION 语句更改数据库的所有者时，将引发此事件，并将检查执行该操作所需的权限。 服务器上任意数据库的任意数据库所有权发生更改时，均将引发此事件。 等效于 [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md)。|  
|DATABASE_PERMISSION_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的任何主体针对某语句权限发出 GRANT、REVOKE 或 DENY 语句时均将引发此事件（仅适用于数据库事件，例如授予对某数据库的权限）。<br /><br /> 服务器上任意数据库的任意数据库权限发生更改 (GDR) 时，均将引发此事件。 等效于 [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md)。|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|在数据库中创建、更改或删除主体（如用户）时，将引发此事件。 等效于 [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md)。 （还等效于 Audit Add DB Principal 事件类，该事件类针对不推荐使用的 sp_grantdbaccess、sp_revokedbaccess、sp_addPrincipal 和 sp_dropPrincipal 存储过程时发生。）<br /><br /> 使用 sp_addrole 或 sp_droprole 存储过程添加或删除数据库角色时，将引发此事件。 创建、更改或删除任何数据库的任何主体时均将引发此事件。 等效于 [Audit Add Role 事件类](../../event-classes/audit-add-role-event-class.md)。|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|数据库范围内存在模拟操作（如 EXECUTE AS \<principal> 或 SETPRINCIPAL）时将引发此事件。 此事件针对任何数据库中完成的模拟引发。 等效于 [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md)。|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|向数据库角色添加登录名或从中删除登录名时将引发此事件。 此事件类由 sp_addrolemember、sp_changegroup 和 sp_droprolemember 存储过程引发。 任何数据库的任何数据库角色成员发生更改时，均将引发此事件。 等效于 [Audit Add Member to DB Role 事件类](../../event-classes/audit-add-member-to-db-role-event-class.md)。|  
|DBCC_GROUP|主体发出任何 DBCC 命令时，将引发此事件。 等效于 [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md)。|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|指示某个主体尝试登录到包含数据库并且失败。 此类中的事件由新连接引发或由连接池中重用的连接引发。 等效于 [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md)。|  
|FAILED_LOGIN_GROUP|指示主体尝试登录到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，但是失败。 此类中的事件由新连接引发或由连接池中重用的连接引发。 等效于 [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md)。|  
|FULLTEXT_GROUP|指示发生了全文事件。 等效于 [Audit Fulltext Event Class](../../event-classes/audit-fulltext-event-class.md)。|  
|LOGIN_CHANGE_PASSWORD_GROUP|通过 ALTER LOGIN 语句或 sp_password 存储过程更改登录密码时，将引发此事件。 等效于 [Audit Login Change Password Event Class](../../event-classes/audit-login-change-password-event-class.md)。|  
|LOGOUT_GROUP|指示主体已注销 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 此类中的事件由新连接引发或由连接池中重用的连接引发。 等效于 [Audit Logout Event Class](../../event-classes/audit-logout-event-class.md)。|  
|SCHEMA_OBJECT_ACCESS_GROUP|每次在架构中使用对象权限时，都将引发此事件。 等效于 [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md)。|  
|SCHEMA_OBJECT_CHANGE_GROUP|针对架构执行 CREATE、ALTER 或 DROP 操作时将引发此事件。 等效于 [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md)。<br /><br /> 此事件针对架构对象引发。 等效于 [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md)。<br /><br /> 任何数据库的任何架构发生更改时，均将引发此事件。 等效于 [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md)。|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|检查更改架构对象（例如表、过程或函数）的所有者的权限时，会引发此事件。 使用 ALTER AUTHORIZATION 语句指定对象所有者时会引发此事件。 服务器上任意数据库的任意架构所有权发生更改时，均将引发此事件。 等效于 [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md)。|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|对架构对象执行 GRANT、DENY 或 REVOKE 语句时将引发此事件。 等效于 [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md)。|  
|SERVER_OBJECT_CHANGE_GROUP|针对服务器对象执行 CREATE、ALTER 或 DROP 操作时将引发此事件。 等效于 [Audit Server Object Management Event Class](../../event-classes/audit-server-object-management-event-class.md)。|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|服务器范围中的对象的所有者发生更改时将引发此事件。 等效于 [Audit Server Object Take Ownership Event Class](../../event-classes/audit-server-object-take-ownership-event-class.md)。|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的任何主体针对某服务器对象权限发出 GRANT、REVOKE、或 DENY 语句时，将引发此事件。 等效于 [Audit Server Object GDR Event Class](../../event-classes/audit-server-object-gdr-event-class.md)。|  
|SERVER_OPERATION_GROUP|使用安全审核操作（如使更改设置、资源、外部访问或授权）时将引发此事件。 等效于 [Audit Server Operation Event Class](../../event-classes/audit-server-operation-event-class.md)。|  
|SERVER_PERMISSION_CHANGE_GROUP|为获取服务器范围内的权限（例如，创建登录名）而发出 GRANT、REVOKE 或 DENY 语句时，将引发此事件。 等效于 [Audit Server Scope GDR Event Class](../../event-classes/audit-server-scope-gdr-event-class.md)。|  
|SERVER_PRINCIPAL_CHANGE_GROUP|创建、更改或删除服务器主体时将引发此事件。 等效于 [Audit Server Principal Management Event Class](../../event-classes/audit-server-principal-management-event-class.md)。<br /><br /> 主体发出 sp_defaultdb 或 sp_defaultlanguage 存储过程或 ALTER LOGIN 语句时，将引发此事件。 等效于 [Audit Addlogin Event Class](../../event-classes/audit-addlogin-event-class.md)。<br /><br /> 调用 sp_addlogin 和 sp_droplogin 存储过程时会引发此事件。 还等效于 [Audit Login Change Property Event Class](../../event-classes/audit-login-change-property-event-class.md)。<br /><br /> 此事件针对 sp_grantlogin 或 sp_revokelogin 存储过程引发。 等效于 [Audit Login GDR Event Class](../../event-classes/audit-login-gdr-event-class.md)。|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|服务器范围内发生模拟（如 EXECUTE AS \<login>）时将引发此事件。 等效于 [Audit Server Principal Impersonation Event Class](../../event-classes/audit-server-principal-impersonation-event-class.md)。|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|向固定服务器角色添加登录名或从中删除登录名时将引发此事件。 此事件由 sp_addsrvrolemember 和 sp_dropsrvrolemember 存储过程引发。 等效于 [Audit Add Login to Server Role 事件类](../../event-classes/audit-add-login-to-server-role-event-class.md)。|  
|SERVER_STATE_CHANGE_GROUP|修改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务状态时将引发此事件。 等效于 [Audit Server Starts and Stops Event Class](../../event-classes/audit-server-starts-and-stops-event-class.md)。|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|指示主体已成功登录到包含数据库。 等效于 Audit Successful Database Authentication 事件类。|  
|SUCCESSFUL_LOGIN_GROUP|指示主体已成功登录到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 此类中的事件由新连接引发或由连接池中重用的连接引发。 等效于 [Audit Login Event Class](../../event-classes/audit-login-event-class.md)。|  
|TRACE_CHANGE_GROUP|对于检查 ALTER TRACE 权限的所有语句，都会引发此事件。 等效于 [Audit Server Alter Trace Event Class](../../event-classes/audit-server-alter-trace-event-class.md)。|  
|USER_CHANGE_PASSWORD_GROUP|每当使用 ALTER USER 语句更改包含数据库用户的密码时，都会引发此事件。|  
|USER_DEFINED_AUDIT_GROUP|此组监视器事件通过使用 [sp_audit_write (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql) 引发。 通常，触发器或存储过程包括对 `sp_audit_write` 的调用以便实现对重要事件的审核。|  
  
### <a name="considerations"></a>注意事项  
 服务器级别操作组涵盖了整个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中的操作。 例如，如果将相应操作组添加到服务器审核规范中，则将记录任何数据库中的任何架构对象访问检查。 在数据库审核规范中，仅记录该数据库中的架构对象访问。  
  
 服务器级别的操作不允许对数据库级别的操作进行详细筛选。 实现详细操作筛选需要数据库级别的审核，例如，对 Employee 组中登录名的 Customers 表执行的 SELECT 操作进行的审核。 在用户数据库审核规范中不要包括服务器范围的对象，例如系统视图。  
  
## <a name="database-level-audit-action-groups"></a>数据库级别审核操作组  
 数据库级别审核操作组是类似于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全审核事件类的操作。 有关事件类的详细信息，请参阅 [SQL Server Event Class Reference](../../event-classes/sql-server-event-class-reference.md)。  
  
 下表介绍了数据库级别审核操作组，并提供了适用的等效 SQL Server 事件类。  
  
|操作组名称|说明|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|更改应用程序角色的密码时将引发此事件。 等效于 [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md)。|  
|AUDIT_CHANGE_GROUP|创建、修改或删除任何审核时，均将引发此事件。 创建、修改或删除任何审核规范时，均将引发此事件。 任何针对某审核的更改均将在该审核中审核。 等效于 [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md)。|  
|BACKUP_RESTORE_GROUP|发出备份或还原命令时，将引发此事件。 等效于 [审核备份和还原事件类](../../event-classes/audit-backup-and-restore-event-class.md)。|  
|DATABASE_CHANGE_GROUP|创建、更改或删除数据库时将引发此事件。 等效于 [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md)。|  
|DATABASE_LOGOUT_GROUP|在包含数据库用户注销某一数据库时，会引发此事件。 等效于 [审核备份和还原事件类](../../event-classes/audit-backup-and-restore-event-class.md)。|  
|DATABASE_OBJECT_ACCESS_GROUP|访问数据库对象（如证书和非对称密钥）时将引发此事件。 等效于 [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md)。|  
|DATABASE_OBJECT_CHANGE_GROUP|针对数据库对象（如架构）执行 CREATE、ALTER 或 DROP 语句时将引发此事件。 等效于 [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md)。|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|数据库范围中的对象的所有者发生更改时将引发此事件。 等效于 [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md)。|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|针对数据库对象（例如，程序集和架构）发出 GRANT、REVOKE 或 DENY 语句时将引发此事件。 等效于 [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md)。|  
|DATABASE_OPERATION_GROUP|数据库中发生操作（如检查点或订阅查询通知）时将引发此事件。 等效于 [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md)。|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|使用 ALTER AUTHORIZATION 语句更改数据库的所有者时，将引发此事件，并将检查执行该操作所需的权限。 等效于 [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md)。|  
|DATABASE_PERMISSION_CHANGE_GROUP|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的任何用户针对某语句权限发出 GRANT、REVOKE 或 DENY 语句时均将引发此事件（仅适用于数据库事件，例如授予对数据库的权限）。 等效于 [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md)。|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|在数据库中创建、更改或删除主体（如用户）时，将引发此事件。 等效于 [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md)。 还等效于 [Audit Add DB User 事件类](../../event-classes/audit-add-db-user-event-class.md)，该事件类针对不推荐使用的 sp_grantdbaccess、sp_revokedbaccess、sp_adduser 和 sp_dropuser 存储过程发生。<br /><br /> 使用不推荐使用的 sp_addrole 和 sp_droprole 存储过程添加或删除数据库角色时，将引发此事件。 等效于 [Audit Add Role 事件类](../../event-classes/audit-add-role-event-class.md)。|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|当数据库范围内存在模拟（如 EXECUTE AS 或 SETUSER）时，将引发此事件 \<user> 。 等效于 [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md)。|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|向数据库角色添加登录名或从中删除登录名时将引发此事件。 此事件类与 sp_addrolemember、sp_changegroup 和 sp_droprolemember 存储过程一起使用。等效于 [Audit Add Member to DB Role 事件类](../../event-classes/audit-add-member-to-db-role-event-class.md)|  
|DBCC_GROUP|主体发出任何 DBCC 命令时，将引发此事件。 等效于 [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md)。|  
|FAILED_DATABASE_AUTHENTICATION_GROUP|指示某个主体尝试登录到包含数据库并且失败。 此类中的事件由新连接引发或由连接池中重用的连接引发。 引发此事件。|  
|SCHEMA_OBJECT_ACCESS_GROUP|每次在架构中使用对象权限时，都将引发此事件。 等效于 [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md)。|  
|SCHEMA_OBJECT_CHANGE_GROUP|针对架构执行 CREATE、ALTER 或 DROP 操作时将引发此事件。 等效于 [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md)。<br /><br /> 此事件针对架构对象引发。 等效于 [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md)。 还等效于 [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md)。|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|检查更改架构对象（例如表、过程或函数）的所有者的权限时，将引发此事件。 使用 ALTER AUTHORIZATION 语句指定对象所有者时会引发此事件。 等效于 [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md)。|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|每次对架构对象发出 GRANT、DENY 或 REVOKE 时，均会引发此事件。 等效于 [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md)。|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|指示主体已成功登录到包含数据库。 等效于 Audit Successful Database Authentication 事件类。|  
|USER_CHANGE_PASSWORD_GROUP|每当使用 ALTER USER 语句更改包含数据库用户的密码时，都会引发此事件。|  
|USER_DEFINED_AUDIT_GROUP|此组监视器事件通过使用 [sp_audit_write (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql) 引发。|  
  
## <a name="database-level-audit-actions"></a>数据库级别审核操作  
 数据库级别的操作支持直接对数据库架构以及架构对象（例如表、视图、存储过程、函数、扩展存储过程、队列、同义词）进行的特定操作进行审核。 不审核类型、XML 架构集合、数据库和架构。 架构对象的审核可以在架构和数据库上配置，这意味着指定架构或数据库包含的所有架构对象上的事件都将被审核。 下表介绍了数据库级别的审核操作。  
  
|操作|说明|  
|------------|-----------------|  
|SELECT|发出 SELECT 语句时将引发此事件。|  
|UPDATE|发出 UPDATE 语句时将引发此事件。|  
|INSERT|发出 INSERT 语句时将引发此事件。|  
|DELETE|发出 DELETE 语句时将引发此事件。|  
|EXECUTE|发出 EXECUTE 语句时将引发此事件。|  
|RECEIVE|发出 RECEIVE 语句时将引发此事件。|  
|REFERENCES|检查 REFERENCES 权限时将引发此事件。|  
  
### <a name="considerations"></a>注意事项  
*  数据库级别的审核操作不适用于列。  
  
*  当查询处理器对查询进行参数化时，审核事件日志中会出现参数而不是查询的列值。 
 
*  不会记录 RPC 语句。   
  
## <a name="audit-level-audit-action-groups"></a>审核级别的审核操作组  
 您也可以对审核过程中的操作进行审核。 这些操作可以是服务器范围或数据库范围的操作。 如果在数据库范围内，则仅针对数据库审核规范而进行。 下表介绍了审核级别的审核操作组。  
  
|操作组名称|说明|  
|-----------------------|-----------------|  
|AUDIT_ CHANGE_GROUP|发出以下命令之一时将引发此事件：<br /><br /> -创建服务器审核<br />-ALTER SERVER AUDIT<br />-删除服务器审核<br />-创建服务器审核规范<br />-ALTER SERVER AUDIT 规范<br />-DROP SERVER 审核规范<br />-创建数据库审核规范<br />-ALTER DATABASE 审核规范<br />-删除数据库审核规范|  
  
## <a name="related-content"></a>相关内容  
 [创建服务器审核和服务器审核规范](create-a-server-audit-and-server-audit-specification.md)  
  
 [创建服务器审核和数据库审核规范](create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION (Transact-SQL)](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
