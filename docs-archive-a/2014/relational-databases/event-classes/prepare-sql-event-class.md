---
title: Prepare SQL 事件类 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Prepare SQL event class
ms.assetid: 4ff3aa04-0f1a-49e2-a43d-7251bab4a458
author: stevestein
ms.author: sstein
ms.openlocfilehash: aaeaa6aee7fa61527180290ac22a584ed22f5178
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588507"
---
# <a name="prepare-sql-event-class"></a><span data-ttu-id="8b8f9-102">Prepare SQL 事件类</span><span class="sxs-lookup"><span data-stu-id="8b8f9-102">Prepare SQL Event Class</span></span>
  <span data-ttu-id="8b8f9-103">Prepare SQL 事件类指示 SqlClient、ODBC、OLE DB 或 DB-Library 已准备了 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以供使用。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-103">The Prepare SQL event class indicates that SqlClient, ODBC, OLE DB, or DB-Library has prepared a [!INCLUDE[tsql](../../includes/tsql-md.md)] statement or statements for use.</span></span>  
  
## <a name="prepare-sql-event-class-data-columns"></a><span data-ttu-id="8b8f9-104">Prepare SQL 事件类的数据列</span><span class="sxs-lookup"><span data-stu-id="8b8f9-104">Prepare SQL Event Class Data Columns</span></span>  
  
