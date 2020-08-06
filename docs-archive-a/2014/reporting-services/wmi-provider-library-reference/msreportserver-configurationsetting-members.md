---
title: MSReportServer_ConfigurationSetting 成员 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 73c0114d2db65da92998de944355f3889ddd12e6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690347"
---
# <a name="msreportserver_configurationsetting-members"></a>MSReportServer_ConfigurationSetting 成员
  MSReportServer_ConfigurationSetting 类包含以下属性和方法。  
  
## <a name="public-properties"></a>公共属性  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|返回连接池大小，报表服务器用来与托管报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例进行通信。 只读。|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|指定报表服务器连接到承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例时使用的登录帐户。 只读。|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|指定尝试登录到报表服务器数据库失败前等待的秒数。 只读。|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|指定报表服务器是使用 Windows 服务帐户、Windows 用户帐户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名访问报表服务器数据库。 只读。|  
|[DatabaseName](configurationsetting-property-databasename.md)|指定承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|指定命令失败或超时之前必须等待的秒数。报表服务器会根据报表服务器数据库对进程进行计时，而不会根据报表的数据源计时。|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|指定用来安装报表服务器数据库的服务器的名称。|  
|[InstallationID 属性](configurationsetting-property-installationid.md)|返回特定报表服务器实例的唯一标识符。|  
|[InstanceName](configurationsetting-property-instancename.md)|指定特定计算机上报表服务器实例的名称。|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|指示报表服务器实例是否已初始化。 只读。|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|指示报表服务器是否配置为 SharePoint 集成模式。|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|指示是否已启用报表服务器 Web 服务。 只读。|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|指示是否已启用报表服务器 Windows 服务。 只读。|  
|[MachineAccountIdentity 属性 (WMI)](configurationsetting-property-machineaccountidentity.md)|获取安装了报表服务器的计算机的计算机帐户标识。|  
|[PathName](configurationsetting-property-pathname.md)|指定报表服务器实例的安装路径。|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|返回 RSReportServer.config 文件中指定的安全连接级别。|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|从报表服务器获取用于发送电子邮件的地址。 只读。|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|指定电子邮件配置中 SendUsing 属性是否设置为 TRUE。|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|从 RSReportServer.config 文件中获取 SMTP 服务器属性。 只读。|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|指定以无人参与方式运行报表时报表服务器将模拟的登录用户帐户。 只读。|  
|[版本](configurationsetting-property-version.md)|返回报表服务器的版本。|  
|[VirtualDirectoryReportManager 属性 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-property-virtualdirectoryreportmanager.md)|返回报表管理器应用程序的虚拟目录。|  
|[VirtualDirectoryReportServer 属性 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-property-virtualdirectoryreportserver.md)|返回报表服务器 Web 服务应用程序的虚拟目录。|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|返回报表服务器 Windows 服务运行时实际使用的标识。 只读。|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|返回在上次配置报表服务器 Windows 服务时所指定的运行时要使用的标识。 只读。|  
  
## <a name="public-methods"></a>公共方法  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|备份实例的加密密钥。 加密密钥会在使用密码加密后存储。|  
|[CreateSSLCertificateBinding 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-createsslcertificatebinding.md)|创建 SSL 证书绑定。|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|从报表服务器数据库删除加密信息。|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|从报表服务器数据库删除加密密钥。|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|生成可用于创建报表服务器数据库的 SQL 脚本。|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|生成可用来向用户授予报表服务器数据库权限的 SQL 脚本。|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|生成可用于升级报表服务器数据库的 SQL 脚本。|  
|[GetAdminSiteUrl 方法 (WMI)](configurationsetting-method-getadminsiteurl.md)|获取管理中心网站的绝对 URL。|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|获取给定报表服务器数据库版本字符串的显示名称。|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|初始化指定报表服务器实例。|  
|[ListInstalledSharePointVersions 方法 (WMI)](configurationsetting-method-listinstalledsharepointversions.md)|返回一组标记，表示与报表服务器安装在同一台计算机上的 [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 版本。|  
|[ListIPAddresses 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listipaddresses.md)|列出计算机的 IP 地址。|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|返回报表服务器数据库中存在的报表服务器安装列表，无论这些安装是否具有访问安全信息的权限。|  
|[ListReservedURLs 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listreservedurls.md)|列出为报表服务器上所有应用程序保留的 URL。|  
|[ListSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificatebindings.md)|列出 HTTP.SYS 中存在的以及 rsreportserver.config 中应有的 SSL 证书绑定。|  
|[ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-listsslcertificates.md)|列出计算机上安装的 SSL 证书。|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|生成新的加密密钥，并使用新密钥对报表服务器数据库中的所有安全信息进行重新加密。|  
|[RemoveSSLCertificateBindings 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-removesslcertificatebinding.md)|删除 SSL 证书绑定。|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|从报表服务器配置中删除无人参与的执行帐户条目。|  
|[RemoveURL 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-removeurl.md)|删除为报表服务器保留的 URL。|  
|[ReserveURL 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-reserveurl.md)|为给定的应用程序添加一个 URL 预留。|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|将指定的加密密钥重新应用于报表服务器数据库。|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|设置与特定报表服务器数据库的报表服务器数据库连接。|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|为报表服务器数据库登录尝试指定默认超时值。|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|为报表服务器数据库连接指定默认超时值。|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|配置报表服务器用来发送电子邮件的电子邮件传递扩展插件。|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|设置报表服务器的安全连接级别。|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|打开和关闭报表服务器 Windows 服务和 Web 服务。|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|指定用于以无人参与方式运行报表的帐户。|  
|[SetVirtualDirectory 方法 (WMI MSReportServer_ConfigurationSetting)](configurationsetting-method-setvirtualdirectory.md)|设置应用程序的虚拟目录。|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|将报表服务器 Windows 服务作为指定的 Windows 用户运行，并授予此帐户足够的文件系统权限以允许操作报表服务器。|  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 类](msreportserver-configurationsetting-class.md)  
  
  
