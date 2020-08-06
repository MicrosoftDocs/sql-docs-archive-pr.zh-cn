---
title: 数据库引擎服务启动选项 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], startup option
- overriding default startup options
- minimal configuration mode [SQL Server], startup option
- default startup options
- temporarily override default startup options [SQL Server]
- startup options [SQL Server]
- starting SQL Server, options
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 844c0813453d371ed204dff6f8976f08bad63fe5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588020"
---
# <a name="database-engine-service-startup-options"></a>数据库引擎服务启动选项
  启动选项指定在启动期间所需的某些文件位置，并指定一些服务器范围的条件。 大多数用户不需要指定启动选项，除非您在排除 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 故障或者具有不常见问题，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户支持指示使用启动选项。  
  
> [!WARNING]  
>  错误地使用启动选项可能会影响服务器性能并且可能阻止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动。  
  
## <a name="about-startup-options"></a>关于启动选项  
 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，安装程序会将一组默认的启动选项写入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 注册表。 可以使用这些启动选项指定备用的 master 数据库文件、master 数据库日志文件或错误日志文件。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 找不到所需文件， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将不启动。  
  
 可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器设置启动选项。 有关信息，请参阅[配置服务器启动选项 (SQL Server Configuration Manager)](scm-services-configure-server-startup-options.md)。  
  
## <a name="list-of-startup-options"></a>启动选项列表  
  
|默认启动选项|说明|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|是 master 数据库文件的完全限定路径（通常为：C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf）。 如果没有提供此选项，则使用现有的注册表参数。|  
|**-e**  *error_log_path*|是错误日志文件的完全限定路径（通常为 C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG）。 如果没有提供此选项，则使用现有的注册表参数。|  
|**-l**  *master_log_path*|是 master 数据库日志文件的完全限定路径（通常为：C:\Program Files\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf）。 如果没有指定此选项，则使用现有的注册表参数。|  
  
