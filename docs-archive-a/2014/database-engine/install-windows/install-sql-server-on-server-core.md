---
title: 在 Server Core 上安装 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2614c43bb763757db7db46b1c7a966221da96f7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688187"
---
# <a name="install-sql-server-2014-on-server-core"></a>在 Server Core 上安装 SQL Server 2014
  您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安装上安装 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]。 本主题提供用于在 Server Core 上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的特定于安装的详细信息。  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 操作系统的 Server Core 安装选项提供了用于运行特定服务器角色的最小环境。 这将有助于减少维护和管理需求以及针对这些服务器角色的攻击面。 有关在上实施的服务器核心的详细信息 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] ，请参阅[server Core For Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=202439) (https://go.microsoft.com/fwlink/?LinkId=202439) 。 有关在 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]上实现 Server Core 的详细信息，请参阅 [Server Core for Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx) 。  
  
## <a name="prerequisites"></a>先决条件  
  
|要求|如何安装|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|包含在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 Server Core 安装中。 如果未启用，则安装程序将在默认情况下启用它。<br /><br /> 无法在计算机上并行运行 2.0、3.0 和 3.5 版。 在安装 .NET Framework 3.5 SP1 时，将自动获得 2.0 和 3.0 层。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 完整配置文件|包含在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 的 Server Core 安装中。 如果未启用，则安装程序将在默认情况下启用它。<br /><br /> 在安装有 Windows Server 操作系统的计算机上，您必须在运行安装程序前下载并安装 .NET Framework 3.5 SP1，以便安装依赖于 .NET 3.5 SP1 的组件。<br /><br /> 有关如何在中获取和启用 .NET Framework 3.5 的建议和指南的详细信息 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] ，请参阅 ([Microsoft .NET Framework 3.5 部署注意事项](https://msdn.microsoft.com/library/windows/hardware/hh975396) https://msdn.microsoft.com/library/windows/hardware/hh975396) 。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core 配置文件|除 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之外，所有 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]版本的安装程序均将 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core 配置文件作为必备组件进行安装。<br /><br /> 对于 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] ，请 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 从[Microsoft .NET Framework 4 (独立安装程序) ](https://www.microsoft.com/download/details.aspx?id=17718)中下载 4 server core 配置文件以获取服务器核心 (https://www.microsoft.com/download/details.aspx?id=17718) ，并在继续安装之前安装它。|  
|Windows Installer 4.5|随 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 Server Core 一同提供。|  
|Windows PowerShell 2.0|随 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 和 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 Server Core 一同提供。|  
  
##  <a name="supported-features"></a><a name="BK_SupportedFeatures"></a>支持的功能  
 使用下表可以查找 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 和 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安装上的 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]所支持的功能。  
  
|Feature|支持|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务|是|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication|是|  
|全文搜索|是|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|是|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|否|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|否|  
|客户端工具连接|是|  
|Integration Services Server<sup>[1]</sup>|是|  
|客户端工具向后兼容性|否|  
|客户端工具 SDK|否|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书|否|  
|管理工具 - 基本|仅限远程<sup>[2]</sup>|  
|管理工具 - 完整|仅限远程<sup>[2]</sup>|  
|Distributed Replay 控制器|否|  
|Distributed Replay 客户端|仅限远程<sup>[2]</sup>|  
|SQL 客户端连接 SDK|是|  
|Microsoft Sync Framework|是<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|否|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|否|  
  
 <sup>[1]</sup>有关中新 Integration Services 服务器及其功能的详细信息 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，请参阅[INTEGRATION SERVICES &#40;SSIS&#41; 服务器](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md)。  
  
 <sup>[2]</sup>不支持在 Server Core 上安装这些功能。 可以在 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 之外的服务器上安装这些组件，然后将这些组件连接到 Server Core 上安装的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服务。  
  
 <sup>[3]</sup>Microsoft Sync Framework 未包含在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装包中。 你可以从该[Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkId=221788) (页面下载适当版本的 Sync Framework https://go.microsoft.com/fwlink/?LinkId=221788) ，并将其安装在运行 SP1 或的 Server Core 安装的计算机上 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 。  
  
## <a name="supported-scenario-matrix"></a>支持的方案矩阵  
 下表显示在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安装上安装 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]时支持的方案矩阵。  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|所有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位版本<sup>[1]</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言|所有语言|  
|操作系统语言/区域设置（组合）上的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语言|JPN（日语）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> GER（德语）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> CHS（中文 - 中国）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ARA（阿拉伯语 (SA)）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> THA（泰语）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> TRK（土耳其语）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> pt-PT（葡萄牙语 - 葡萄牙）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ENG（英语）Windows 上的 ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Windows 版本|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位 x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位 x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位 x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位 x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位 x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位 x64 Web Server Core|  
  
 <sup>[1]</sup>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]不支持在 Server Core 上安装版本32位版本。  
  
## <a name="upgrading"></a>正在升级  
 在 Server Core 安装上，支持从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
## <a name="installation"></a>安装  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持在 Server Core 操作系统上使用安装向导进行安装。 在 Server Core 上进行安装时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序支持完全静默模式（通过使用 /Q 参数）或简单静默模式（通过使用 /QS 参数）。 有关详细信息，请参阅 [从命令提示符安装 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不能在运行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 的计算机上与早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起并行安装。  
  
 无论使用哪种安装方法，您都需要作为个人或代表实体确认接受软件许可条款，除非您对于软件的使用受单独的协议（如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 批量许可协议或与 ISV 或 OEM 之间的第三方协议）管辖。  
  
 将在安装程序用户界面中显示许可条款，供您审核审阅和接受。 使用 /Q 或 /QS 参数进行无人参与安装时，必须包含 /IACCEPTSQLSERVERLICENSETERMS 参数。 可以通过 [Microsoft Software License Terms](https://go.microsoft.com/fwlink/?LinkId=148209)（Microsoft 软件许可条款）单独查看许可条款。  
  
> [!NOTE]  
>  根据您接收软件的方式（例如，通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 批量许可），您对软件的使用可能受其他条款和条件约束。  
  
 若要安装特定功能，请使用 /FEATURES 参数并指定父功能或功能值。 有关功能参数及其用法的详细信息，请参阅以下部分。  
  
### <a name="feature-parameters"></a>功能参数  
  
|功能参数|说明|  
|-----------------------|-----------------|  
|SQLENGINE|仅安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。|  
|复制|将复制组件与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]一起安装。|  
|FULLTEXT|将全文组件与 [!INCLUDE[ssDE](../../includes/ssde-md.md)]一起安装。|  
|AS|安装所有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 组件。|  
|IS|安装所有的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 组件。|  
|CONN|安装连接组件。|  
  
 请参阅以下的功能参数用法示例：  
  
|参数和值|说明|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|仅安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。|  
|/FEATURES=SQLEngine,FullText|安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和全文组件。|  
|/FEATURES=SQLEngine,Conn|安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和连接组件。|  
|/FEATURES=SQLEngine,AS,IS,Conn|安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和连接组件。|  
  
### <a name="installation-options"></a>安装选项  
 在 Server Core 操作系统上安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 时，安装程序支持以下安装选项：  
  
1.  **从命令行安装**  
  
     若要使用命令提示符安装选项安装特定功能，请使用 /FEATURES 参数并指定父功能或功能值。 以下是在命令行中使用参数的示例：  
  
    ```cmd
    setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **使用配置文件安装**  
  
     安装程序仅支持通过命令提示符使用配置文件。 配置文件是具有基本参数结构（名称/值对）和说明性注释的文本文件。 在命令提示符处指定的配置文件应该具有 .INI 文件扩展名。 请参阅以下 ConfigurationFile.INI 示例：  
  
    -   安装 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
         以下示例说明了如何安装包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 的新的独立实例：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"
        ```  
  
    -   安装连接组件  
  
         以下示例说明如何安装连接组件：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True
        ```  
  
    -   安装所有支持的功能  
  
         以下示例说明如何在 Server Core 上安装所有支持的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能：  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     以下示例介绍了如何使用配置文件启动安装程序。  
  
    -   配置文件  
  
         以下是有关如何使用配置文件的一些示例：  
  
        -   在命令提示符处指定配置文件：  
  
        ```cmd
        setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   在命令提示符处而不是配置文件中指定密码：  
  
        ```cmd
        setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源媒体的根级别的 \x86 和 \x64 文件夹中包含 DefaultSetup.ini 文件，请打开该 DefaultSetup.ini 文件，然后将 *Features* 参数添加到该文件中。  
  
         如果 DefaultSetup.ini 文件不存在，您可以创建该文件并将其复制到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源介质根级别的 \x86 和 \x64 文件夹中。  
  
## <a name="configuring-remote-access-of-ssnoversion-running-on-server-core"></a>配置运行在 Server Core 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的远程访问  
 执行下述操作以配置运行在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安装上的 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]实例的远程访问。  
  
### <a name="enable-remote-connections-on-the-instance-of-ssnoversion"></a>启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上的远程连接  
 若要启用远程连接，请在本地使用 SQLCMD.exe 并对 Server Core 实例执行以下语句：  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-ssnoversion-browser-service"></a>启用并启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务  
 默认情况下，Browser 服务是禁用的。  如果在 Server Core 上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例禁用了该服务，请从命令提示符运行以下命令来启用它：  
  
 `sc config SQLBROWSER start= auto`  
  
 在启用该服务后，请从命令提示符运行以下命令来启动该服务：  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>在 Windows 防火墙中创建例外  
 若要在 Windows 防火墙中创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 访问的例外，请执行 [配置 Windows 防火墙以允许 SQL Server 访问](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)中指定的步骤。  
  
### <a name="enable-tcpip-on-the-instance-of-ssnoversion"></a>在实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上启用 TCP/IP  
 可以在 Server Core 上通过 Windows PowerShell 为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用 TCP/IP 协议。 执行以下步骤:  
  
1.  在运行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 的计算机上，启动任务管理器。  
  
2.  在 **“应用程序”** 选项卡上，单击 **“新建任务”** 。  
  
3.  在 **“创建新任务”** 对话框上的 **“打开”** 字段中键入 **sqlps.exe** ，然后单击 **“确定”** 。 这将打开** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**窗口。  
  
4.  在 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell** 窗口中，运行以下脚本以启用 TCP/IP 协议：  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = New-Object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>卸载  
 登录到运行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core 的计算机之后，您将拥有一个带有管理员命令提示符的受限制桌面环境。 您可以使用此命令提示符来启动 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例的卸载。 若要卸载 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例，请从命令提示符以完全静默模式（通过使用 /Q 参数）或简单静默模式（通过使用 /QS 参数）启动卸载。 /QS 参数将通过用户界面显示进度，但是不接受任何输入。 /Q 在没有任何用户界面的情况下以静默模式运行。  
  
 卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的现有实例：  
  
```cmd
setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 若要删除命名实例，请指定实例名称，而不是前面示例中的“MSSQLSERVER”。  
  
> [!WARNING]
>  如果您无意中关闭了命令提示符，可以使用以下步骤启动一个新的命令提示符：  
> 
>  1.  按 Ctrl+Shift+Esc 以显示任务管理器。  
> 2.  在 **“应用程序”** 选项卡上，单击 **“新建任务”** 。  
> 3.  在“创建新任务”  对话框上的“打开”  字段中键入 **cmd** ，然后 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。  
  
## <a name="see-also"></a>另请参阅  
 [使用配置文件安装 SQL Server 2014](install-sql-server-using-a-configuration-file.md)   
 [从命令提示符安装 SQL Server 2014](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014 的各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [服务器核心安装选项入门指南](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [配置服务器核心安装：概述](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Windows PowerShell 中按任务焦点列出的故障转移群集 Cmdlet](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters](https://go.microsoft.com/fwlink/?LinkId=221421)  
