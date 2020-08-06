---
title: 通过 FTP 传递快照 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2e6700e6989a5a7e32202a0710bc663978a136cf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578809"
---
# <a name="deliver-a-snapshot-through-ftp"></a>通过 FTP 传递快照
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中通过 FTP 传递快照。  
  
##  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，就必须指定一个共享目录作为通用命名约定 (UNC) 路径，例如 \\\ftpserver\home\snapshots。 有关详细信息，请参阅[保护快照文件夹](../security/secure-the-snapshot-folder.md)。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   若要通过文件传输协议 (FTP) 传输快照文件，必须先配置一个 FTP 服务器。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 文档。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 为了帮助改进安全性，建议您在通过 Internet 使用 FTP 快照传递时实现虚拟专用网络 (VPN)。 有关详细信息，请参阅[使用 VPN 通过 Internet 发布数据](../publish-data-over-the-internet-using-vpn.md)。  
  
 出于安全考虑，最好不允许匿名登录 FTP 服务器。 快照代理必须对指定的目录具有写权限，而分发代理或合并代理必须具有读权限。 如果使用请求订阅，就必须指定一个共享目录作为通用命名约定 (UNC) 路径，例如 \\\ftpserver\home\snapshots。 有关详细信息，请参阅[保护快照文件夹](../security/secure-the-snapshot-folder.md)。  
  
 如果可能，请在运行时提示用户输入其凭据。 如果将凭据存储在脚本文件中，则必须确保此文件的安全。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 配置 FTP 服务器后，请在“发布属性 \<Publication>”对话框中为该服务器指定目录和安全信息。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-ftp-information"></a>指定 FTP 信息  
  
1.  在“发布属性 - \<Publication>”对话框中，从以下任一页面选择“允许订阅服务器下载使用 FTP 的快照文件”：    
    -   “FTP 快照”页面，用于运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前版本的发布服务器的快照发布、事务发布以及合并发布。    
    -   **“FTP 快照和 Internet”** 页，用于运行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本的发布服务器的合并发布。    
2.  为 **“FTP 服务器名称”** 、 **“端口号”** 、 **“从 FTP 根文件夹开始的路径”** 、 **“登录名”** 和 **“密码”** 指定值。    
     例如，如果 FTP 服务器的根目录是 \\\ftpserver\home，但你想将快照存储在 \\\ftpserver\home\snapshots，请为“从 FTP 根文件夹开始的路径”属性指定 \snapshots\ftp（复制在创建快照文件时将“ftp”追加到快照文件夹路径）。    
3.  指定快照代理应将快照文件写入在步骤 2 中指定的目录。 例如，若要让快照代理将快照文件写入 \\\ftpserver\home\snapshots\ftp，必须在下面两个位置之一指定路径 \\\ftpserver\home\snapshots：    
    -   与发布关联的分发服务器的默认快照位置。    
         有关指定默认快照位置的详细信息，请参阅[指定默认快照位置](../snapshot-options.md#snapshot-folder-locations)。    
    -   发布的备用快照文件夹位置。 如果压缩快照，则需要指定备用位置。    
         在 "**发布属性- \<Publication> ** " 对话框的 "快照" 页上的 "**将文件放入下列文件夹**" 文本框中输入路径。   
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 通过使用复制存储过程，可以按编程方式设置在 FTP 服务器上提供快照文件的选项以及修改这些 FTP 设置。 所用的过程由发布的类型决定。 FTP 快照传递仅可同请求订阅一起使用。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>为快照发布或事务发布启用 FTP 快照传递  
  
1.  在发布服务器上，对发布数据库执行 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 **@publication**将、的值指定 `true` 为 **@enabled_for_internet** ，并为以下参数指定适当的值：    
    -   **@ftp_address**-用于传递快照的 FTP 服务器的地址。    
    -    (可选) **@ftp_port** -FTP 服务器所使用的端口。    
    -    (可选) **@ftp_subdirectory** -分配给 FTP 登录名的默认 FTP 目录的子目录。 例如，如果 FTP 服务器根目录为 \ftpserver\home， \\ 并且你希望快照存储在 \\ \ftpserver\home\snapshots 中，则**\snapshots\ftp** **@ftp_subdirectory** 在创建快照文件) 时，指定 \snapshots\ftp for (复制会将 "FTP" 追加到快照文件夹路径中。    
    -    (可选) **@ftp_login** -连接到 FTP 服务器时使用的登录帐户。    
    -    (可选) **@ftp_password** -FTP 登录名的密码。  
  
     此操作将创建一个使用 FTP 的发布。 有关详细信息，请参阅 [Create a Publication](create-a-publication.md)。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>为合并发布启用 FTP 快照传递  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 为 **@publication** 以下参数指定值，并为其指定 `true` **@enabled_for_internet** 适当的值：  
  
    -   **@ftp_address**-用于传递快照的 FTP 服务器的地址。    
    -    (可选) **@ftp_port** -FTP 服务器所使用的端口。    
    -    (可选) **@ftp_subdirectory** -分配给 FTP 登录名的默认 FTP 目录的子目录。 例如，如果 FTP 服务器根目录为 \ftpserver\home， \\ 并且你希望快照存储在 \\ \ftpserver\home\snapshots 中，则**\snapshots\ftp** **@ftp_subdirectory** 在创建快照文件) 时，指定 \snapshots\ftp for (复制会将 "FTP" 追加到快照文件夹路径中。    
    -    (可选) **@ftp_login** -连接到 FTP 服务器时使用的登录帐户。    
    -    (可选) **@ftp_password** -FTP 登录名的密码。  
  
     此操作将创建一个使用 FTP 的发布。 有关详细信息，请参阅 [Create a Publication](create-a-publication.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>创建对使用 FTP 快照传递的快照发布或事务发布的请求订阅  
  
1.  在订阅服务器上，对订阅数据库执行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)。 指定 **@publisher** 和 **@publication** 。  
  
    -   在订阅服务器上，对订阅数据库执行 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 、在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 其下运行订阅服务器分发代理的 Windows 凭据 **@job_login** ，并为指定和 **@job_password** 值 `true` **@use_ftp** 。  
  
2.  在发布服务器上，对发布数据库执行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 以注册请求订阅。 有关详细信息，请参阅 [创建请求订阅](../create-a-pull-subscription.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>创建对使用 FTP 快照传递的合并发布的请求订阅  
  
1.  在订阅服务器上，对订阅数据库执行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)。 指定 **@publisher** 和 **@publication** 。   
2.  在订阅服务器上，对订阅数据库执行 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 、在其下运行订阅服务器分发代理的 Windows 凭据 **@job_login** ，并为指定和 **@job_password** 值 `true` **@use_ftp** 。    
3.  在发布服务器上，对发布数据库执行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) 以注册请求订阅。 有关详细信息，请参阅 [创建请求订阅](../create-a-pull-subscription.md)。  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>为快照发布或事务发布更改一个或多个 FTP 快照传递设置  
  
