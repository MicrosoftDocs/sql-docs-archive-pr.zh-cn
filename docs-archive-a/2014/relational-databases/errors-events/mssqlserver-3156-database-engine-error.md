---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 25b5a037012a6d6b47b91e763a49cfb67b89f43c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586723"
---
# <a name="mssqlserver_3156"></a><span data-ttu-id="abb27-102">MSSQLSERVER_3156</span><span class="sxs-lookup"><span data-stu-id="abb27-102">MSSQLSERVER_3156</span></span>
    
## <a name="details"></a><span data-ttu-id="abb27-103">详细信息</span><span class="sxs-lookup"><span data-stu-id="abb27-103">Details</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="abb27-104">产品名称</span><span class="sxs-lookup"><span data-stu-id="abb27-104">Product Name</span></span>|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|<span data-ttu-id="abb27-105">事件 ID</span><span class="sxs-lookup"><span data-stu-id="abb27-105">Event ID</span></span>|<span data-ttu-id="abb27-106">3156</span><span class="sxs-lookup"><span data-stu-id="abb27-106">3156</span></span>|  
|<span data-ttu-id="abb27-107">事件源</span><span class="sxs-lookup"><span data-stu-id="abb27-107">Event Source</span></span>|<span data-ttu-id="abb27-108">MSSQLSERVER</span><span class="sxs-lookup"><span data-stu-id="abb27-108">MSSQLSERVER</span></span>|  
|<span data-ttu-id="abb27-109">组件</span><span class="sxs-lookup"><span data-stu-id="abb27-109">Component</span></span>|<span data-ttu-id="abb27-110">SQLEngine</span><span class="sxs-lookup"><span data-stu-id="abb27-110">SQLEngine</span></span>|  
|<span data-ttu-id="abb27-111">符号名称</span><span class="sxs-lookup"><span data-stu-id="abb27-111">Symbolic Name</span></span>|<span data-ttu-id="abb27-112">LDDB_CANT_WRITE</span><span class="sxs-lookup"><span data-stu-id="abb27-112">LDDB_CANT_WRITE</span></span>|  
|<span data-ttu-id="abb27-113">消息正文</span><span class="sxs-lookup"><span data-stu-id="abb27-113">Message Text</span></span>|<span data-ttu-id="abb27-114">文件 '%ls' 无法还原为 '%ls'。</span><span class="sxs-lookup"><span data-stu-id="abb27-114">File '%ls' cannot be restored to '%ls'.</span></span> <span data-ttu-id="abb27-115">请使用 WITH MOVE 选项来标识该文件的有效位置。</span><span class="sxs-lookup"><span data-stu-id="abb27-115">Use WITH MOVE to identify a valid location for the file.</span></span>|  
  
## <a name="explanation"></a><span data-ttu-id="abb27-116">说明</span><span class="sxs-lookup"><span data-stu-id="abb27-116">Explanation</span></span>  
 <span data-ttu-id="abb27-117">此常规消息标识因指定位置错误而无法还原的文件的逻辑文件名或物理文件名。</span><span class="sxs-lookup"><span data-stu-id="abb27-117">This general message identifies the logical or physical file names of files that could not be restored because of a problem with the specified location.</span></span>  
  
### <a name="possible-causes"></a><span data-ttu-id="abb27-118">可能的原因</span><span class="sxs-lookup"><span data-stu-id="abb27-118">Possible Causes</span></span>  
 <span data-ttu-id="abb27-119">可能的原因包括：</span><span class="sxs-lookup"><span data-stu-id="abb27-119">The possible causes include the following:</span></span>  
  
-   <span data-ttu-id="abb27-120">可能需要具备对指定 Windows 目录的访问权限。</span><span class="sxs-lookup"><span data-stu-id="abb27-120">You might need access to the specified Windows directory.</span></span>  
  
-   <span data-ttu-id="abb27-121">键入的路径可能有误或指定的路径不存在。</span><span class="sxs-lookup"><span data-stu-id="abb27-121">You might have mistyped the path or specified a path that does not exist.</span></span>  
  
-   <span data-ttu-id="abb27-122">某个无法覆盖的文件可能正在使用该文件名。</span><span class="sxs-lookup"><span data-stu-id="abb27-122">The file name might be being used by a file that cannot be overwritten.</span></span>  
  
## <a name="user-action"></a><span data-ttu-id="abb27-123">用户操作</span><span class="sxs-lookup"><span data-stu-id="abb27-123">User Action</span></span>  
 <span data-ttu-id="abb27-124">在错误日志中查找提供详细信息的其他消息。</span><span class="sxs-lookup"><span data-stu-id="abb27-124">Look at the error logs for other messages that provide more details.</span></span>  
  
 <span data-ttu-id="abb27-125">更正指定位置的错误，例如，授予访问权限或使用 RESTORE 语句中的 WITH MOVE 选项重新定位文件。</span><span class="sxs-lookup"><span data-stu-id="abb27-125">Correct the problem with the specified location, for example, by granting access, or use the WITH MOVE option in your RESTORE statement to relocate the file.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="abb27-126">另请参阅</span><span class="sxs-lookup"><span data-stu-id="abb27-126">See Also</span></span>  
 <span data-ttu-id="abb27-127">[将数据库还原到新位置 (SQL Server)](../backup-restore/restore-a-database-to-a-new-location-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="abb27-127">[Restore a Database to a New Location &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md) </span></span>  
 <span data-ttu-id="abb27-128">[将文件还原到 &#40;SQL Server 的新位置&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md) </span><span class="sxs-lookup"><span data-stu-id="abb27-128">[Restore Files to a New Location &#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md) </span></span>  
 [<span data-ttu-id="abb27-129">RESTORE &#40;Transact-SQL&#41;</span><span class="sxs-lookup"><span data-stu-id="abb27-129">RESTORE &#40;Transact-SQL&#41;</span></span>](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