|其他启动选项|说明|  
|---------------------------|-----------------|  
|**-c**|缩短从命令提示符启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时的启动时间。 通常， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 通过调用服务控制管理器作为服务启动。 由于在通过命令提示符启动时 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 不作为服务启动，因此请使用 **-c** 跳过此步骤。|  
|**-f**|以最小配置启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 在配置值的设置（例如，过度分配内存）妨碍服务器启动时，这非常有用。 在最低配置模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 置于单用户模式。 有关详细信息，请参阅下面的 **-m** 说明。|  
|**-g**  *memory_to_reserve*|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程之内但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存池之外分配内存而保留的内存整数量 (MB)。 内存池以外的内存是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于加载诸如下列项目的区域：扩展过程 .dll 文件、分布式查询引用的 OLE DB 提供程序以及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中引用的自动化对象。 默认值为 256 MB。<br /><br /> 使用此选项可帮助优化内存分配，但仅限于物理内存超过操作系统设置的应用程序可用虚拟内存配置限制时。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内存使用要求异乎寻常，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的虚拟地址空间都在使用，则对于这样的大内存配置适合使用此选项。 对此选项的不当使用会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例无法启动或遇到运行时错误。<br /><br /> 除非你在 **错误日志中看到下列任何警告，否则请使用** -g [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 参数的默认值：<br /><br /> -"虚拟分配字节失败： FAIL_VIRTUAL_RESERVE \<size> "<br /><br /> -"虚拟分配字节失败： FAIL_VIRTUAL_COMMIT \<size> "<br /><br /> 这些消息可能指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正试图释放部分 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存池空间，以便为扩展存储过程 .dll 文件或自动化对象等项目找到空间。 在这种情况下，可以考虑增加由 **-g** 开关保留的内存量。<br /><br /> 使用小于默认值的值将增加 SQL Server 内存管理器所管理的内存池和线程栈中的可用内存量；而在不使用很多扩展存储过程、分布式查询或自动化对象的系统中，这种方法可改善需要大量内存的工作负荷的性能。|  
|**-m**|在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，只能连接一个用户，并且不启动 CHECKPOINT 进程。 CHECKPOINT 保证将已完成的事务定期从磁盘缓存写入数据库设备。 （通常，在遇到需要修复的系统数据库问题时使用此选项。）启用 sp_configure allow updates 选项。 默认情况下，allow updates 处于禁用状态。 在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可使计算机本地 Administrators 组的任何成员作为 sysadmin 固定服务器角色的成员连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 有关详细信息，请参阅 [在系统管理员被锁定时连接到 SQL Server](connect-to-sql-server-when-system-administrators-are-locked-out.md)。有关单用户模式的详细信息，请参阅 [在单用户模式下启动 SQL Server](start-sql-server-in-single-user-mode.md)。|  
|**-m "客户端应用程序名称"**|当你将 **-m** 选项与 **SQLCMD** 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 结合使用时，限制对指定的客户端应用程序的连接。 例如，-m"sqlcmd" 将连接限制为单个连接，并且该连接必须将自身标识为 SQLCMD 客户端程序。 当您正在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且未知的客户端应用程序正在占用这个唯一的可用连接时，使用此选项。 若要通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器进行连接，请使用 **-m"Microsoft SQL Server Management Studio - Query"** 。<br /><br /> 客户端应用程序名称区分大小写。<br /><br /> ** \* \* 安全 \* 说明 \* **请勿将此选项作为安全功能使用。 客户端应用程序提供客户端应用程序名称，并且提供假名称来作为连接字符串的一部分。|  
|**-n**|不要使用 Windows 应用程序日志来记录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 如果你使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -n **启动**实例，我们建议你同时使用 **-e** 启动选项。 否则，将不会记录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。|  
|**-s**|用于启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的命名实例。 如果 **-s** 参数未设置，则系统会尝试启动默认实例。 必须先在命令提示符处切换到实例的相应 BINN 目录，然后才能启动 **sqlservr.exe**。 例如，如果 Instance1 为其二进制文件使用了 \mssql$Instance1，则用户必须位于 \mssql$Instance1\binn 目录中才能启动 **sqlservr.exe -s instance1**。|  
|**-T**  *trace#*|指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启动时，指定的跟踪标志 (*trace#* ) 应同时生效。 跟踪标记用于以非标准行为启动服务器。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)。<br /><br /> ** \* \* 重要 \* 说明 \* **在使用 **-T**选项指定跟踪标志时，请使用大写 "T" 来传递跟踪标志号。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也可接受小写“t”，只是它用于设置仅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持工程师才需要的其他内部跟踪标志。 （不读取“控制面板”启动窗口中指定的参数。）|  
|**-x**|禁用下列监视功能：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能监视器计数器<br /><br /> 保留 CPU 时间和高速缓存命中率统计信息<br /><br /> 收集 DBCC SQLPERF 命令的信息<br /><br /> 收集某些动态管理视图的信息<br /><br /> 许多扩展事件事件点<br /><br /> <br /><br /> ** \* \* 警告 \* ： \* **使用 **-x**启动选项时，可让你诊断的性能和功能问题的信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 大大减少。|  
|**-E**|增加为文件组中的每个文件分配的区数。 对于那些运行索引或数据扫描的用户数量受到限制的数据仓库应用程序，此选项可能十分有用。 不应在其他应用程序中使用此选项，因为它可能降低性能。 32 位版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持此选项。|  
  
## <a name="using-startup-options-for-troubleshooting"></a>使用启动选项进行故障排除  
 某些启动选项（如单用户模式和最低配置模式）主要在故障排除过程中使用。 使用“-m”或“-f”选项启动服务器进行故障排除的最简单方法是使用命令行，同时还能手动启动 sqlservr.exe 。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net start **启动**时，启动选项使用的是左斜线 (/)，而不是连字符 (-)。  
  
## <a name="using-startup-options-during-normal-operations"></a>在正常操作中使用启动选项  
 最好在每次启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时使用某些启动选项。 完成这些选项（如“-g”或用跟踪标志启动）的最简单方法是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器来配置启动参数****。 这些工具将启动选项保存为注册表项，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将始终用这些启动选项来启动。  
  
## <a name="compatibility-support"></a>兼容性支持  
 **不支持**  -h [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]参数。 启用 AWE 时，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本的 32 位实例使用此参数以便为热添加内存元数据保留虚拟内存地址空间。 有关详细信息，请参阅 [SQL Server 2014 中不再使用的 SQL Server 功能](../../getting-started/discontinued-sql-server-features-in-sql-server-2014.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [配置 scan for startup procs 服务器配置选项](configure-the-scan-for-startup-procs-server-configuration-option.md)  
  
 [启动、停止、暂停、继续、重新启动数据库引擎、SQL Server 代理或 SQL Server Browser 服务](start-stop-pause-resume-restart-sql-server-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [检查点 (Transact-SQL)](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [sqlservr Application](../../tools/sqlservr-application.md)  
  
  
