---
title: 标识和访问控制（复制）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ae16d0908efa211a773b278fc8e86b1bf1966d7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689858"
---
# <a name="identity-and-access-control-replication"></a>标识和访问控制（复制）
  身份验证是指一个实体（在此上下文中通常是计算机）验证另一实体（也称“主体”  ，通常是另一计算机或用户）是否与其自称的身份相符的过程。 授权是给予通过身份验证的主体对资源（例如，文件系统中的文件或数据库中的表）的访问权限的过程。  
  
 复制安全性使用身份验证和授权，来控制对复制数据库对象和涉及复制处理的计算机及代理的访问。 这是通过三种机制实现的：  
  
-   代理安全性：通过复制代理安全模式，可以对运行复制代理和建立连接所用的帐户进行精细的控制。 有关代理安全模式的详细信息，请参阅 [Replication Agent Security Model](replication-agent-security-model.md)。 有关为代理设置登录名和密码的信息，请参阅[管理复制中的登录名和密码](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)。  
  
-   管理角色：确保使用正确的服务器和数据库角色进行复制设置、维护和处理。 有关详细信息，请参阅 [Security Role Requirements for Replication](security-role-requirements-for-replication.md)。  
  
-   发布访问列表 (PAL) ：通过 PAL 授予对发布的访问权限。 PAL 的功能与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 的访问控制列表相似。 当有订阅服务器连接到发布服务器或分发服务器并请求访问发布时，将对照 PAL 检查代理传递的身份验证信息。 有关 PAL 的详细信息和最佳做法，请参阅[保护发布服务器](secure-the-publisher.md)。  
  
## <a name="filtering-published-data"></a>筛选已发布数据  
 除了使用身份验证和授权来控制对被复制的数据和对象的访问之外，复制还包含两个选项，用来控制订阅服务器上哪些数据可用：列筛选和行筛选。 有关筛选的详细信息，请参阅[筛选已发布数据](../publish/filter-published-data.md)。  
  
 定义项目时，可以只发布那些发布所必需的列，而省略那些不必要或包含敏感数据的行。 例如，从 Adventure Works 数据库向现场销售代表发布 **Customer** 表时，可以省略 **AnnualSales** 列，该列可能仅与公司的高层管理者有关。  
  
 通过筛选已发布数据，可以限制对数据的访问，并可指定订阅服务器上的可用数据。 例如，可以筛选 **Customer** 表，以使公司合作伙伴们只收到其 **ShareInfo** 列的值为“yes”的客户的信息。 对于合并复制，如果使用包括 HOST_NAME() 的参数化筛选器，则需要考虑安全问题。 有关详细信息，请参阅 [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md)中“使用 HOST_NAME() 筛选”部分。  

## <a name="manage-logins-and-passwords-in-replication"></a>管理复制中的登录名和密码
  在配置复制时，为复制代理指定登录名和密码。 配置复制后，可以更改登录名和密码。 有关详细信息，请参阅 [View and Modify Replication Security Settings](view-and-modify-replication-security-settings.md)。 若要更改复制代理所使用的帐户的密码，请执行 [sp_changereplicationserverpasswords (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理安全模式](replication-agent-security-model.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server 复制安全性](view-and-modify-replication-security-settings.md)   
 [复制威胁和漏洞缓解](threat-and-vulnerability-mitigation-replication.md)   

  
  
