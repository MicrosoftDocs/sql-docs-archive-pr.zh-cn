---
title: CLR 集成代码访问安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
ms.openlocfilehash: 75b283da2760b39349351802a83caae04e546c06
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580774"
---
# <a name="clr-integration-code-access-security"></a><span data-ttu-id="249d6-102">CLR 集成代码访问安全性</span><span class="sxs-lookup"><span data-stu-id="249d6-102">CLR Integration Code Access Security</span></span>
  <span data-ttu-id="249d6-103">公共语言运行时 (CLR) 支持用于托管代码的一种称为代码访问安全性的安全模式。</span><span class="sxs-lookup"><span data-stu-id="249d6-103">The common language runtime (CLR) supports a security model called code access security for managed code.</span></span> <span data-ttu-id="249d6-104">在这种模式下，根据代码的标识来对程序集授予权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-104">In this model, permissions are granted to assemblies based on the identity of the code.</span></span> <span data-ttu-id="249d6-105">有关详细信息，请参阅 .NET Framework 软件开发包中的“代码访问安全性”部分。</span><span class="sxs-lookup"><span data-stu-id="249d6-105">For more information, see the "Code Access Security" section in the .NET Framework software development kit.</span></span>  
  
 <span data-ttu-id="249d6-106">决定授予程序集的权限的安全策略定义在三个不同的位置：</span><span class="sxs-lookup"><span data-stu-id="249d6-106">The security policy that determines the permissions granted to assemblies is defined in three different places:</span></span>  
  
-   <span data-ttu-id="249d6-107">计算机策略：这是对安装了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的计算机中运行的所有托管代码都有效的策略。</span><span class="sxs-lookup"><span data-stu-id="249d6-107">Machine policy: This is the policy in effect for all managed code running in the machine on which [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] is installed.</span></span>  
  
