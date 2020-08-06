---
title: 创建或配置可用性组侦听程序 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.newaglistener.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], client connectivity
ms.assetid: 2bc294f6-2312-4b6b-9478-2fb8a656e645
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2c74e92286eab4bc1be8f3f538d83d86f056cf01
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694563"
---
# <a name="create-or-configure-an-availability-group-listener-sql-server"></a>创建或配置可用性组侦听器 (SQL Server)
  本主题说明如何通过在中使用、或 PowerShell 为 AlwaysOn 可用性组创建或配置单个*可用性组侦听器* [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)] [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 。  
  
> [!IMPORTANT]  
>  若要创建某个可用性组的第一个可用性组侦听器，我们强烈建议您使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell。 除非必要情况，例如创建附加侦听器，否则，应避免直接在 WSFC 群集中创建侦听器。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="does-a-listener-exist-for-this-availability-group-already"></a><a name="DoesListenerExist"></a> 已存在此可用性组的侦听器？  
 **确定可用性组是否已存在一个侦听器**  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
> [!NOTE]  
>  如果某个侦听程序已存在并且你想要创建附加的侦听程序，请参阅本文后面的 [为可用性组创建其他侦听程序（可选）](#CreateAdditionalListener)。  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   您只能通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]为每个可用性组创建一个侦听器。 通常情况下，每个可用性组只需要一个侦听器。 但是，某些用户群体要求一个可用性组多个侦听器。   通过 SQL Server 创建一个侦听器之后，您可以将 Windows PowerShell 用于故障转移群集或使用 WSFC 故障转移群集管理器来创建其他侦听器。 有关详细信息，请参阅本主题后面的 [为可用性组创建其他侦听程序（可选）](#CreateAdditionalListener)。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
 建议对于多子网配置使用静态 IP 地址，尽管不是必需的。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
  
-   您必须连接到承载主副本的服务器实例。  
  
-   如果您正在跨多个子网设置一个可用性组侦听器并计划使用静态 IP 地址，则对于承载您要为其创建侦听器的可用性组的可用性副本的每个子网，您需要获取其静态 IP 地址。 通常，您需要向网络管理员索取静态 IP 地址。  
  
> [!IMPORTANT]  
>  在创建你的第一个侦听程序之前，我们强烈建议你阅读 [AlwaysOn 客户端连接 (SQL Server)](always-on-client-connectivity-sql-server.md)。  
  
###  <a name="requirements-for-the-dns-name-of-an-availability-group-listener"></a><a name="DNSnameReqs"></a> 可用性组侦听器的 DNS 名称的要求  
 每个可用性组侦听器都需要一个 DNS 主机名，该名称在域和 NetBIOS 中是唯一的。 DNS 名称为字符串值。 该名称只能包含字母数字字符、破折号 (-) 和连字符 (_)，顺序不分先后。 DNS 主机名不区分大小写。 最大长度为 63 个字符，但是，在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，您可以指定的最大长度为 15 个字符。  
  
 我们建议您指定一个有意义的字符串。 例如，对于名为 `AG1`的可用性组，有意义的 DNS 主机名将是 `ag1-listener`。  
  
> [!IMPORTANT]  
>  NetBIOS 只识别 dns_name 中的前 15 个字符。 如果您的两个 WSFC 群集均由同一 Active Directory 控制，而您试图使用超过 15 个字符的名称（具有相同的 15 字符前缀）在这两个群集中创建可用性组侦听器，此时您将收到错误，报告无法使虚拟网络名称资源联机。 有关 DNS 名称的前缀命名规则的信息，请参阅 [分配域名](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx)。  
  
###  <a name="windows-permissions"></a><a name="WinPermissions"></a> Windows 权限  
  
|权限|链接|  
|-----------------|----------|  
|托管可用性组的 WSFC 群集的群集对象名称 (CNO) 必须具有“创建计算机对象”  权限。<br /><br /> 在 Active Directory 中，CNO 默认不具有显式“创建计算机对象”  权限，并且可以创建 10 个虚拟计算机对象 (VCO)。 在创建了 10 个 VCO 后，再创建 VCO 将失败。 可通过将权限显式授予 WSFC 群集的 CNO，避免发生此情况。 请注意，您已删除的可用性组的 VCO 并不自动在 Active Directory 中删除，因此，在手动删除它们之前，10 个 VCO 的默认数目限制仍会将其计算在内。<br /><br /> 注意：在某些组织中，安全策略禁止向单独用户帐户授予“创建计算机对象”权限  。|为安装此群集的人员配置帐户的步骤（位于[故障转移群集分步指南  ：在 Active Directory 中配置帐户](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_installer)中）<br /><br /> 预配置群集名称帐户的步骤（位于[故障转移群集分步指南  ：在 Active Directory 中配置帐户](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating)中）|  
|如果你的组织要求你为侦听器虚拟网络名称预配置计算机帐户，则你需要具有  “帐户操作员”组的成员资格或域管理员的帮助。<br /><br /> 提示：一般情况下，最简单的方法是不为侦听程序虚拟网络名称预配置计算机帐户。 如果可以，请在运行 WSFC 高可用性向导时自动创建并配置该帐户。|*故障转移群集分步指南：在 Active Directory 中配置帐户* 中的 [为群集服务或应用程序预配置帐户的步骤](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating2)。|  
  
###  <a name="sql-server-permissions"></a><a name="SqlPermissions"></a> SQL Server 权限  
  
|任务|权限|  
|----------|-----------------|  
|创建可用性组侦听器|需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
|修改现有可用性组侦听器|对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!TIP]  
>  [“新建可用性组”向导 ](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 支持为新可用性组创建侦听程序。  
  
 **创建和配置可用性组侦听器**  
  
1.  在对象资源管理器中，连接到承载可用性组的主副本的服务器实例，然后单击此服务器名称以展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  单击您要配置其侦听器的可用性组，然后选择以下备选方法之一：  
  
    -   若要创建一个侦听程序，请右键单击“可用性组侦听程序”  节点，然后选择“新建侦听程序”  命令。 这将打开 **“新建可用性组侦听器”** 对话框。 有关详细信息，请参阅本主题后面的[添加可用性组侦听程序（对话框）](#AddAgListenerDialog)。  
  
    -   若要更改现有侦听程序的端口号，请展开“可用性组侦听程序”  节点，右键单击此侦听程序，然后选择“属性”  命令。 在 **“端口”** 字段中输入新的端口号，然后单击 **“确定”** 。  
  
###  <a name="new-availability-group-listener-dialog-box"></a><a name="AddAgListenerDialog"></a> 新建可用性组（对话框）  
 **侦听器 DNS 名称**  
 指定可用性组侦听器的 DNS 主机名。 DNS 名称为字符串，且在域和 NetBIOS 中必须唯一。 该名称只能包含字母数字字符、破折号 (-) 和连字符 (_)，顺序不分先后。 DNS 主机名不区分大小写。 最大长度为 15 个字符。  
  
 有关详细信息，请参阅本主题前面的 [可用性组侦听器的 DNS 名称的要求](#DNSnameReqs)。  
  
 端口   
 该侦听器使用的 TPC 端口。  
  
 **网络模式**  
 指示该侦听器使用的 TCP 协议，选择如下一种：  
  
 **DHCP**  
 侦听器将使用运行动态主机配置协议 (DHCP) 的服务器分配的动态 IP 地址。 DHCP 仅限于单个子网。  
  
> [!IMPORTANT]  
>  不建议在生产环境中使用 DHCP。 如果停止工作且 DHCP IP 租期已到，则需要额外的时间来注册与侦听器 DNS 名称相关联且影响客户端连接的新 DHCP 网络 IP 地址。 但是，DHCP 适合用于设置开发和测试环境以验证可用性组的基本功能并适合与应用程序集成。  
  
 **静态 IP**  
 侦听器将使用一个或多个静态 IP 地址。 其他 IP 地址是可选的。 若要跨多个子网创建一个可用性组侦听器，必须在侦听器配置中为每个子网指定一个静态 IP 地址。 请与您的网络管理员联系以获取这些静态 IP 地址。  
  
 如果您选择 **“静态 IP”** ，则会在 **“网络模式”** 字段下出现一个子网网格。 此网格将显示有关该可用性组侦听器可以访问的每个子网的信息。 在通过单击 **“添加”** 添加静态 IP 地址之前，该网格为空。  
  
 这些列如下所示：  
  
 **子网**  
 显示您添加到可用性组侦听器的每个子网的标识符。  
  
 **IP 地址**  
 显示给定子网的 IP 地址。  对于给定子网，静态 IP 地址可以是 IPv4 地址或 IPv6 地址。  
  
 **添加**  
 单击“添加”可将静态 IP 地址添加到所选子网，或添加到该侦听器的其他子网。 这将打开 **“添加 IP 地址”** 对话框。 有关详细信息，请参阅[添加 IP 地址对话框 (SQL Server Management Studio)](add-ip-address-dialog-box-sql-server-management-studio.md) 帮助主题。  
  
 **删除**  
 单击此项可以从侦听器中移除所选子网。  
  
 **确定**  
 单击此选项可创建指定的可用性组侦听器。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  

### <a name="to-create-or-configure-an-availability-group-listener"></a>创建和配置可用性组侦听器
  
1.  连接到承载主副本的服务器实例。  
  
2.  使用 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql) 语句的 LISTENER 选项或 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句的 ADD LISTENER 选项。  
  
     下面的示例将可用性组侦听器添加到名为 `MyAg2`的现有可用性组。 将为此侦听器指定唯一的 DNS 名称 `MyAg2ListenerIvP6`。 两个副本位于不同的子网，因此按照建议，侦听器使用静态 IP 地址。 对于这两个可用性副本中的每一个，WITH IP 子句都指定一个将使用 IPv6 格式的静态 IP 地址 `2001:4898:f0:f00f::cf3c and 2001:4898:e0:f213::4ce2`。 此示例还指定使用可选的 PORT 参数来将端口 `60173` 指定为侦听器端口。  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAg2   
          ADD LISTENER 'MyAg2ListenerIvP6' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
    GO  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-create-or-configure-an-availability-group-listener"></a>创建和配置可用性组侦听器 
  
1.  将目录 (`cd`) 更改为承载主副本的服务器实例。  
  
2.  使用下列 cmdlet 之一创建或修改可用性组侦听器：  
  
     `New-SqlAvailabilityGroupListener`  
     创建一个新的可用性组侦听器，并将其附加到一个现有可用性组。  
  
     例如，下列 `New-SqlAvailabilityGroupListener` 命令为可用性组 `MyListener` 创建命为 `MyAg` 的可用性组侦听器。 此侦听器将使用传递到 `-StaticIp` 参数的 IPv4 地址作为其虚拟 IP 地址。  
  
    ```powershell
    New-SqlAvailabilityGroupListener -Name MyListener `
    -StaticIp '192.168.3.1/255.255.252.0' `
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg
    ```  
  
     `Set-SqlAvailabilityGroupListener`  
     修改现有可用性组侦听器的端口设置。  
  
     例如，下列 `Set-SqlAvailabilityGroupListener` 命令将名为 `MyListener` 的可用性组侦听器的端口号设置为 `1535`。 此端口用于侦听与侦听器的连接。  
  
    ```powershell
    Set-SqlAvailabilityGroupListener -Port 1535 `
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
    ```  
  
     `Add-SqlAGListenerstaticIp`  
     将一个静态 IP 地址添加到现有的可用性组侦听器配置。 此 IP 地址可以是带子网的 IPv4 地址或 IPv6 地址。  
  
     例如，下列 `Add-SqlAGListenerstaticIp` 命令将一个静态 IPv4 地址添加到可用性组 `MyListener` 的可用性组侦听器 `MyAg`。 此 IPv6 地址用作子网 `255.255.252.0`上侦听器的虚拟 IP 地址。 如果可用性组跨多个子网，则应将针对每个子网的静态 IP 地址添加到侦听器。  
  
    ```powershell
    $path = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\ MyListener" `
    Add-SqlAGListenerstaticIp -Path $path `
    -StaticIp "2001:0db8:85a3:0000:0000:8a2e:0370:7334"  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 PowerShell 环境中使用**get-help** cmdlet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
若要设置并使用 SQL Server PowerShell 提供程序，请参阅[SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)。
  
## <a name="troubleshooting"></a>疑难解答  
  
###  <a name="failure-to-create-an-availability-group-listener-because-of-active-directory-quotas"></a><a name="ADQuotas"></a>由于 Active Directory 配额，导致无法创建可用性组侦听器  
 新的可用性组侦听器可能在创建时失败，因为您已经达到参与群集节点计算机帐户的 Active Directory 配额。  有关详细信息，请参阅下列文章：  
  
-   [超链接 " https://support.microsoft.com/kb/307532 " 如何在群集服务帐户修改计算机对象时对其进行故障排除](https://support.microsoft.com/kb/307532)  
  
-   [超链接 " https://technet.microsoft.com/library/cc904295(WS.10).aspx " Active Directory 配额](https://technet.microsoft.com/library/cc904295\(WS.10\).aspx)  
  
##  <a name="follow-up-after-creating-an-availability-group-listener"></a><a name="FollowUp"></a>跟进：在创建可用性组侦听器之后  
  
###  <a name="multisubnetfailover-keyword-and-associated-features"></a><a name="MultiSubnetFailover"></a>MultiSubnetFailover 关键字和相关功能  
 `MultiSubnetFailover` 是一个新连接字符串关键字，在 SQL Server 2012 中可使用它通过 AlwaysOn 可用性组和 AlwaysOn 故障转移群集实例进行更快速的故障转移。 在连接字符串中设置 `MultiSubnetFailover=True` 时，将启用以下三个子功能：  
  
-   更快进行多子网故障转移到 AlwaysOn 可用性组或故障转移群集实例的多子网侦听器。  
  
-   更快进行单子网故障转移到 AlwaysOn 可用性组或故障转移群集实例的单子网侦听器。  
  
    -   当连接到具有单个子网中的单个 IP 的侦听器时使用此功能。 这将进行更频繁的 TCP 连接重试以加快单子网故障转移。  
  
-   多子网 AlwaysOn 故障转移群集实例的命名实例解析。  
  
    -   这将添加对具有多子网端点的 AlwaysOn 故障转移群集实例的命名实例解析支持。  
  
 **NET Framework 3.5 或 OLEDB 不支持 MultiSubnetFailover=True**  
  
 **问题：** 如果你的可用性组或故障转移群集实例具有侦听程序名称 (称为 WSFC 群集管理器中的网络名称或客户端访问点) 根据不同子网中的多个 IP 地址，并且你使用的是具有 .NET Framework 3.5 SP1 或 SQL Native Client 11.0 OLEDB 的 ADO.NET，则可能50% 的客户端与可用性组侦听器的连接请求将达到连接超时。  
  
 **解决方法：** 我们建议你执行以下任务之一。  
  
-   如果您无权操作群集资源，则将连接超时更改为 30 秒（该值导致 20 秒的 TCP 超时期加上 10 秒的缓冲）。  
  
     优点  ：如果发生跨子网故障转移，则客户端恢复时间将比较短。  
  
     缺点  ：半数的客户端连接将需要 20 多秒  
  
-   如果您有权操作群集资源，则强烈建议您将可用性组侦听器的网络名称设置为 `RegisterAllProvidersIP=0`。 有关详细信息，请参阅本节后面的“RegisterAllProvidersIP 设置”。  
  
     优点  ：无需增加客户端连接超时值。  
  
     **缺点：** 如果发生跨子网故障转移，则客户端恢复时间可能为15分钟或更长，具体取决于您的 `HostRecordTTL` 设置以及您的跨站点 DNS/AD 复制计划的设置。  
  
###  <a name="registerallprovidersip-setting"></a><a name="RegisterAllProvidersIP"></a>RegisterAllProvidersIP 设置  
 在使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell 创建可用性组侦听器时，将在 WSFC 中创建客户端访问点，其 `RegisterAllProvidersIP` 属性设为 1 (true)。 此属性值的影响取决于客户端连接字符串，如下所示：  
  
-   将 `MultiSubnetFailover` 设置为 true 的连接字符串  
  
     [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]将 `RegisterAllProvidersIP` 属性设置为1，以便在故障转移后，针对客户端连接字符串指定的客户端，根据建议缩短重新连接时间 `MultiSubnetFailover = True` 。 请注意，为了利用侦听器多子网功能，您的客户端可能会要求支持 `MultiSubnetFailover` 关键字的数据访问接口。 有关针对多子网故障转移的驱动程序支持的信息，请参阅 [AlwaysOn 客户端连接 (SQL Server)](always-on-client-connectivity-sql-server.md)。  
  
     有关多子网群集的信息，请参阅 [SQL Server 多子网群集 (SQL Server)](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)为每个可用性组创建一个侦听器。  
  
    > [!TIP]  
    >  在 `RegisterAllProvidersIP = 1`时，如果您在 WSFC 群集上运行 WSFC 验证配置向导，该向导将生成以下警告消息：  
    >   
    >  “网络名称 ‘Name:<network_name>’ 的 RegisterAllProviderIP 属性设为 1。对于当前群集配置，该值应设为 0。”  
    >   
    >  请忽略此消息。  
  
-   未将 `MultiSubnetFailover` 设置为 true 的连接字符串  
  
     在 `RegisterAllProvidersIP = 1`时，其连接字符串未使用 `MultiSubnetFailover = True`的任何客户端都将会经历高延迟的连接。 发生这种情况的原因是这些客户端将按顺序尝试与所有 IP 的连接。 相反，如果将 `RegisterAllProvidersIP` 更改为 0，将在 WSFC 群集中的客户端接入点注册活动 IP 地址，从而缩短旧客户端的延迟时间。 因此，如果您的旧客户端需要连接到某一可用性组侦听器并且不能使用 `MultiSubnetFailover` 属性，我们建议您将更改 `RegisterAllProvidersIP` 为0。  
  
    > [!IMPORTANT]  
    >  在您通过 WSFC 群集（故障转移群集管理器 GUI）创建可用性组侦听器时，`RegisterAllProvidersIP` 默认将为 0 (false)。  
  
###  <a name="hostrecordttl-setting"></a><a name="HostRecordTTL"></a>HostRecordTTL 设置  
 默认情况下，客户端缓存 20 分钟的群集 DNS 记录。  通过缩短缓存记录的 `HostRecordTTL`（生存时间 (TTL)），旧客户端可以更快地重新连接。  但是，减小 `HostRecordTTL` 设置还可能导致到 DN 服务器的流量增加。  
  
###  <a name="sample-powershell-script-to-disable-registerallprovidersip-and-reduce-ttl"></a><a name="SampleScript"></a>用于禁用 RegisterAllProvidersIP 和减少 TTL 的示例 PowerShell 脚本  
 下面的 PowerShell 示例演示如何为侦听器资源配置 `RegisterAllProvidersIP` 和 `HostRecordTTL` 群集参数。  DNS 记录将缓存 5 分钟，而不是默认的 20 分钟。  同时修改两个群集参数可以缩短无法使用 `MultiSubnetFailover` 参数的旧客户端在故障转移后连接到正确 IP 地址的时间。  使用您要更改的侦听器名称替换 `yourListenerName` 。  
  
```powershell
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName | Set-ClusterParameter RegisterAllProvidersIP 0
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
Stop-ClusterResource yourListenerName  
Start-ClusterResource yourAGResource  
```  
  
 有关故障转移期间的恢复时间的详细信息，请参阅 [Client Recovery Latency During Failover](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md#DNS)。  
  
###  <a name="follow-up-recommendations"></a><a name="FollowUpRecommendations"></a>跟进建议  
 在创建可用性组侦听器后：  
  
-   请求您的网络管理员将该侦听器的 IP 地址保留为专用。  
  
-   将该侦听器的 DNS 主机名提供给应用程序开发人员，以便在请求与此可用性组的客户端连接时用于连接字符串中。  
  
-   如有可能，鼓励开发人员更新客户端连接字符串，以便指定 `MultiSubnetFailover = True`。 有关针对多子网故障转移的驱动程序支持的信息，请参阅 [AlwaysOn 客户端连接 (SQL Server)](always-on-client-connectivity-sql-server.md)。  
  
###  <a name="create-an-additional-listener-for-an-availability-group-optional"></a><a name="CreateAdditionalListener"></a>为可用性组创建其他侦听器 (可选)   
 通过 SQL Server 创建一个侦听器之后，您可以添加其他侦听器，如下所示：  
  
1.  使用下列任一工具创建侦听器：  
  
    -   **使用 WSFC 故障转移群集管理器：**  
  
        1.  添加客户端访问点并配置 IP 地址。  
  
        2.  使侦听器联机。  
  
        3.  向 WSFC 可用性组资源添加一个依赖项。  
  
         有关故障转移群集管理器的对话框和选项卡的信息，请参阅 [用户界面：故障转移群集管理器管理单元](https://technet.microsoft.com/library/cc772502.aspx)。  
  
    -   **将 Windows PowerShell 用于故障转移群集：**  
  
        1.  使用 [Add-ClusterResource](https://technet.microsoft.com/library/ee460983.aspx) 创建网络名称和 IP 地址资源。  
  
        2.  使用 [Start-ClusterResource](https://technet.microsoft.com/library/ee461056.aspx) 启动网络名称资源。  
  
        3.  使用 [Add-ClusterResourceDependency](https://technet.microsoft.com/library/ee461014.aspx) 设置网络名称与现有 SQL Server 可用性组资源之间的依赖关系。  
  
         有关将 Windows PowerShell 用于故障转移群集的信息，请参阅 [服务器管理器命令概述](https://technet.microsoft.com/library/cc732757.aspx#BKMK_wps)。  
  
2.  在新的侦听器上启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 侦听。 在创建其他侦听器之后，可连接到承载可用性组主副本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，并使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]或 PowerShell 修改侦听器端口。  
  
 有关详细信息，请参阅 [How to create multiple listeners for same availability group](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao.aspx)（如何为同一可用性组创建多个侦听程序）（SQL Server AlwaysOn 团队博客）。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
-   [删除可用性组侦听程序 (SQL Server)](remove-an-availability-group-listener-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相关内容  
  
-   [如何为相同的可用性组创建多个侦听程序](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao.aspx)  
  
-   [SQL Server AlwaysOn 团队博客：官方 SQL Server AlwaysOn 团队博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组 &#40;SQL Server 概述&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [SQL Server 多子网群集 (SQL Server)](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
