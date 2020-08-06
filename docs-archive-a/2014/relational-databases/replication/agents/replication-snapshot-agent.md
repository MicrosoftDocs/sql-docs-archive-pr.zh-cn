---
title: 复制快照代理 | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, executables
- agents [SQL Server replication], Snapshot Agent
- command prompt [SQL Server replication]
- Snapshot Agent, parameter reference
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a26aca7b33a7355500350572ea5e8ed21bddeacb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578144"
---
# <a name="replication-snapshot-agent"></a>复制快照代理
  复制快照代理是一个可执行文件，用于准备快照文件（其中包含已发布表和数据库对象的架构及数据），然后将这些文件存储在快照文件夹中，并在分发数据库中记录同步作业。  
  
> [!NOTE]  
>  可以按任意顺序指定参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
      snapshot [ -?]   
-Publisherserver_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSizebcp_batch_size]  
[-DefinitionFiledef_path_and_file_name]  
[-Distributorserver_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostNamedynamic_filter_host_name]  
[-DynamicFilterLogindynamic_filter_login]  
[-DynamicSnapshotLocationdynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiterfield_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocksnumber_of_blocks ]  
[-HRBcpBlockSizeblock_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageIntervalkeep_alive_interval]  
[-LoginTimeOutlogin_time_out_seconds]  
[-MaxBcpThreadsnumber_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Outputoutput_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSizepacket_size]
[-PrefetchTables [0|1] ]  
[-ProfileNameprofile_name]  
[-PublisherDBpublisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-PublisherLoginpublisher_login]  
[-PublisherPasswordpublisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOutquery_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiterrow_delimiter]  
[-StartQueueTimeoutstart_queue_timeout_seconds]  
[-UsePerArticleContentsViewuse_per_article_contents_view]  
```  
  
## <a name="arguments"></a>参数  
 **-?**  
 输出所有可用的参数。  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 发布服务器的名称。 为该服务器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认实例指定 server_name。 为该服务器上的 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认实例指定 server_name。  
  
 **-Publication** _publication_  
 发布的名称。 只有将发布设置为总是使快照可用于新订阅或重新初始化的订阅时，此参数才有效。  
  
 **-70Subscribers**  
 如果有任何订阅服务器在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 版，则必须使用此参数。  
  
 **-BcpBatchSize** _bcp_\_ *batch*\_ *size*  
 在一次大容量复制操作中发送的行数。  执行 **bcp in** 操作时，批的大小为要作为一个事务发送到服务器的行数，并且也是分发代理记录 bcp 进度消息之前必须发送的行数。 当执行 **bcp out** 操作时，将使用固定批大小 1000。 值为 0 表示不记录任何消息。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 代理定义文件的路径。 代理定义文件中包含该代理的命令行参数。 文件的内容被当作可执行文件进行分析。 使用双引号 (") 指定包含任意字符的参数值。  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 分发服务器名称。 为该服务器上的 *默认实例指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 为该服务器上的 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认实例指定 server_name。  
  
 **-DistributorDeadlockPriority** [ **-1**|**0**|**1**]  
 死锁发生时快照代理连接到分发服务器的优先级。 指定此参数是为了解决快照生成期间在快照代理和用户应用程序之间发生的死锁问题。  
  
|DistributorDeadlockPriority 值|说明|  
|---------------------------------------|-----------------|  
|**-1**|在分发服务器上发生死锁时，应用程序而非快照代理优先。|  
|**0** （默认值）|未分配优先级。|  
|**1**|在分发服务器上发生死锁时，快照代理优先。|  
  
 **-DistributorLogin** _distributor_login_  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到分发服务器时所用的登录名。  
  
 **-DistributorPassword** _distributor_password_  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到分发服务器时使用的密码。 .  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定分发服务器的安全模式。 值 **0** 指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证模式（默认设置），值 **1** 指示 Windows 身份验证模式。  
  
 **-DynamicFilterHostName** _dynamic_filter_host_name_  
 在创建动态快照时，用来为筛选中的 [HOST_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/host-name-transact-sql) 设置值。 例如，如果为项目指定了子集筛选器子句 `rep_id = HOST_NAME()` ，并且在调用合并代理之前将 **DynamicFilterHostName** 属性设置为“FBJones”，则只会复制 **rep_id** 列中具有“FBJones”的行。  
  
 **-DynamicFilterLogin** _dynamic_filter_login_  
 在创建动态快照时，用来为筛选中的 [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql) 设置值。 例如，如果为项目指定了子集筛选器子句 `user_id = SUSER_SNAME()` ，并且在调用 **SQLSnapshot** 对象的 **Run** 方法之前将 **DynamicFilterLogin** 属性设置为“rsmith”，则只将 **user_id** 列中具有“rsmith”的行包括在快照中。  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 应生成动态快照的位置。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 建立连接时快照代理使用的安全套接字层 (SSL) 加密的等级。  
  
|EncryptionLevel 值|说明|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定使用 SSL，但是代理不验证 SSL 服务器证书是否已由可信的颁发者进行签名。|  
|**2**|指定使用 SSL，并验证证书。|  

 > [!NOTE]  
 >  使用 SQL Server 的完全限定的域名定义有效的 SSL 证书。 为了在将 -EncryptionLevel 设置为 2 时成功连接代理，请在本地 SQL Server 上创建别名。 “Alias Name”参数应为服务器名称，”Server”参数应设置为 SQL Server 的完全限定名称。
  
 有关详细信息，请参阅[SQL Server 复制安全性](../security/view-and-modify-replication-security-settings.md)。  
  
 **-FieldDelimiter** _field_delimiter_  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大容量复制数据文件中用于标记字段末尾的字符或字符序列。 默认值为 \n\<x$3>\n。  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 指定在快照操作过程中记录的历史记录大小。 选择 **1**可将历史日志记录对性能的影响减至最小。  
  
|HistoryVerboseLevel 值|说明|  
|-------------------------------|-----------------|  
|**0**|进度消息将写入控制台或输出文件。 不在分发数据库中记录历史记录。|  
|**1**|总是更新具有相同状态（启动、进行中、成功等）的上一历史记录消息。 如果不存在状态相同的上一记录，将插入新记录。|  
|**2** （默认值）|除非记录为空闲消息或长时间运行的作业消息等信息（此时将更新上一记录），否则插入新的历史记录。|  
|**3**|始终插入新记录，除非它与空闲消息有关。|  
  
 **-HRBcpBlocks** _number_of_blocks_  
 在编写器线程和读取器线程之间排队的 **bcp** 数据块的数量。 默认值为 50。 **HRBcpBlocks** 仅用于 Oracle 发布。  
  
> [!NOTE]  
>  此参数用于通过 Oracle 发布服务器优化 **bcp** 的性能。  
  
 -**HRBcpBlockSize**_block_size_  
 每个 **bcp** 数据块的大小（以 KB 为单位）。 默认值为 64 KB。 **HRBcpBlocks** 仅用于 Oracle 发布。  
  
> [!NOTE]  
>  此参数用于通过 Oracle 发布服务器优化 **bcp** 的性能。  
  
 **-HRBcpDynamicBlocks**  
 每个 **bcp** 数据块的大小是否可以动态增长。 **HRBcpBlocks** 仅用于 Oracle 发布。  
  
> [!NOTE]  
>  此参数用于通过 Oracle 发布服务器优化 **bcp** 的性能。  
  
 **-KeepAliveMessageInterval** _keep_alive_interval_  
 快照代理在向 [MSsnapshot_history](/sql/relational-databases/system-tables/mssnapshot-history-transact-sql) 表中记录“waiting for backend message”之前等待的时间（以秒为单位）。 默认值为 300 秒。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 登录超时前等待的秒数。 默认值为 15 秒。  
  
 **-MaxBcpThreads** _number_of_threads_  
 指定可以并行执行的大容量复制操作的数量。 同时存在的线程和 ODBC 连接的最大数量为 **MaxBcpThreads** 或显示在分发数据库中同步事务中的大容量复制请求数中较小的那一个。 **MaxBcpThreads** 的值必须大于 **0** ，并且不存在任何硬编码的上限。 默认值为 **1**。  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 是否将无关删除操作发送到订阅服务器。 无关删除操作是针对不属于订阅服务器分区的行发送到订阅服务器的 DELETE 命令。 无关删除操作不会影响数据的完整性或收敛，但它们会导致不必要的网络通信。 **MaxNetworkOptimization** 的默认值是 **0**。 将 **MaxNetworkOptimization** 设置为 **1** 可将不相关的删除操作发生的机会减至最小，从而减少网络通信，并最大程度地优化网络。 如果存在多个级别的联接筛选器和复杂子集筛选器，则将此参数设置为 **1** 还会增加元数据的存储并导致发布服务器性能下降。 您应仔细评估您的复制拓扑，仅当无关删除操作导致的网络通信高到无法接受时才应将 **MaxNetworkOptimization** 设置为 **1** 。  
  
> [!NOTE]
>  仅当合并发布的同步优化选项设置为**true**时，才会将此参数设置为**1** ，这 (**@keep_partition_changes** [sp_addmergepublication &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)) 的参数。  
  
 **-Output** _output_path_and_file_name_  
 代理输出文件的路径。 如果未提供文件名，则向控制台发送该输出。 如果指定的文件名已存在，会将输出追加到该文件。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定输出是否应提供详细内容。  
  
|OutputVerboseLevel 值|说明|  
|------------------------------|-----------------|  
|**0**|仅输出错误消息。|  
|**1** （默认值）|输出所有进度报告消息（默认值）。|  
|**2**|输出所有错误消息和进度报告消息，这对于调试很有用。|  

 **-PrefetchTables** [ **0**| **1**]  
 可选参数，指定是否预提取并缓存表对象。  默认行为是，根据内部计算结果，使用 SMO 组件来预提取特定表属性。  如果 SMO 预提取操作的耗时相当长，你会发现此参数非常有用。 如果你不使用此参数，此决定是在运行时做出，依据为以项目形式添加到发布中的表所占的百分比。  
  
|OutputVerboseLevel 值|说明|  
|------------------------------|-----------------|  
|**0**|禁止调用 SMO 组件的预提取方法。|  
|**1**|快照代理会调用预提取方法，以使用 SMO 缓存一些表属性|  
  
 **-PacketSize** _packet_size_  
 快照代理连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时使用的数据包大小（以字节为单位）。 默认值为 8192 字节。  
  
> [!NOTE]  
>  除非您确信能够提高性能，否则不要更改数据包的大小。 对于大多数应用程序而言，默认数据包大小为最佳数值。  
  
 **-ProfileName** _profile_name_  
 指定用于代理参数的代理配置文件。 如果 **ProfileName** 为 NULL，则将禁用代理配置文件。 如果未指定 **ProfileName** ，则使用该代理类型的默认配置文件。 有关信息，请参阅[复制代理配置文件](replication-agent-profiles.md)。  
  
 **-PublisherDB** _publisher_database_  
 发布数据库的名称。 Oracle 发布服务器不支持该参数。  
  
 **-PublisherDeadlockPriority** [ **-1**|**0**|**1**]  
 死锁发生时快照代理连接到发布服务器的优先级。 指定此参数是为了解决快照生成期间在快照代理和用户应用程序之间发生的死锁问题。  
  
|PublisherDeadlockPriority 值|说明|  
|-------------------------------------|-----------------|  
|**-1**|在发布服务器上发生死锁时，应用程序而非快照代理优先。|  
|**0** （默认值）|未分配优先级。|  
|**1**|在发布服务器上发生死锁时，快照代理优先。|  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 指定参加与发布数据库进行的数据库镜像会话的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移伙伴实例。 有关详细信息，请参阅 [数据库镜像和复制 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherLogin** _publisher_login_  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器时所用的登录名。  
  
 **-PublisherPassword** _publisher_password_  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证连接到发布服务器时使用的密码。 .  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 指定发布服务器的安全模式。 值 **0** 指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证（默认值），值 **1** 指示 Windows 身份验证模式。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 查询超时前等待的秒数。默认值为 1800 秒。  
  
 **-ReplicationType** [ **1**| **2**]  
 指定复制的类型。 值 **1** 指示事务复制，值 **2** 指示合并复制。  
  
 **-RowDelimiter** _row_delimiter_  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大容量复制数据文件中用于标记行尾的字符或字符序列。 默认值为 \n\<,@g>\n。  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 当运行的并发动态快照进程数达到 **@max_concurrent_dynamic_snapshots** [&#40;transact-sql&#41;的 sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)属性设置的限制时，快照代理等待的最大秒数。 如果在经过最大秒数之后快照代理仍在等待，快照代理将退出。 值 0 表示代理将无限期地等待，尽管可以将其取消。  
  
 \- **UsePerArticleContentsView** _use_per_article_contents_view_  
 已不推荐使用此参数，支持它是为了能够向后兼容。  
  
## <a name="remarks"></a>备注  
  
> [!IMPORTANT]  
>  如果您安装的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理是通过本地系统帐户而非域用户帐户（默认值）运行，则该服务仅可访问本地计算机。 如果将在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理下运行的快照代理配置为登录 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时使用 Windows 身份验证模式，则快照代理将失败。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 默认设置为  身份验证。  
  
 若要启动快照代理，请从命令提示符处执行 **snapshot.exe** 。 有关信息，请参阅 [复制代理可执行文件](../concepts/replication-agent-executables-concepts.md)。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理管理](replication-agent-administration.md)  
  
  