-   <span data-ttu-id="249d6-108">用户策略：这是对进程承载的托管代码有效的策略。</span><span class="sxs-lookup"><span data-stu-id="249d6-108">User policy: This is the policy in effect for managed code hosted by a process.</span></span> <span data-ttu-id="249d6-109">[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务正在运行。</span><span class="sxs-lookup"><span data-stu-id="249d6-109">For [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] service is running.</span></span>  
  
-   <span data-ttu-id="249d6-110">主机策略：这是由 CLR（在本例中为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）的主机设置的策略，对该主机中运行的托管代码有效。</span><span class="sxs-lookup"><span data-stu-id="249d6-110">Host policy: This is the policy set up by the host of the CLR (in this case, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) that is in effect for managed code running in that host.</span></span>  
  
 <span data-ttu-id="249d6-111">CLR 支持的代码访问安全机制基于如下假设：运行时既可承载完全可信任的代码，也可承载部分可信任的代码。</span><span class="sxs-lookup"><span data-stu-id="249d6-111">The code access security mechanism supported by the CLR is based on the assumption that the runtime can host both fully trusted and partially trusted code.</span></span> <span data-ttu-id="249d6-112">在允许访问资源之前，由 CLR 代码访问安全性保护的资源通常由 requirethe 相应权限的托管应用程序编程接口进行包装。</span><span class="sxs-lookup"><span data-stu-id="249d6-112">The resources that are protected by CLR code access security are typically wrapped by managed application programming interfaces that requirethe corresponding permission before allowing access to the resource.</span></span> <span data-ttu-id="249d6-113">仅当调用堆栈中) 的程序集级别 (的所有调用方都具有相应的资源权限时，demandfor 才满足权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-113">The demandfor the permission is satisfied only if all the callers (at the assembly level) in the call stack have the corresponding resource permission.</span></span>  
  
 <span data-ttu-id="249d6-114">在中运行时授予托管代码的代码访问安全权限集向 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中加载的程序集授予一组权限 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，用户和计算机级别策略可能会进一步限制授予用户代码的最终权限集。</span><span class="sxs-lookup"><span data-stu-id="249d6-114">The set of code access security permissions that are granted to managed code when running inside [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grants a set of permissions to an assembly loaded in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], the eventual set of permissions given to user code may be restricted further by the user and machine-level policies.</span></span>  
  
## <a name="sql-server-host-policy-level-permission-sets"></a><span data-ttu-id="249d6-115">SQL Server 主机策略级别权限集</span><span class="sxs-lookup"><span data-stu-id="249d6-115">SQL Server Host Policy Level Permission Sets</span></span>  
 <span data-ttu-id="249d6-116">[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略级别授予程序集的代码访问安全性权限集由创建该程序集时指定的权限集决定。</span><span class="sxs-lookup"><span data-stu-id="249d6-116">The set of code access security permissions granted to assemblies by the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] host policy level is determined by the permission set specified when creating the assembly.</span></span> <span data-ttu-id="249d6-117">有三个权限集： `SAFE` `EXTERNAL_ACCESS` 和 `UNSAFE` (使用[CREATE ASSEMBLY &#40;transact-sql&#41;](/sql/t-sql/statements/create-assembly-transact-sql)) 的**PERMISSION_SET**选项指定。</span><span class="sxs-lookup"><span data-stu-id="249d6-117">There are three permission sets: `SAFE`, `EXTERNAL_ACCESS` and `UNSAFE` (specified using the **PERMISSION_SET** option of[CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)).</span></span>  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]<span data-ttu-id="249d6-118">.</span><span class="sxs-lookup"><span data-stu-id="249d6-118">.</span></span> <span data-ttu-id="249d6-119">此策略并不用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建 CLR 实例时有效的默认应用程序域。</span><span class="sxs-lookup"><span data-stu-id="249d6-119">This policy is not meant for the default application domain that would be in effect when [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] creates an instance of the CLR.</span></span>  
  
 <span data-ttu-id="249d6-120">用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集和用户指定的用户程序集策略的 fixedpolicy。</span><span class="sxs-lookup"><span data-stu-id="249d6-120">The [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fixedpolicy for system assemblies and user-specified policy for user assemblies.</span></span>  
  
 <span data-ttu-id="249d6-121">用于 CLR 程序集和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集的固定策略授予其完全信任。</span><span class="sxs-lookup"><span data-stu-id="249d6-121">The fixed policy for CLR assemblies and [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] system assemblies grants them full trust.</span></span>  
  
 <span data-ttu-id="249d6-122">[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略的用户指定部分基于为每个程序集指定三个权限存储桶之一的程序集所有者。</span><span class="sxs-lookup"><span data-stu-id="249d6-122">The user-specified portion of the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] host policy is based on the assembly owner specifying one of three permission buckets for each assembly.</span></span> <span data-ttu-id="249d6-123">有关以下列出的安全权限的详细信息，请参阅 .NET Framework SDK。</span><span class="sxs-lookup"><span data-stu-id="249d6-123">For more information about the security permissions listed below, see the .NET Framework SDK.</span></span>  
  
### <a name="safe"></a><span data-ttu-id="249d6-124">SAFE</span><span class="sxs-lookup"><span data-stu-id="249d6-124">SAFE</span></span>  
 <span data-ttu-id="249d6-125">只允许内部计算和本地数据访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-125">Only internal computation and local data access are allowed.</span></span> <span data-ttu-id="249d6-126">`SAFE` 是最具限制性的权限集。</span><span class="sxs-lookup"><span data-stu-id="249d6-126">`SAFE` is the most restrictive permission set.</span></span> <span data-ttu-id="249d6-127">由具有 `SAFE` 权限的程序集执行的代码无法访问外部系统资源，例如文件、网络、环境变量或注册表。</span><span class="sxs-lookup"><span data-stu-id="249d6-127">Code executed by an assembly with `SAFE` permissions cannot access external system resources such as files, the network, environment variables, or the registry.</span></span>  
  
 <span data-ttu-id="249d6-128">`SAFE` 程序集具有以下权限和值：</span><span class="sxs-lookup"><span data-stu-id="249d6-128">`SAFE` assemblies have the following permissions and values:</span></span>  
  
|<span data-ttu-id="249d6-129">权限</span><span class="sxs-lookup"><span data-stu-id="249d6-129">Permission</span></span>|<span data-ttu-id="249d6-130">值/说明</span><span class="sxs-lookup"><span data-stu-id="249d6-130">Value(s)/Description</span></span>|  
|----------------|-----------------------------|  
|`SecurityPermission`|<span data-ttu-id="249d6-131">`Execution:` 用于执行托管代码的权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-131">`Execution:` Permission to execute managed code.</span></span>|  
|`SqlClientPermission`|<span data-ttu-id="249d6-132">`Context connection = true`、`context connection = yes`：只能使用上下文连接并且连接字符串只能指定值“context connection=true”或“context connection=yes”。</span><span class="sxs-lookup"><span data-stu-id="249d6-132">`Context connection = true`, `context connection = yes`: Only the context-connection can be used and the connection string can only specify a value of "context connection=true" or "context connection=yes".</span></span><br /><br /> <span data-ttu-id="249d6-133">**AllowBlankPassword = false：** 不允许使用空白密码。</span><span class="sxs-lookup"><span data-stu-id="249d6-133">**AllowBlankPassword = false:**  Blank passwords are not permitted.</span></span>|  
  
### <a name="external_access"></a><span data-ttu-id="249d6-134">EXTERNAL_ACCESS</span><span class="sxs-lookup"><span data-stu-id="249d6-134">EXTERNAL_ACCESS</span></span>  
 <span data-ttu-id="249d6-135">EXTERNAL_ACCESS 程序集具有与程序集相同的权限，还可以 `SAFE` 访问外部系统资源，例如文件、网络、环境变量和注册表。</span><span class="sxs-lookup"><span data-stu-id="249d6-135">EXTERNAL_ACCESS assemblies have the same permissions as `SAFE` assemblies, with the additional ability to access external system resources such as files, networks, environmental variables, and the registry.</span></span>  
  
 <span data-ttu-id="249d6-136">`EXTERNAL_ACCESS` 程序集还具有以下权限和值：</span><span class="sxs-lookup"><span data-stu-id="249d6-136">`EXTERNAL_ACCESS` assemblies also have the following permissions and values:</span></span>  
  
|<span data-ttu-id="249d6-137">权限</span><span class="sxs-lookup"><span data-stu-id="249d6-137">Permission</span></span>|<span data-ttu-id="249d6-138">值/说明</span><span class="sxs-lookup"><span data-stu-id="249d6-138">Value(s)/Description</span></span>|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|<span data-ttu-id="249d6-139">`Unrestricted:`允许分布式事务。</span><span class="sxs-lookup"><span data-stu-id="249d6-139">`Unrestricted:` Distributed transactions are allowed.</span></span>|  
|`DNSPermission`|<span data-ttu-id="249d6-140">`Unrestricted:`从域名服务器请求信息的权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-140">`Unrestricted:` Permission to request information from Domain Name Servers.</span></span>|  
|`EnvironmentPermission`|<span data-ttu-id="249d6-141">`Unrestricted:` 允许对系统和用户环境变量进行完全访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-141">`Unrestricted:` Full access to system and user environment variables is allowed.</span></span>|  
|`EventLogPermission`|<span data-ttu-id="249d6-142">`Administer:` 允许执行以下操作：创建事件源、读取现有日志、删除事件源或日志、对项做出响应、清除事件日志、侦听事件以及访问所有事件日志的集合。</span><span class="sxs-lookup"><span data-stu-id="249d6-142">`Administer:` The following actions are allowed: creating an event source, reading existing logs, deleting event sources or logs, responding to entries, clearing an event log, listening to events, and accessing a collection of all event logs.</span></span>|  
|`FileIOPermission`|<span data-ttu-id="249d6-143">`Unrestricted:` 允许对文件和文件夹进行完全访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-143">`Unrestricted:` Full access to files and folders is allowed.</span></span>|  
|`KeyContainerPermission`|<span data-ttu-id="249d6-144">`Unrestricted:` 允许对密钥容器进行完全访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-144">`Unrestricted:` Full access to key containers is allowed.</span></span>|  
|`NetworkInformationPermission`|<span data-ttu-id="249d6-145">`Access:` 允许进行 Ping 操作。</span><span class="sxs-lookup"><span data-stu-id="249d6-145">`Access:` Pinging is permitted.</span></span>|  
|`RegistryPermission`|<span data-ttu-id="249d6-146">允许对 `HKEY_CLASSES_ROOT`、`HKEY_LOCAL_MACHINE`、`HKEY_CURRENT_USER`、`HKEY_CURRENT_CONFIG` 和 `HKEY_USERS.` 的读取权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-146">Allows read rights to `HKEY_CLASSES_ROOT`, `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CURRENT_CONFIG`, and `HKEY_USERS.`</span></span>|  
|`SecurityPermission`|<span data-ttu-id="249d6-147">`Assertion:` 能够断言此代码的所有调用方都具有执行该操作所需的权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-147">`Assertion:` Ability to assert that all the callers of this code have the requisite permission for the operation.</span></span><br /><br /> <span data-ttu-id="249d6-148">`ControlPrincipal:` 能够操作主体对象。</span><span class="sxs-lookup"><span data-stu-id="249d6-148">`ControlPrincipal:` Ability to manipulate the principal object.</span></span><br /><br /> <span data-ttu-id="249d6-149">`Execution:` 用于执行托管代码的权限。</span><span class="sxs-lookup"><span data-stu-id="249d6-149">`Execution:` Permission to execute managed code.</span></span><br /><br /> <span data-ttu-id="249d6-150">`SerializationFormatter:` 能够提供序列化服务。</span><span class="sxs-lookup"><span data-stu-id="249d6-150">`SerializationFormatter:` Ability to provide serialization services.</span></span>|  
|<span data-ttu-id="249d6-151">**SmtpPermission**</span><span class="sxs-lookup"><span data-stu-id="249d6-151">**SmtpPermission**</span></span>|<span data-ttu-id="249d6-152">`Access:` 允许与 SMTP 主机端口 25 建立出站连接。</span><span class="sxs-lookup"><span data-stu-id="249d6-152">`Access:` Outbound connections to SMTP host port 25 are allowed.</span></span>|  
|`SocketPermission`|<span data-ttu-id="249d6-153">`Connect:` 允许与传输地址建立出站连接（所有端口、所有协议）。</span><span class="sxs-lookup"><span data-stu-id="249d6-153">`Connect:` Outbound connections (all ports, all protocols) on a transport address are allowed.</span></span>|  
|`SqlClientPermission`|<span data-ttu-id="249d6-154">`Unrestricted:` 允许对数据源进行完全访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-154">`Unrestricted:` Full access to the datasource is allowed.</span></span>|  
|`StorePermission`|<span data-ttu-id="249d6-155">`Unrestricted:` 允许对 X.509 证书存储区进行完全访问。</span><span class="sxs-lookup"><span data-stu-id="249d6-155">`Unrestricted:` Full access to X.509 certificate stores is allowed.</span></span>|  
|`WebPermission`|<span data-ttu-id="249d6-156">`Connect:` 允许与 Web 资源建立出站连接。</span><span class="sxs-lookup"><span data-stu-id="249d6-156">`Connect:` Outbound connections to web resources are allowed.</span></span>|  
  
### <a name="unsafe"></a><span data-ttu-id="249d6-157">UNSAFE</span><span class="sxs-lookup"><span data-stu-id="249d6-157">UNSAFE</span></span>  
 <span data-ttu-id="249d6-158">UNSAFE 允许程序集不受限制地访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部和外部的资源。</span><span class="sxs-lookup"><span data-stu-id="249d6-158">UNSAFE allows assemblies unrestricted access to resources, both within and outside [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="249d6-159">从 `UNSAFE` 程序集内部执行代码时也可以调用非托管代码。</span><span class="sxs-lookup"><span data-stu-id="249d6-159">Code executing from within an `UNSAFE` assembly can also call unmanaged code.</span></span>  
  
 <span data-ttu-id="249d6-160">`UNSAFE` 程序集被授予 `FullTrust`。</span><span class="sxs-lookup"><span data-stu-id="249d6-160">`UNSAFE` assemblies are given `FullTrust`.</span></span>  
  
> [!IMPORTANT]  
>  <span data-ttu-id="249d6-161">对于执行计算和数据管理任务而无需访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 外部资源的程序集，`SAFE` 是推荐的权限设置。</span><span class="sxs-lookup"><span data-stu-id="249d6-161">`SAFE` is the recommended permission setting for assemblies that perform computation and data management tasks without accessing resources outside [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="249d6-162">`EXTERNAL_ACCESS`默认情况下，程序集作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户执行， `EXTERNAL_ACCESS` 只应将执行权限提供给受信任的登录名，以作为服务帐户运行。</span><span class="sxs-lookup"><span data-stu-id="249d6-162">`EXTERNAL_ACCESS` assemblies by default execute as the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] service account, permission to execute `EXTERNAL_ACCESS` should only be given to logins trusted to run as the service account.</span></span> <span data-ttu-id="249d6-163">从安全角度来看，`EXTERNAL_ACCESS` 和 `UNSAFE` 程序集是等同的。</span><span class="sxs-lookup"><span data-stu-id="249d6-163">From a security perspective, `EXTERNAL_ACCESS` and `UNSAFE` assemblies are identical.</span></span> <span data-ttu-id="249d6-164">但是，`EXTERNAL_ACCESS` 程序集提供了 `UNSAFE` 程序集所不具备的各种可靠性和健壮性保护。</span><span class="sxs-lookup"><span data-stu-id="249d6-164">However, `EXTERNAL_ACCESS` assemblies provide various reliability and robustness protections that are not in `UNSAFE` assemblies.</span></span> <span data-ttu-id="249d6-165">指定将 `UNSAFE` 允许程序集中的代码对执行非法操作 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="249d6-165">Specifying `UNSAFE` allows the code in the assembly to perform illegal operations against the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="249d6-166">有关在中创建 CLR 程序集的详细信息 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请参阅[管理 Clr 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。</span><span class="sxs-lookup"><span data-stu-id="249d6-166">For more information about creating CLR assemblies in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], see [Managing CLR Integration Assemblies](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).</span></span>  
  
## <a name="accessing-external-resources"></a><span data-ttu-id="249d6-167">访问外部资源</span><span class="sxs-lookup"><span data-stu-id="249d6-167">Accessing External Resources</span></span>  
 <span data-ttu-id="249d6-168">如果用户定义类型 (UDT)、存储过程或其他类型的构造程序集均使用 `SAFE` 权限集进行注册，则在构造中执行的托管代码将无法访问外部资源。</span><span class="sxs-lookup"><span data-stu-id="249d6-168">If a user-defined type (UDT), stored procedure, or other type of construct assembly is registered with the `SAFE` permission set, then managed code executing in the construct is unable to access external resources.</span></span> <span data-ttu-id="249d6-169">但是，如果指定了 `EXTERNAL_ACCESS` 或 `UNSAFE` 权限集，并且托管代码尝试访问外部资源，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会应用以下规则：</span><span class="sxs-lookup"><span data-stu-id="249d6-169">However, if either the `EXTERNAL_ACCESS` or `UNSAFE` permission sets are specified, and managed code attempts to access external resources, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applies the following rules:</span></span>  
  
|<span data-ttu-id="249d6-170">如果</span><span class="sxs-lookup"><span data-stu-id="249d6-170">If</span></span>|<span data-ttu-id="249d6-171">Then</span><span class="sxs-lookup"><span data-stu-id="249d6-171">Then</span></span>|  
|--------|----------|  
|<span data-ttu-id="249d6-172">执行上下文与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名相对应。</span><span class="sxs-lookup"><span data-stu-id="249d6-172">The execution context corresponds to a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] login.</span></span>|<span data-ttu-id="249d6-173">拒绝访问外部资源的尝试并引发一个安全异常。</span><span class="sxs-lookup"><span data-stu-id="249d6-173">Attempts to access external resources are denied and a security exception is raised.</span></span>|  
|<span data-ttu-id="249d6-174">执行上下文与 Windows 登录名相对应并且执行上下文为原始调用方。</span><span class="sxs-lookup"><span data-stu-id="249d6-174">The execution context corresponds to a Windows login and the execution context is the original caller.</span></span>|<span data-ttu-id="249d6-175">在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的安全上下文下访问外部资源。</span><span class="sxs-lookup"><span data-stu-id="249d6-175">The external resource is accessed under the security context of the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] service account.</span></span>|  
|<span data-ttu-id="249d6-176">调用方不是原始调用方。</span><span class="sxs-lookup"><span data-stu-id="249d6-176">The caller is not the original caller.</span></span>|<span data-ttu-id="249d6-177">拒绝访问并引发一个安全异常。</span><span class="sxs-lookup"><span data-stu-id="249d6-177">Access is denied and a security exception is raised.</span></span>|  
|<span data-ttu-id="249d6-178">执行上下文与 Windows 登录名相对应并且执行上下文是原始调用方，而该调用方已被模拟。</span><span class="sxs-lookup"><span data-stu-id="249d6-178">The execution context corresponds to a Windows login and the execution context is the original caller and the caller has been impersonated.</span></span>|<span data-ttu-id="249d6-179">访问使用调用方安全上下文，而非服务帐户。</span><span class="sxs-lookup"><span data-stu-id="249d6-179">Access uses the caller security context; not the service account.</span></span>|  
  
## <a name="permission-set-summary"></a><span data-ttu-id="249d6-180">权限集汇总</span><span class="sxs-lookup"><span data-stu-id="249d6-180">Permission Set Summary</span></span>  
 <span data-ttu-id="249d6-181">下表总结了授予 `SAFE`、`EXTERNAL_ACCESS` 和 `UNSAFE` 权限集的权限以及为其设定的限制。</span><span class="sxs-lookup"><span data-stu-id="249d6-181">The following chart summarizes the restrictions and permissions granted to the `SAFE`, `EXTERNAL_ACCESS`, and `UNSAFE` permission sets.</span></span>  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|<span data-ttu-id="249d6-182">仅执行</span><span class="sxs-lookup"><span data-stu-id="249d6-182">Execute only</span></span>|<span data-ttu-id="249d6-183">执行和访问外部资源</span><span class="sxs-lookup"><span data-stu-id="249d6-183">Execute + access to external resources</span></span>|<span data-ttu-id="249d6-184">不受限制（包括 P/Invoke）</span><span class="sxs-lookup"><span data-stu-id="249d6-184">Unrestricted (including P/Invoke)</span></span>|  
|`Programming model restrictions`|<span data-ttu-id="249d6-185">是</span><span class="sxs-lookup"><span data-stu-id="249d6-185">Yes</span></span>|<span data-ttu-id="249d6-186">是</span><span class="sxs-lookup"><span data-stu-id="249d6-186">Yes</span></span>|<span data-ttu-id="249d6-187">无限制</span><span class="sxs-lookup"><span data-stu-id="249d6-187">No restrictions</span></span>|  
|`Verifiability requirement`|<span data-ttu-id="249d6-188">是</span><span class="sxs-lookup"><span data-stu-id="249d6-188">Yes</span></span>|<span data-ttu-id="249d6-189">是</span><span class="sxs-lookup"><span data-stu-id="249d6-189">Yes</span></span>|<span data-ttu-id="249d6-190">否</span><span class="sxs-lookup"><span data-stu-id="249d6-190">No</span></span>|  
|`Local data access`|<span data-ttu-id="249d6-191">是</span><span class="sxs-lookup"><span data-stu-id="249d6-191">Yes</span></span>|<span data-ttu-id="249d6-192">是</span><span class="sxs-lookup"><span data-stu-id="249d6-192">Yes</span></span>|<span data-ttu-id="249d6-193">是</span><span class="sxs-lookup"><span data-stu-id="249d6-193">Yes</span></span>|  
|`Ability to call native code`|<span data-ttu-id="249d6-194">否</span><span class="sxs-lookup"><span data-stu-id="249d6-194">No</span></span>|<span data-ttu-id="249d6-195">否</span><span class="sxs-lookup"><span data-stu-id="249d6-195">No</span></span>|<span data-ttu-id="249d6-196">是</span><span class="sxs-lookup"><span data-stu-id="249d6-196">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="249d6-197">另请参阅</span><span class="sxs-lookup"><span data-stu-id="249d6-197">See Also</span></span>  
 <span data-ttu-id="249d6-198">[CLR 集成安全性](clr-integration-security.md) </span><span class="sxs-lookup"><span data-stu-id="249d6-198">[CLR Integration Security](clr-integration-security.md) </span></span>  
 <span data-ttu-id="249d6-199">[宿主保护属性和 CLR 集成编程](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md) </span><span class="sxs-lookup"><span data-stu-id="249d6-199">[Host Protection Attributes and CLR Integration Programming](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md) </span></span>  
 <span data-ttu-id="249d6-200">[CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) </span><span class="sxs-lookup"><span data-stu-id="249d6-200">[CLR Integration Programming Model Restrictions](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) </span></span>  
 [<span data-ttu-id="249d6-201">CLR 宿主环境</span><span class="sxs-lookup"><span data-stu-id="249d6-201">CLR Hosted Environment</span></span>](../clr-integration-architecture-clr-hosted-environment.md)  
  
  