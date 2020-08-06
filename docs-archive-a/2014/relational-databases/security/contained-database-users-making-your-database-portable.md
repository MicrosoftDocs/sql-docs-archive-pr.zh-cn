---
title: 包含的数据库用户 - 使数据库可移植 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6aef800c41b0c1b44e285f959d1b9e12c58ea937
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693704"
---
# <a name="contained-database-users---making-your-database-portable"></a>包含的数据库用户 - 使数据库可移植
  使用包含的数据库用户在数据库级别对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 连接进行身份验证。 “包含的数据库”是独立于其他数据库以及承载数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 实例（和 master 数据库）的一种数据库。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持包含的数据库用户进行 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]时，将包含的数据库用户与数据库级别防火墙规则相结合。 本主题介绍与传统的登录名/用户模型和 Windows 或服务器级别防火墙规则相比，使用包含的数据库模型的差异和好处。 在特定情况下，可管理性或应用程序业务逻辑可能仍然需要使用传统登录名/用户模型和服务器级别防火墙规则。  
  
> [!NOTE]  
>  随着 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 发展 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务并转向更有保证的 SLA，你可能需要切换到包含的数据库用户模型和数据库范围防火墙规则，以针对给定数据库获得更高可用性的 SLA 和更高的最大登录率。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议立即考虑进行这类更改。  
  
## <a name="traditional-login-and-user-model"></a>传统的登录名和用户模型  
 在传统的连接模型中，通过提供由 Windows 进行身份验证的用户或组凭据，Windows 用户或 Windows 组成员可连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。 或者该连接会提供名称和密码并且使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接（这在连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]时是唯一选项）。 在这两种情况下，master 数据库必须拥有匹配连接凭据的登录名。 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 确认了 Windows 身份验证凭据或验证了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证凭据之后，该连接通常会尝试连接到用户数据库。 若要连接到某个用户数据库，登录名必须能够映射到（即关联）用户数据库中的某个数据库用户。 连接字符串还可以指定连接到特定数据库，该数据库在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中为可选但在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中为必需。  
  
 重要原则是登录名（在 master 数据库中）和用户（在用户数据库中）必须存在，并且彼此相关。 这意味着到用户数据库的连接依赖于 master 数据库中的登录名，并且这限制了将数据库移动到其他托管 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 服务器的功能。 而且，如果由于任何原因，到 master 数据库的连接不可用 (例如，故障转移正在进行中) ，整个连接时间将会增加，或者连接可能超时。因此，这可能会降低连接可伸缩性。  
  
## <a name="contained-database-user-model"></a>包含的数据库用户模型  
 在包含的数据库用户模型中，master 数据库中不存在登录名。 相反，身份验证过程发生在用户数据库中，并且用户数据库中的数据库用户在 master 数据库中没有关联的登录名。 包含的数据库用户模型支持 Windows 身份验证（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中）和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证（在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中）。 若要作为包含的数据库用户进行连接，连接字符串必须始终包含用户数据库的参数，以便 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 知道哪个数据库负责管理身份验证过程。 包含的数据库用户的活动仅限于验证数据库，因此当作为包含的数据库用户进行连接时，必须在用户将需要的每个数据库中独立创建数据库用户帐户。 若要更改数据库， [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 用户必须创建一个新的连接。 如果另一个数据库中存在相同的用户， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的包含的数据库用户可以更改数据库。  
  
 对于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，在从传统模型切换到包含的数据库用户模型时，无需更改连接字符串。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接，如果数据库名称尚不存在，它将必须添加到连接字符串。  
  
> [!IMPORTANT]  
>  在使用传统模型时，服务器级别角色和服务器级别权限可以限制对所有数据库的访问。 在使用包含的数据库模型时，数据库所有者和具有 ALTER ANY USER 权限的数据库用户可以授予对数据库的访问权限。 这将减少高特权服务器登录名的访问控制，并且使访问控制扩大至将高特权数据库用户包含在内。  
  
## <a name="firewalls"></a>防火墙  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Windows 防火墙规则适用于所有连接，并且对登录名（传统模型连接）和包含的数据库用户具有相同影响。 有关 Windows 防火墙的详细信息，请参阅 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。  
  
### <a name="sssds-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 防火墙  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 允许适用于服务器级别连接（登录名）和适用于数据库级别连接（包含的数据库用户）的单独防火墙规则。 连接到用户数据库时，会首先检查数据库防火墙规则。 如果没有允许访问数据库的规则，则检查服务器级别防火墙规则，这将需要对逻辑服务器 master 数据库的访问权限。 与包含的数据库用户相结合的数据库级别防火墙规则可以无需在连接过程中访问服务器的 master 数据库，从而提供改进的连接可伸缩性。  
  
 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 防火墙规则的详细信息，请参阅以下主题：  
  
-   [Azure SQL Database 防火墙](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [如何：配置防火墙设置（Azure SQL 数据库）](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule（Azure SQL 数据库）](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule（Azure SQL 数据库）](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>语法差异  
  
|传统模型|包含的数据库用户模型|  
|-----------------------|-----------------------------------|  
|连接到 master 数据库时：<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> 随后连接到用户数据库时：<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|连接到用户数据库时：<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|传统模型|包含的数据库用户模型|  
|-----------------------|-----------------------------------|  
|要更改密码，在 master 数据库的上下文中：<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|要更改密码，在用户数据库的上下文中：<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>备注  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例启用包含的数据库用户。 有关详细信息，请参阅 [contained database authentication Server Configuration Option](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)。  
  
-   具有非重叠名称的包含的数据库用户和登录名可以在应用程序中共存。  
  
-   如果 master 数据库中有一个名为 **name1** 的登录名，并且你创建一个名为 **name1**的包含的数据库用户，当在连接字符串中提供数据库名称时，将在连接到数据库的情况下提取登录上下文上的数据库用户上下文。 即，包含的数据库用户将优先使用具有相同名称的登录名。  
  
-   在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，包含的数据库用户的名称不能与服务器管理员帐户的名称相同。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器管理员帐户绝不能是包含的数据库用户。 服务器管理员具有足够的权限来创建和管理包含的数据库用户。 服务器管理员可以向包含的数据库用户授予针对用户数据库的权限。  
  
-   由于包含的数据库用户是数据库级别主体，因此需要在会使用它们的每个数据库中创建包含的数据库用户。 标识仅限于数据库，在所有方面都独立于同一台服务器上其他数据库中具有相同名称和相同密码的用户。  
  
-   使用你通常用于登录名的相同强度密码。  
  
## <a name="see-also"></a>另请参阅  
 [包含的数据库](../databases/contained-databases.md)   
 [针对包含数据库的安全性最佳方法](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER (Transact-SQL)](/sql/t-sql/statements/create-user-transact-sql)  
  
  
