---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: rothja
ms.author: jroth
ms.openlocfilehash: 4489f9d1ad576d49d885842f6969f9b61065791c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580234"
---
# <a name="issasynchstatus-ole-db"></a><span data-ttu-id="d396c-102">ISSAsynchStatus (OLE DB)</span><span class="sxs-lookup"><span data-stu-id="d396c-102">ISSAsynchStatus (OLE DB)</span></span>
  <span data-ttu-id="d396c-103">**ISSAsynchStatus**公开对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 异步操作的支持。</span><span class="sxs-lookup"><span data-stu-id="d396c-103">**ISSAsynchStatus** exposes support for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asynchronous operations.</span></span> <span data-ttu-id="d396c-104">这是一个可选接口，它继承自 core OLE DB interface **IDBAsynchStatus**。</span><span class="sxs-lookup"><span data-stu-id="d396c-104">This is an optional interface that inherits from the core OLE DB interface **IDBAsynchStatus**.</span></span> <span data-ttu-id="d396c-105">除了从 IDBAsynchStatus 继承的 Abort 和 GetStatus 方法外，ISSAsynchStatus 还提供一个新方法，用于在完成异步操作或发生超时前等待\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d396c-105">In addition to the **Abort** and **GetStatus** methods inherited from **IDBAsynchStatus**, **ISSAsynchStatus** provides one new method that is used to wait until an asynchronous operation has completed or a time-out occurs.</span></span>  
  
|<span data-ttu-id="d396c-106">方法</span><span class="sxs-lookup"><span data-stu-id="d396c-106">Method</span></span>|<span data-ttu-id="d396c-107">说明</span><span class="sxs-lookup"><span data-stu-id="d396c-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="d396c-108">ISSAsynchStatus::Abort &#40;OLE DB&#41;</span><span class="sxs-lookup"><span data-stu-id="d396c-108">ISSAsynchStatus::Abort &#40;OLE DB&#41;</span></span>](issasynchstatus-abort-ole-db.md)|<span data-ttu-id="d396c-109">取消异步执行的操作。</span><span class="sxs-lookup"><span data-stu-id="d396c-109">Cancels an asynchronously executing operation.</span></span>|  
|[<span data-ttu-id="d396c-110">ISSAsynchStatus::GetStatus &#40;OLE DB&#41;</span><span class="sxs-lookup"><span data-stu-id="d396c-110">ISSAsynchStatus::GetStatus &#40;OLE DB&#41;</span></span>](issasynchstatus-getstatus-ole-db.md)|<span data-ttu-id="d396c-111">返回异步执行操作的状态。</span><span class="sxs-lookup"><span data-stu-id="d396c-111">Returns the status of an asynchronously executing operation.</span></span>|  
|[<span data-ttu-id="d396c-112">ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;</span><span class="sxs-lookup"><span data-stu-id="d396c-112">ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;</span></span>](issasynchstatus-waitforasynchcompletion-ole-db.md)|<span data-ttu-id="d396c-113">一直等待，直到异步执行的操作完成或发生超时。</span><span class="sxs-lookup"><span data-stu-id="d396c-113">Waits until the asynchronously executing operation is complete or a time-out occurs.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="d396c-114">备注</span><span class="sxs-lookup"><span data-stu-id="d396c-114">Remarks</span></span>  
 <span data-ttu-id="d396c-115">ISSAsynchStatus::GetStatus 方法的 ISSAsynchStatus 实现与 IDBAsynchStatus::GetStatus 方法大体相同，不同之处在于如果中止对数据源对象的初始化，前者将返回 E_UNEXPECTED，而不是 DB_E_CANCELED（但是 ISSAsynchStatus::WaitForAsynchCompletion 将返回 DB_E_CANCELED）\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d396c-115">The **ISSAsynchStatus** implementation of the **ISSAsynchStatus::GetStatus** method is the same as the **IDBAsynchStatus::GetStatus** method except that if the initialization of a data source object is aborted, E_UNEXPECTED is returned rather than DB_E_CANCELED (although **ISSAsynchStatus::WaitForAsynchCompletion** returns DB_E_CANCELED).</span></span> <span data-ttu-id="d396c-116">这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。</span><span class="sxs-lookup"><span data-stu-id="d396c-116">This is because the data source object is not left in the usual state following an abort operation, so that further initialization operations may be attempted.</span></span>  
  
 <span data-ttu-id="d396c-117">以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：</span><span class="sxs-lookup"><span data-stu-id="d396c-117">The following methods support the use of asynchronous execution in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:</span></span>  
  
-   <span data-ttu-id="d396c-118">**ICommand::Execute**</span><span class="sxs-lookup"><span data-stu-id="d396c-118">**ICommand::Execute**</span></span>  
  
-   <span data-ttu-id="d396c-119">**IOpenRowset::OpenRowset**</span><span class="sxs-lookup"><span data-stu-id="d396c-119">**IOpenRowset::OpenRowset**</span></span>  
  
-   <span data-ttu-id="d396c-120">**IMultipleResults::GetResult**</span><span class="sxs-lookup"><span data-stu-id="d396c-120">**IMultipleResults::GetResult**</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d396c-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d396c-121">See Also</span></span>  
 <span data-ttu-id="d396c-122">[接口 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md) </span><span class="sxs-lookup"><span data-stu-id="d396c-122">[Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md) </span></span>  
 [<span data-ttu-id="d396c-123">执行异步操作</span><span class="sxs-lookup"><span data-stu-id="d396c-123">Performing Asynchronous Operations</span></span>](../native-client/features/performing-asynchronous-operations.md)  
  
  
