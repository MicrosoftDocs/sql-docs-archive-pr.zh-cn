---
title: rsconfig 实用工具 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 499fa5529991b36e467567b4c7006845dfcd2578
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691574"
---
# <a name="rsconfig-utility-ssrs"></a>rsconfig 实用工具 (SSRS)
  **rsconfig.exe** 实用工具可以在 RSReportServer.config 文件中加密并存储连接和帐户值。 加密值包括用于无人参与报表处理的报表服务器数据库连接信息和帐户值。  
  
## <a name="syntax"></a>语法  
  
```  
  
      rsconfig {-?}  
{-cconnection}  
{-eunattendedaccount}  
{-mcomputername}  
{-iinstancename}  
{-sservername}  
{-ddatabasename}  
{-aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>参数  
  
|术语|可选/必需|定义|  
|----------|------------------------|----------------|  
|**-?**|可选。|显示 Rsconfig.exe 参数的语法。|  
|`-c`|如果未使用 `-e` 参数，则为必需项。|指定用于将报表服务器连接到报表服务器数据库的连接字符串、凭据和数据源值。<br /><br /> 此参数不带值。 但是，必须对其指定其他参数以提供所有必需的连接值。<br /><br /> 可以指定的参数 `-c` 包括 `-m` 、 **-s**、、、、、 `-i` `-d` `-a` `-u` `-p` 和 `-t` 。|  
|`-e`|如果未使用 `-c` 参数，则为必需项。|指定无人参与报表执行帐户。<br /><br /> 此参数不带值。 但是，您必须在命令行中指定其他参数，以指定配置文件中加密的值。<br /><br /> 可以使用 `-e` 指定的参数包括 `-u` 和 `-p`。 您还可以设置 `-t`。|  
|`-m`  *computername*|如果要配置远程报表服务器实例，则此参数是必需的。|指定承载报表服务器的计算机的名称。 如果省略该参数，则默认值为 `localhost`。|  
|-s**  servername**  **|必需。|指定承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。|  
|`-i`  *instancename*|如果使用了命名实例，则此参数是必需的。|如果使用了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 命名实例承载报表服务器数据库，则此值指定该命名实例。|  
|`-d`  *database*|必需。|指定报表服务器数据库的名称。|  
|`-a`  *authmethod*|必需。|指定报表服务器连接到报表服务器数据库时使用的身份验证方法。 有效值是 `Windows` 或 `SQL`（该参数不区分大小写）。<br /><br /> `Windows` 指定报表服务器使用 Windows 身份验证。<br /><br /> `SQL` 指定报表服务器使用 SQL Server 身份验证。|  
|`-u`  *[域 \\ ]用户名*|`-e` 是必需的，`-c` 是可选的。|指定报表服务器数据库连接或无人参与帐户的用户帐户。<br /><br /> 对于 **rsconfig -e**，该参数是必需的。 必须是域用户帐户。<br /><br /> 对于**rsconfig-c**和 `-a SQL` ，此参数必须指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。<br /><br /> 对于**rsconfig**和 `-a Windows` ，此参数可以指定域用户、内置帐户或服务帐户凭据。 若要指定域帐户，请以“domain\username”** 格式指定域** 和用户名**。 如果使用了内置帐户，则该参数是可选的。 如果要使用服务帐户凭据，则可省略该参数。|  
|`-p`  *权限*|如果指定了 `-u`，则该参数是必需的。|指定与 *username* 参数一起使用的密码。 如果帐户不需要密码，则可将该参数设置为空值。 对于域帐户，此值区分大小写。|  
|`-t`|可选。|将错误消息输出到跟踪日志。 此参数不带值。 有关详细信息，请参阅 [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md)。|  
  
## <a name="permissions"></a>权限  
 您必须是要配置的承载报表服务器的计算机本地管理员。  
  
## <a name="file-location"></a>文件位置  
 Rsconfig.exe 位于 **\Program Files\Microsoft SQL Server\110\Tools\Binn**中。 可以在文件系统的任何文件夹中运行此实用工具。  
  
## <a name="remarks"></a>备注  
 Rsconfig.exe 有以下两个用途：  
  
-   修改报表服务器用于连接到报表服务器数据库的连接信息。  
  
-   配置报表服务器在其他凭据不可用时登录远程数据库服务器所用的特殊帐户。  
  
 可以针对**的本地或远程实例来运行** rsconfig [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]实用工具。 不能使用 **rsconfig** 实用工具解密和查看已设置的值。  
  
 要配置的计算机上必须安装 Windows Management Instrumentation (WMI) 才能运行此配置工具。  
  
## <a name="examples"></a>示例  
 以下示例阐释了 **rsconfig**的使用方法。  
  
#### <a name="specifying-a-domain-user-account"></a>指定域用户帐户  
 此示例显示如何配置报表服务器，以便在连接本地报表服务器数据库时使用域用户帐户。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>指定 SQL Server 数据库用户帐户  
 此示例显示如何配置报表服务器配置以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名连接到远程报表服务器数据库。  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>指定内置帐户  
 此示例显示如何配置报表服务器，以便在连接本地报表服务器数据库时使用内置帐户。 请注意，未使用 `-u` 参数。 支持的内置帐户值的示例包括用于本地系统的 NT AUTHORITY\SYSTEM 和用于网络服务的 NT AUTHORITY\NETWORKSERVICE ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 仅) 。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>指定服务帐户  
 此示例显示如何配置报表服务器，以便在连接本地报表服务器数据库时使用 Report Server Windows 服务帐户和 Web 服务帐户。 请注意，未使用 `-u` 参数，并且没有指定任何帐户信息。 从命令中清除帐户值时， **rsconfig** 实用工具使用每个服务运行时都要使用的集成安全性和服务帐户。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>指定本地服务器中的无人参与帐户  
 此示例显示如何配置用于报表的无人参与报表执行的帐户，该帐户不向外部数据源传递凭据。 该帐户必须是 Windows 域帐户。 无法为用户名和密码指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 该帐户在本地报表服务器实例中配置。 在 ReportingServices\LogFiles 文件夹的跟踪日志中捕获错误消息。  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>指定远程服务器中的无人参与帐户  
 此示例显示在与 Rsconfig.exe 版本相同的远程报表服务器实例（例如，报表服务器和 Rsconfig.exe 都为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 版）中如何配置帐户。 在远程服务器的跟踪日志中捕获错误消息信息。  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSRS Configuration Manager 配置报表服务器数据库连接&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [&#40;SSRS Configuration Manager 配置无人参与的执行帐户&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services 报表服务器（本机模式）](../report-server/reporting-services-report-server-native-mode.md)   
 [存储加密的 Report Server 数据（SSRS 配置管理器）](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 配置文件](../report-server/reporting-services-configuration-files.md)   
 [报表服务器命令提示实用工具 &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)  
  
  