1.  在发布服务器上，对发布数据库执行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 为指定以下值之一 **@property** ，并为此设置指定新值 **@value** ：    
    -   `ftp_address` - 用于传递快照的 FTP 服务器的地址。    
    -   `ftp_port` - FTP 服务器所使用的端口。    
    -   `ftp_subdirectory` - 用于 FTP 快照的默认 FTP 目录的子目录。    
    -   `ftp_login` - 用于连接到 FTP 服务器的登录名。    
    -   `ftp_password` - FTP 登录名的密码。  
  
2.  （可选）对更改的每个 FTP 设置重复步骤 1。    
3.  （可选）若要禁用 FTP 快照传递，请在发布服务器上对发布数据库执行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) 。 将的值指定 `enabled_for_internet` 为 **@property** ，并将的值指定 `false` 为 **@value** 。  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>为合并发布更改 FTP 快照传递的设置  
  
1.  在发布服务器上，对发布数据库执行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 为指定以下值之一 **@property** ，并为此设置指定新值 **@value** ：  
  
    -   `ftp_address` - 用于传递快照的 FTP 服务器的地址。    
    -   `ftp_port` - FTP 服务器所使用的端口。    
    -   `ftp_subdirectory` - 用于 FTP 快照的默认 FTP 目录的子目录。   
    -   `ftp_login` - 用于连接到 FTP 服务器的登录名。    
    -   `ftp_password` - FTP 登录名的密码。    
2.  （可选）对更改的每个 FTP 设置重复步骤 1。    
3.  （可选）若要禁用 FTP 快照传递，请在发布服务器上对发布数据库执行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) 。 将的值指定 `enabled_for_internet` 为 **@property** ，并将的值指定 `false` 为 **@value** 。  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例创建一个合并发布，该发布允许订阅服务器通过使用 FTP 访问快照数据。 访问 FTP 共享区时，订阅服务器应使用安全的 VPN 连接。 **sqlcmd** 脚本变量用于提供登录名和密码值。 有关详细信息，请参阅[将 sqlcmd 与脚本变量结合使用](../../scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 下面的示例创建一个对合并发布的订阅，在该订阅中订阅服务器通过使用 FTP 来获取快照。 访问 FTP 共享区时，订阅服务器应使用安全的 VPN 连接。 **sqlcmd** 脚本变量用于提供登录名和密码值。 有关详细信息，请参阅[将 sqlcmd 与脚本变量结合使用](../../scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>另请参阅  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [通过 FTP 传输快照](../transfer-snapshots-through-ftp.md)   
 [更改发布和项目属性](change-publication-and-article-properties.md)   
 [使用快照初始化订阅](../initialize-a-subscription-with-a-snapshot.md)  
  
  
