---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9978f35ebe41eeda1470220772f87e83ab1ad942
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586715"
---
# <a name="mssqlserver_7308"></a><span data-ttu-id="8dc0b-102">MSSQLSERVER_7308</span><span class="sxs-lookup"><span data-stu-id="8dc0b-102">MSSQLSERVER_7308</span></span>
    
## <a name="details"></a><span data-ttu-id="8dc0b-103">详细信息</span><span class="sxs-lookup"><span data-stu-id="8dc0b-103">Details</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="8dc0b-104">产品名称</span><span class="sxs-lookup"><span data-stu-id="8dc0b-104">Product Name</span></span>|<span data-ttu-id="8dc0b-105">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8dc0b-105">SQL Server</span></span>|  
|<span data-ttu-id="8dc0b-106">事件 ID</span><span class="sxs-lookup"><span data-stu-id="8dc0b-106">Event ID</span></span>|<span data-ttu-id="8dc0b-107">7308</span><span class="sxs-lookup"><span data-stu-id="8dc0b-107">7308</span></span>|  
|<span data-ttu-id="8dc0b-108">事件源</span><span class="sxs-lookup"><span data-stu-id="8dc0b-108">Event Source</span></span>|<span data-ttu-id="8dc0b-109">MSSQLSERVER</span><span class="sxs-lookup"><span data-stu-id="8dc0b-109">MSSQLSERVER</span></span>|  
|<span data-ttu-id="8dc0b-110">组件</span><span class="sxs-lookup"><span data-stu-id="8dc0b-110">Component</span></span>|<span data-ttu-id="8dc0b-111">SQLEngine</span><span class="sxs-lookup"><span data-stu-id="8dc0b-111">SQLEngine</span></span>|  
|<span data-ttu-id="8dc0b-112">符号名称</span><span class="sxs-lookup"><span data-stu-id="8dc0b-112">Symbolic Name</span></span>|<span data-ttu-id="8dc0b-113">RMT_STA_DISABLED</span><span class="sxs-lookup"><span data-stu-id="8dc0b-113">RMT_STA_DISABLED</span></span>|  
|<span data-ttu-id="8dc0b-114">消息正文</span><span class="sxs-lookup"><span data-stu-id="8dc0b-114">Message Text</span></span>|<span data-ttu-id="8dc0b-115">因为 OLE DB 访问接口“%ls”配置为在单线程单元模式下运行，所以该访问接口无法用于分布式查询。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-115">OLE DB provider '%ls' cannot be used for distributed queries because the provider is configured to run in single-threaded apartment mode.</span></span>|  
  
## <a name="explanation"></a><span data-ttu-id="8dc0b-116">说明</span><span class="sxs-lookup"><span data-stu-id="8dc0b-116">Explanation</span></span>  
 <span data-ttu-id="8dc0b-117">您使用了配置为在单线程单元 (STA) 模式下运行的 OLE DB 访问接口。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-117">You have used an OLE DB provider that is configured to run in single-threaded apartment (STA) mode.</span></span> <span data-ttu-id="8dc0b-118">在单线程单元 (STA) 模式下运行的 OLE DB 访问接口无法用于分布式查询。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-118">OLE DB providers that run in single-threaded apartment (STA) mode cannot be used for distributed queries.</span></span>  
  
## <a name="user-action"></a><span data-ttu-id="8dc0b-119">用户操作</span><span class="sxs-lookup"><span data-stu-id="8dc0b-119">User Action</span></span>  
 <span data-ttu-id="8dc0b-120">若要解决此错误，请将该访问接口配置为在多线程单元 (MTA) 模式下运行。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-120">To resolve this error, configure the provider to run in multithreaded apartment (MTA) mode.</span></span> <span data-ttu-id="8dc0b-121">如果该提供程序不支持 MTA，且无法升级到支持 MTA 的版本，请考虑将该提供程序配置为在进程外运行。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-121">If the provider does not support MTA, and the provider cannot be upgraded to a version that supports MTA, consider configuring the provider to run out-of-process.</span></span> <span data-ttu-id="8dc0b-122">该提供程序的供应商应能够告知你该提供程序是支持 MTA 还是在进程外运行。</span><span class="sxs-lookup"><span data-stu-id="8dc0b-122">The provider vendor should be able to tell you if the provider supports MTA or running out-of-process.</span></span>  
  
  
