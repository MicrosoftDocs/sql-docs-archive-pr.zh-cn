---
title: FileTable (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2016
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6c0a38f0e947b0c4f68a49e13a40071f6a30cd07
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692966"
---
# <a name="filetables-sql-server"></a><span data-ttu-id="a5cb2-102">FileTable (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="a5cb2-102">FileTables (SQL Server)</span></span>
  <span data-ttu-id="a5cb2-103">FileTable 功能为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的文件数据提供对 Windows 文件命名空间的支持以及与 Windows 应用程序的兼容性支持。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-103">The FileTable feature brings support for the Windows file namespace and compatibility with Windows applications to the file data stored in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="a5cb2-104">FileTable 使得应用程序可以集成其存储和数据管理组件，可对非结构化数据和元数据提供集成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务（包括全文搜索和语义搜索）。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-104">FileTable lets an application integrate its storage and data management components, and provides integrated [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services - including full-text search and semantic search - over unstructured data and metadata.</span></span>  
  
 <span data-ttu-id="a5cb2-105">换言之，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将文件和文档存储在称作 FileTable 的特别的表中，但是从 Windows 应用程序访问它们，就好像它们存储在文件系统中，而不必对您的客户端应用程序进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-105">In other words, you can store files and documents in special tables in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] called FileTables, but access them from Windows applications as if they were stored in the file system, without making any changes to your client applications.</span></span>  
  
 <span data-ttu-id="a5cb2-106">FileTable 功能是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM 技术的基础上生成的。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-106">The FileTable feature builds on top of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM technology.</span></span> <span data-ttu-id="a5cb2-107">有关 FILESTREAM 的详细信息，请参阅 [FILESTREAM (SQL Server)](filestream-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-107">To learn more about FILESTREAM, see [FILESTREAM &#40;SQL Server&#41;](filestream-sql-server.md).</span></span>  
  
##  <a name="benefits-of-the-filetable-feature"></a><a name="Goals"></a> <span data-ttu-id="a5cb2-108">FileTable 功能的优点</span><span class="sxs-lookup"><span data-stu-id="a5cb2-108">Benefits of the FileTable Feature</span></span>  
 <span data-ttu-id="a5cb2-109">FileTable 功能的目标包括：</span><span class="sxs-lookup"><span data-stu-id="a5cb2-109">The goals of the FileTable feature include the following:</span></span>  
  
-   <span data-ttu-id="a5cb2-110">针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储的文件数据的 Windows API 兼容性。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-110">Windows API compatibility for file data stored within a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.</span></span> <span data-ttu-id="a5cb2-111">Windows API 兼容性包括以下方面：</span><span class="sxs-lookup"><span data-stu-id="a5cb2-111">Windows API compatibility includes the following:</span></span>  
  
    -   <span data-ttu-id="a5cb2-112">对 FILESTREAM 数据的非事务性流式访问和就地更新。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-112">Non-transactional streaming access and in-place updates to FILESTREAM data.</span></span>  
  
    -   <span data-ttu-id="a5cb2-113">目录和文件的分层命名空间。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-113">A hierarchical namespace of directories and files.</span></span>  
  
    -   <span data-ttu-id="a5cb2-114">文件属性的存储，如创建日期和修改日期。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-114">Storage of file attributes, such as created date and modified date.</span></span>  
  
    -   <span data-ttu-id="a5cb2-115">对 Windows 文件和目录管理 API 的支持。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-115">Support for Windows file and directory management APIs.</span></span>  
  
-   <span data-ttu-id="a5cb2-116">与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的兼容性包括针对 FILESTREAM 和文件属性数据的管理工具、服务和关系查询功能。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-116">Compatibility with other [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] features including management tools, services, and relational query capabilities over FILESTREAM and file attribute data.</span></span>  
  
 <span data-ttu-id="a5cb2-117">这样，FileTable 将消除使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来存储和管理非结构化数据的一个巨大障碍，这些数据目前作为文件存储在文件服务器上。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-117">Thus FileTables remove a significant barrier to the use of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for the storage and management of unstructured data that is currently residing as files on file servers.</span></span> <span data-ttu-id="a5cb2-118">企业可以将这些数据从文件服务器移到 FileTable，以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的集成管理和服务。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-118">Enterprises can move this data from file servers into FileTables to take advantage of integrated administration and services provided by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].</span></span> <span data-ttu-id="a5cb2-119">同时，它们可以保持现有 Windows 应用程序的 Windows 应用程序兼容性，将这些数据视为文件系统中的文件。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-119">At the same time, they can maintain Windows application compatibility for their existing Windows applications that see this data as files in the file system.</span></span>  
    
##  <a name="what-is-a-filetable"></a><a name="Description"></a> <span data-ttu-id="a5cb2-120">什么是 FileTable？</span><span class="sxs-lookup"><span data-stu-id="a5cb2-120">What Is a FileTable?</span></span>  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] <span data-ttu-id="a5cb2-121">对于需要在数据库中存储文件和目录的应用程序，借助 Windows API 兼容性和非事务性访问，提供一种特殊的 **文件表**，也称为 **FileTable**。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-121">provides a special **table of files**, also referred to as a **FileTable**, for applications that require file and directory storage in the database, with Windows API compatibility and non-transactional access.</span></span> <span data-ttu-id="a5cb2-122">FileTable 是一种专用的用户表，它包含存储 FILESTREAM 数据的预定义架构以及文件和目录层次结构信息、文件属性。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-122">A FileTable is a specialized user table with a pre-defined schema that stores FILESTREAM data, as well as file and directory hierarchy information and file attributes.</span></span>  
  
 <span data-ttu-id="a5cb2-123">FileTable 提供以下功能：</span><span class="sxs-lookup"><span data-stu-id="a5cb2-123">A FileTable provides the following functionality:</span></span>  
  
-   <span data-ttu-id="a5cb2-124">FileTable 表示目录和文件的一种层次结构。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-124">A FileTable represents a hierarchy of directories and files.</span></span> <span data-ttu-id="a5cb2-125">它为目录和其中所含的文件存储与该层次结构中所有节点有关的数据。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-125">It stores data related to all the nodes in that hierarchy, for both directories and the files they contain.</span></span> <span data-ttu-id="a5cb2-126">该层次结构以您创建 FileTable 时指定的根目录为起点。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-126">This hierarchy starts from a root directory that you specify when you create the FileTable.</span></span>  
  
-   <span data-ttu-id="a5cb2-127">FileTable 中的每行表示一个文件或目录。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-127">Every row in a FileTable represents a file or a directory.</span></span>  
  
-   <span data-ttu-id="a5cb2-128">每行包含以下项：</span><span class="sxs-lookup"><span data-stu-id="a5cb2-128">Every row contains the following items.</span></span> <span data-ttu-id="a5cb2-129">有关 FileTable 的架构的详细信息，请参阅 [FileTable Schema](filetable-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-129">For more information about the schema of a FileTable, see [FileTable Schema](filetable-schema.md).</span></span>  
  
    -   <span data-ttu-id="a5cb2-130">流数据的**file_stream** 列和 **stream_id** (GUID) 标识符。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-130">A**file_stream** column for stream data and a **stream_id** (GUID) identifier.</span></span> <span data-ttu-id="a5cb2-131">（ **file_stream** 列对于目录为 NULL。）</span><span class="sxs-lookup"><span data-stu-id="a5cb2-131">(The **file_stream** column is NULL for a directory.)</span></span>  
  
    -   <span data-ttu-id="a5cb2-132">用于表示和维护文件以及目录层次结构的 **path_locator** 列和 **parent_path_locator** 列。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-132">Both **path_locator** and **parent_path_locator** columns for representing and maintaining the file and directory hierarchy.</span></span>  
  
    -   <span data-ttu-id="a5cb2-133">10 个文件属性，如可用于文件 I/O API 的创建日期和修改日期。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-133">10 file attributes such as created date and modified date that are useful with file I/O APIs.</span></span>  
  
    -   <span data-ttu-id="a5cb2-134">支持针对文件和文档的全文搜索和语义搜索的类型列。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-134">A type column that supports full-text search and semantic search over files and documents.</span></span>  
  
-   <span data-ttu-id="a5cb2-135">FileTable 强制执行某些系统定义的约束和触发器以维护文件命名空间语义。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-135">A FileTable enforces certain system-defined constraints and triggers to maintain file namespace semantics.</span></span>  
  
-   <span data-ttu-id="a5cb2-136">针对非事务性访问配置数据库时，在为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置的 FILESTREAM 共享区下公开在 FileTable 中表示的文件和目录层次结构。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-136">When the database is configured for non-transactional access, the file and directory hierarchy represented in the FileTable is exposed under the FILESTREAM share configured for the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.</span></span> <span data-ttu-id="a5cb2-137">这为 Windows 应用程序提供了文件系统访问方法。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-137">This provides file system access for Windows applications.</span></span>  
  
 <span data-ttu-id="a5cb2-138">FileTable 的一些其他特性包括：</span><span class="sxs-lookup"><span data-stu-id="a5cb2-138">Some additional characteristics of FileTables include the following:</span></span>  
  
-   <span data-ttu-id="a5cb2-139">存储在 FileTable 中的文件和目录数据通过用于非事务性文件访问的 Windows 共享区（针对基于 Windows API 的应用程序）公开。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-139">The file and directory data stored in a FileTable is exposed through a Windows share for non-transactional file access for Windows API based applications.</span></span> <span data-ttu-id="a5cb2-140">对于 Windows 应用程序，这看起来像一个包含文件和目录的普通共享区。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-140">For a Windows application, this looks like a normal share with its files and directories.</span></span> <span data-ttu-id="a5cb2-141">应用程序可使用一组广泛的 Windows API，用于对此共享区下的文件和目录进行管理。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-141">Applications can use a rich set of Windows APIs to manage the files and directories under this share.</span></span>  
  
-   <span data-ttu-id="a5cb2-142">通过该共享区公开的目录层次结构是一个在 FileTable 中维护的纯逻辑目录结构。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-142">The directory hierarchy surfaced through the share is a purely logical directory structure that is maintained within the FileTable.</span></span>  
  
-   <span data-ttu-id="a5cb2-143">通过该 Windows 共享区对创建或更改文件/目录的调用被 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件拦截并在 FileTable 中的相应关系数据中得到反映。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-143">Calls to create or change a file or directory through the Windows share are intercepted by a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] component and reflected in the corresponding relational data in the FileTable.</span></span>  
  
-   <span data-ttu-id="a5cb2-144">Windows API 操作本质上是非事务性的，并不与用户事务关联。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-144">Windows API operations are non-transactional in nature, and are not associated with user transactions.</span></span> <span data-ttu-id="a5cb2-145">但是，完全支持对存储在 FileTable 中的 FILESTREAM 数据的事务性访问，就像对待常规表中的任何 FILESTREAM 列一样。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-145">However, transactional access to FILESTREAM data stored in a FileTable is fully supported, as is the case for any FILESTREAM column in a regular table.</span></span>  
  
-   <span data-ttu-id="a5cb2-146">还可以通过常规 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问来查询和更新 FileTable。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-146">FileTables can also be queried and updated through normal [!INCLUDE[tsql](../../includes/tsql-md.md)] access.</span></span> <span data-ttu-id="a5cb2-147">它们还与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具和诸如备份的功能集成。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-147">They are also integrated with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] management tools, and features such as backup.</span></span>  
  
  
##  <a name="additional-considerations-for-using-filetables"></a><a name="additional"></a> <span data-ttu-id="a5cb2-148">使用 FileTable 的其他注意事项</span><span class="sxs-lookup"><span data-stu-id="a5cb2-148">Additional Considerations for Using FileTables</span></span>  
  
###  <a name="administrative-considerations"></a><a name="DBA"></a> <span data-ttu-id="a5cb2-149">管理注意事项</span><span class="sxs-lookup"><span data-stu-id="a5cb2-149">Administrative Considerations</span></span>  
 <span data-ttu-id="a5cb2-150">**关于 FILESTREAM 和 FileTable**</span><span class="sxs-lookup"><span data-stu-id="a5cb2-150">**About FILESTREAM and FileTables**</span></span>  
  
-   <span data-ttu-id="a5cb2-151">独立于 FILESTREAM 配置 FileTable。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-151">You configure FileTables separately from FILESTREAM.</span></span> <span data-ttu-id="a5cb2-152">因此，您可以继续使用 FILESTREAM 功能，而不启用非事务性访问或创建 FileTable。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-152">Therefore you can continue to use the FILESTREAM feature without enabling non-transactional access or creating FileTables.</span></span>  
  
-   <span data-ttu-id="a5cb2-153">除了通过 FileTable，没有对 FILESTREAM 数据的其他非事务性访问。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-153">There is no non-transactional access to FILESTREAM data except through FileTables.</span></span> <span data-ttu-id="a5cb2-154">因此，在启用非事务性访问时并不会影响现有的 FILESTREAM 列和应用程序的行为。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-154">Therefore, when you enable non-transactional access, the behavior of existing FILESTREAM columns and applications is not affected.</span></span>  
  
 <span data-ttu-id="a5cb2-155">**关于 FileTable 和非事务性访问**</span><span class="sxs-lookup"><span data-stu-id="a5cb2-155">**About FileTables and non-transactional access**</span></span>  
  
-   <span data-ttu-id="a5cb2-156">可以在数据库级别启用或禁用非事务性访问。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-156">You can enable or disable non-transactional access at the database level.</span></span>  
  
-   <span data-ttu-id="a5cb2-157">您可以通过将非事务性访问关闭或者启用只读或完全读/写访问，在数据库级别配置或优化非事务性访问。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-157">You can configure or fine-tune non-transactional access at the database level by turning it off, or by enabling read only or full read/write access.</span></span>  
  
  
###  <a name="filetables-do-not-support-memory-mapped-files"></a><a name="memory"></a> <span data-ttu-id="a5cb2-158">FileTable 不支持内存映射文件</span><span class="sxs-lookup"><span data-stu-id="a5cb2-158">FileTables Do Not Support Memory-Mapped Files</span></span>  
 <span data-ttu-id="a5cb2-159">FileTable 不支持内存映射文件。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-159">FileTables do not support memory-mapped files.</span></span> <span data-ttu-id="a5cb2-160">“记事本”和“画图”是两个常见的使用内存映射文件的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-160">Notepad and Paint are two common examples of applications that use memory-mapped files.</span></span> <span data-ttu-id="a5cb2-161">不能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的计算机上使用这些应用程序来打开存储在 FileTable 中的文件。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-161">You cannot use these applications on the same computer as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to open files that are stored in a FileTable.</span></span> <span data-ttu-id="a5cb2-162">但是，可以从远程计算机使用这些应用程序来打开存储在 FileTable 中的文件，因为在这些情况下不使用内存映射功能。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-162">However you can use these applications from a remote computer to open files that are stored in a FileTable, because in these circumstances the memory-mapping feature is not used.</span></span>  
  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> <span data-ttu-id="a5cb2-163">相关任务</span><span class="sxs-lookup"><span data-stu-id="a5cb2-163">Related Tasks</span></span>  
 [<span data-ttu-id="a5cb2-164">启用 FileTable 的先决条件</span><span class="sxs-lookup"><span data-stu-id="a5cb2-164">Enable the Prerequisites for FileTable</span></span>](enable-the-prerequisites-for-filetable.md)  
 <span data-ttu-id="a5cb2-165">介绍如何启用创建和使用 FileTable 的先决条件。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-165">Describes how to enable the prerequisites for creating and using FileTables.</span></span>  
  
 [<span data-ttu-id="a5cb2-166">创建、更改和删除 FileTable</span><span class="sxs-lookup"><span data-stu-id="a5cb2-166">Create, Alter, and Drop FileTables</span></span>](create-alter-and-drop-filetables.md)  
 <span data-ttu-id="a5cb2-167">说明如何创建新的 FileTable 或者更改或删除现有的 FileTable。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-167">Describes how to create a new FileTable, or alter or drop an existing FileTable.</span></span>  
  
 [<span data-ttu-id="a5cb2-168">将文件加载到 FileTable 中</span><span class="sxs-lookup"><span data-stu-id="a5cb2-168">Load Files into FileTables</span></span>](load-files-into-filetables.md)  
 <span data-ttu-id="a5cb2-169">说明如何将文件加载或迁移到 FileTable 中。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-169">Describes how to load or migrate files into FileTables.</span></span>  
  
 [<span data-ttu-id="a5cb2-170">在 FileTable 中使用目录和路径</span><span class="sxs-lookup"><span data-stu-id="a5cb2-170">Work with Directories and Paths in FileTables</span></span>](work-with-directories-and-paths-in-filetables.md)  
 <span data-ttu-id="a5cb2-171">说明 FileTable 中用于存储文件的目录结构。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-171">Describes the directory structure in which the files are stored in FileTables.</span></span>  
  
 [<span data-ttu-id="a5cb2-172">使用 Transact-SQL 访问 FileTable</span><span class="sxs-lookup"><span data-stu-id="a5cb2-172">Access FileTables with Transact-SQL</span></span>](access-filetables-with-transact-sql.md)  
 <span data-ttu-id="a5cb2-173">说明 Transact-SQL 数据操作语言 (DML) 命令如何与 FileTable 一起使用。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-173">Describes how Transact-SQL data manipulation language (DML) commands work with FileTables.</span></span>  
  
 [<span data-ttu-id="a5cb2-174">使用文件输入输出 API 访问 FileTable</span><span class="sxs-lookup"><span data-stu-id="a5cb2-174">Access FileTables with File Input-Output APIs</span></span>](access-filetables-with-file-input-output-apis.md)  
 <span data-ttu-id="a5cb2-175">说明如何在 FileTable 上执行文件系统 I/O。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-175">Describes how file system I/O works on a FileTable.</span></span>  
  
 [<span data-ttu-id="a5cb2-176">管理 FileTable</span><span class="sxs-lookup"><span data-stu-id="a5cb2-176">Manage FileTables</span></span>](manage-filetables.md)  
 <span data-ttu-id="a5cb2-177">说明用于管理 FileTable 的常见管理任务。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-177">Describes common administrative tasks for managing FileTables.</span></span>  
  
  
##  <a name="related-content"></a><a name="relcontent"></a> <span data-ttu-id="a5cb2-178">相关内容</span><span class="sxs-lookup"><span data-stu-id="a5cb2-178">Related Content</span></span>  
 [<span data-ttu-id="a5cb2-179">FileTable 架构</span><span class="sxs-lookup"><span data-stu-id="a5cb2-179">FileTable Schema</span></span>](filetable-schema.md)  
 <span data-ttu-id="a5cb2-180">说明 FileTable 的预定义固定架构。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-180">Describes the pre-defined and fixed schema of a FileTable.</span></span>  
  
 [<span data-ttu-id="a5cb2-181">FileTable 与其他 SQL Server 功能的兼容性</span><span class="sxs-lookup"><span data-stu-id="a5cb2-181">FileTable Compatibility with Other SQL Server Features</span></span>](filetable-compatibility-with-other-sql-server-features.md)  
 <span data-ttu-id="a5cb2-182">说明 FileTable 如何与 SQL Server 的其他功能配合使用。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-182">Describes how FileTables work with other features of SQL Server.</span></span>  
  
 [<span data-ttu-id="a5cb2-183">FileTable DDL、函数、存储过程和视图</span><span class="sxs-lookup"><span data-stu-id="a5cb2-183">FileTable DDL, Functions, Stored Procedures, and Views</span></span>](../views/views.md)  
 <span data-ttu-id="a5cb2-184">列出用于支持 FileTable 功能的新增或更改的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象。</span><span class="sxs-lookup"><span data-stu-id="a5cb2-184">Lists the [!INCLUDE[tsql](../../includes/tsql-md.md)] statements and the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database objects that have been added or changed to support the FileTable feature.</span></span>  
  
 
  