|<span data-ttu-id="8b8f9-105">数据列名称</span><span class="sxs-lookup"><span data-stu-id="8b8f9-105">Data column name</span></span>|<span data-ttu-id="8b8f9-106">数据类型</span><span class="sxs-lookup"><span data-stu-id="8b8f9-106">Data type</span></span>|<span data-ttu-id="8b8f9-107">说明</span><span class="sxs-lookup"><span data-stu-id="8b8f9-107">Description</span></span>|<span data-ttu-id="8b8f9-108">列 ID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-108">Column ID</span></span>|<span data-ttu-id="8b8f9-109">可筛选</span><span class="sxs-lookup"><span data-stu-id="8b8f9-109">Filterable</span></span>|  
|----------------------|---------------|-----------------|---------------|----------------|  
|<span data-ttu-id="8b8f9-110">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-110">ApplicationName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-111">客户端应用程序的名称，该客户端应用程序创建了指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的连接。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-111">Name of the client application that created the connection to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="8b8f9-112">此列由应用程序传递的值填充，而不是由所显示的程序名填充。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-112">This column is populated with the values passed by the application rather than the displayed name of the program.</span></span>|<span data-ttu-id="8b8f9-113">10</span><span class="sxs-lookup"><span data-stu-id="8b8f9-113">10</span></span>|<span data-ttu-id="8b8f9-114">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-114">Yes</span></span>|  
|<span data-ttu-id="8b8f9-115">ClientProcessID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-115">ClientProcessID</span></span>|`int`|<span data-ttu-id="8b8f9-116">主机为运行该客户端应用程序的进程分配的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-116">ID assigned by the host computer to the process where the client application is running.</span></span> <span data-ttu-id="8b8f9-117">如果客户端提供了客户端进程 ID，则填充此数据列。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-117">This data column is populated if the client provides the client process ID.</span></span>|<span data-ttu-id="8b8f9-118">9</span><span class="sxs-lookup"><span data-stu-id="8b8f9-118">9</span></span>|<span data-ttu-id="8b8f9-119">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-119">Yes</span></span>|  
|<span data-ttu-id="8b8f9-120">DatabaseID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-120">DatabaseID</span></span>|`int`|<span data-ttu-id="8b8f9-121">由 USE *database* 语句指定的数据库的 ID；如果未对给定实例发出 USE *database* 语句，则为默认数据库的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-121">ID of the database specified by the USE *database* statement or the default database if no USE *database* statement has been issued for a given instance.</span></span> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] <span data-ttu-id="8b8f9-122">如果在跟踪中捕获 ServerName 数据列而且服务器可用，则将显示数据库名。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-122">displays the name of the database if the ServerName data column is captured in the trace and the server is available.</span></span> <span data-ttu-id="8b8f9-123">可使用 DB_ID 函数来确定数据库的值。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-123">Determine the value for a database by using the DB_ID function.</span></span>|<span data-ttu-id="8b8f9-124">3</span><span class="sxs-lookup"><span data-stu-id="8b8f9-124">3</span></span>|<span data-ttu-id="8b8f9-125">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-125">Yes</span></span>|  
|<span data-ttu-id="8b8f9-126">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-126">DatabaseName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-127">正在其中运行用户语句的数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-127">Name of the database in which the user statement is running.</span></span>|<span data-ttu-id="8b8f9-128">35</span><span class="sxs-lookup"><span data-stu-id="8b8f9-128">35</span></span>|<span data-ttu-id="8b8f9-129">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-129">Yes</span></span>|  
|<span data-ttu-id="8b8f9-130">EventClass</span><span class="sxs-lookup"><span data-stu-id="8b8f9-130">EventClass</span></span>|`int`|<span data-ttu-id="8b8f9-131">事件类型 = 71。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-131">Type of event = 71.</span></span>|<span data-ttu-id="8b8f9-132">27</span><span class="sxs-lookup"><span data-stu-id="8b8f9-132">27</span></span>|<span data-ttu-id="8b8f9-133">否</span><span class="sxs-lookup"><span data-stu-id="8b8f9-133">No</span></span>|  
|<span data-ttu-id="8b8f9-134">EventSequence</span><span class="sxs-lookup"><span data-stu-id="8b8f9-134">EventSequence</span></span>|`int`|<span data-ttu-id="8b8f9-135">给定事件在请求中的顺序。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-135">Sequence of a given event within the request.</span></span>|<span data-ttu-id="8b8f9-136">51</span><span class="sxs-lookup"><span data-stu-id="8b8f9-136">51</span></span>|<span data-ttu-id="8b8f9-137">否</span><span class="sxs-lookup"><span data-stu-id="8b8f9-137">No</span></span>|  
|<span data-ttu-id="8b8f9-138">GroupID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-138">GroupID</span></span>|`int`|<span data-ttu-id="8b8f9-139">在其中激发 SQL 跟踪事件的工作负荷组的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-139">ID of the workload group where the SQL Trace event fires.</span></span>|<span data-ttu-id="8b8f9-140">66</span><span class="sxs-lookup"><span data-stu-id="8b8f9-140">66</span></span>|<span data-ttu-id="8b8f9-141">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-141">Yes</span></span>|  
|<span data-ttu-id="8b8f9-142">Handle</span><span class="sxs-lookup"><span data-stu-id="8b8f9-142">Handle</span></span>|`int`|<span data-ttu-id="8b8f9-143">准备好的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的句柄。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-143">Handle of the prepared [!INCLUDE[tsql](../../includes/tsql-md.md)] statement.</span></span>|<span data-ttu-id="8b8f9-144">33</span><span class="sxs-lookup"><span data-stu-id="8b8f9-144">33</span></span>|<span data-ttu-id="8b8f9-145">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-145">Yes</span></span>|  
|<span data-ttu-id="8b8f9-146">HostName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-146">HostName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-147">正在运行客户端的计算机的名称。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-147">Name of the computer on which the client is running.</span></span> <span data-ttu-id="8b8f9-148">如果客户端提供了主机名，则填充此数据列。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-148">This data column is populated if the host name is provided by the client.</span></span> <span data-ttu-id="8b8f9-149">若要确定主机名，请使用 HOST_NAME 函数。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-149">To determine the host name, use the HOST_NAME function.</span></span>|<span data-ttu-id="8b8f9-150">8</span><span class="sxs-lookup"><span data-stu-id="8b8f9-150">8</span></span>|<span data-ttu-id="8b8f9-151">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-151">Yes</span></span>|  
|<span data-ttu-id="8b8f9-152">IsSystem</span><span class="sxs-lookup"><span data-stu-id="8b8f9-152">IsSystem</span></span>|`int`|<span data-ttu-id="8b8f9-153">指示事件是发生在系统进程中还是发生在用户进程中。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-153">Indicates whether the event occurred on a system process or a user process.</span></span> <span data-ttu-id="8b8f9-154">1 = 系统，0 = 用户。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-154">1 = system, 0 = user.</span></span>|<span data-ttu-id="8b8f9-155">60</span><span class="sxs-lookup"><span data-stu-id="8b8f9-155">60</span></span>|<span data-ttu-id="8b8f9-156">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-156">Yes</span></span>|  
|<span data-ttu-id="8b8f9-157">LoginName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-157">LoginName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-158">用户的登录名（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全登录名或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登录凭据，格式为“DOMAIN\username”）。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-158">Name of the login of the user (either [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] security login or the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows login credentials in the form of DOMAIN\username).</span></span>|<span data-ttu-id="8b8f9-159">11</span><span class="sxs-lookup"><span data-stu-id="8b8f9-159">11</span></span>|<span data-ttu-id="8b8f9-160">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-160">Yes</span></span>|  
|<span data-ttu-id="8b8f9-161">LoginSid</span><span class="sxs-lookup"><span data-stu-id="8b8f9-161">LoginSid</span></span>|`image`|<span data-ttu-id="8b8f9-162">登录用户的安全标识号 (SID)。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-162">Security identification number (SID) of the logged-in user.</span></span> <span data-ttu-id="8b8f9-163">您可以在 sys.server_principals 目录视图中找到此信息。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-163">You can find this information in the sys.server_principals catalog view.</span></span> <span data-ttu-id="8b8f9-164">服务器中的每个登录名都具有唯一的 SID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-164">Each SID is unique for each login in the server.</span></span>|<span data-ttu-id="8b8f9-165">41</span><span class="sxs-lookup"><span data-stu-id="8b8f9-165">41</span></span>|<span data-ttu-id="8b8f9-166">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-166">Yes</span></span>|  
|<span data-ttu-id="8b8f9-167">NTDomainName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-167">NTDomainName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-168">用户所属的 Windows 域。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-168">Windows domain to which the user belongs.</span></span>|<span data-ttu-id="8b8f9-169">7</span><span class="sxs-lookup"><span data-stu-id="8b8f9-169">7</span></span>|<span data-ttu-id="8b8f9-170">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-170">Yes</span></span>|  
|<span data-ttu-id="8b8f9-171">NTUserName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-171">NTUserName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-172">Windows 用户名。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-172">Windows user name.</span></span>|<span data-ttu-id="8b8f9-173">6</span><span class="sxs-lookup"><span data-stu-id="8b8f9-173">6</span></span>|<span data-ttu-id="8b8f9-174">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-174">Yes</span></span>|  
|<span data-ttu-id="8b8f9-175">RequestID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-175">RequestID</span></span>|`int`|<span data-ttu-id="8b8f9-176">包含该语句的请求的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-176">ID of the request containing the statement.</span></span>|<span data-ttu-id="8b8f9-177">49</span><span class="sxs-lookup"><span data-stu-id="8b8f9-177">49</span></span>|<span data-ttu-id="8b8f9-178">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-178">Yes</span></span>|  
|<span data-ttu-id="8b8f9-179">ServerName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-179">ServerName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-180">所跟踪的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-180">Name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] being traced.</span></span>|<span data-ttu-id="8b8f9-181">26</span><span class="sxs-lookup"><span data-stu-id="8b8f9-181">26</span></span>|<span data-ttu-id="8b8f9-182">否</span><span class="sxs-lookup"><span data-stu-id="8b8f9-182">No</span></span>|  
|<span data-ttu-id="8b8f9-183">SessionLoginName</span><span class="sxs-lookup"><span data-stu-id="8b8f9-183">SessionLoginName</span></span>|`nvarchar`|<span data-ttu-id="8b8f9-184">发起会话的用户的登录名。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-184">Login name of the user who originated the session.</span></span> <span data-ttu-id="8b8f9-185">例如，如果您使用 Login1 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，再以 Login2 的身份执行语句，则 SessionLoginName 将显示 Login1，而 LoginName 将显示 Login2。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-185">For example, if you connect to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] using Login1 and execute a statement as Login2, SessionLoginName shows Login1 and LoginName shows Login2.</span></span> <span data-ttu-id="8b8f9-186">此列将同时显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和 Windows 登录名。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-186">This column displays both [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and Windows logins.</span></span>|<span data-ttu-id="8b8f9-187">64</span><span class="sxs-lookup"><span data-stu-id="8b8f9-187">64</span></span>|<span data-ttu-id="8b8f9-188">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-188">Yes</span></span>|  
|<span data-ttu-id="8b8f9-189">SPID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-189">SPID</span></span>|`int`|<span data-ttu-id="8b8f9-190">发生该事件的会话的 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-190">ID of the session on which the event occurred.</span></span>|<span data-ttu-id="8b8f9-191">12</span><span class="sxs-lookup"><span data-stu-id="8b8f9-191">12</span></span>|<span data-ttu-id="8b8f9-192">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-192">Yes</span></span>|  
|<span data-ttu-id="8b8f9-193">StartTime</span><span class="sxs-lookup"><span data-stu-id="8b8f9-193">StartTime</span></span>|`datetime`|<span data-ttu-id="8b8f9-194">该事件（如果存在）的启动时间。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-194">Time at which the event started, if available.</span></span>|<span data-ttu-id="8b8f9-195">14</span><span class="sxs-lookup"><span data-stu-id="8b8f9-195">14</span></span>|<span data-ttu-id="8b8f9-196">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-196">Yes</span></span>|  
|<span data-ttu-id="8b8f9-197">TransactionID</span><span class="sxs-lookup"><span data-stu-id="8b8f9-197">TransactionID</span></span>|`bigint`|<span data-ttu-id="8b8f9-198">系统分配的事务 ID。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-198">System-assigned ID of the transaction.</span></span>|<span data-ttu-id="8b8f9-199">4</span><span class="sxs-lookup"><span data-stu-id="8b8f9-199">4</span></span>|<span data-ttu-id="8b8f9-200">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-200">Yes</span></span>|  
|<span data-ttu-id="8b8f9-201">XactSequence</span><span class="sxs-lookup"><span data-stu-id="8b8f9-201">XactSequence</span></span>|`bigint`|<span data-ttu-id="8b8f9-202">用于说明当前事务的标记。</span><span class="sxs-lookup"><span data-stu-id="8b8f9-202">Token used to describe the current transaction.</span></span>|<span data-ttu-id="8b8f9-203">50</span><span class="sxs-lookup"><span data-stu-id="8b8f9-203">50</span></span>|<span data-ttu-id="8b8f9-204">是</span><span class="sxs-lookup"><span data-stu-id="8b8f9-204">Yes</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="8b8f9-205">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8b8f9-205">See Also</span></span>  
 [<span data-ttu-id="8b8f9-206">sp_trace_setevent (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="8b8f9-206">sp_trace_setevent &#40;Transact-SQL&#41;</span></span>](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  