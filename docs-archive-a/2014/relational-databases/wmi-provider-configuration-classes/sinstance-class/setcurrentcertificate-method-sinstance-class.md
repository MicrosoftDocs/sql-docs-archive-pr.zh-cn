---
title: SetCurrentCertificate 方法 (SInstance 类) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetCurrentCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 7349fb87-b973-4160-a2be-cab73abf5b31
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 44e65ab30659cacca09e63a94a1f3596a182dda5
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687636"
---
# <a name="setcurrentcertificate-method-sinstance-class"></a><span data-ttu-id="bc0be-102">SetCurrentCertificate 方法（SInstance 类）</span><span class="sxs-lookup"><span data-stu-id="bc0be-102">SetCurrentCertificate Method (SInstance Class)</span></span>
  <span data-ttu-id="bc0be-103">设置当前安全证书。</span><span class="sxs-lookup"><span data-stu-id="bc0be-103">Sets the current security certificate.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bc0be-104">语法</span><span class="sxs-lookup"><span data-stu-id="bc0be-104">Syntax</span></span>  
  
```  
  
object  
.SetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a><span data-ttu-id="bc0be-105">组成部分</span><span class="sxs-lookup"><span data-stu-id="bc0be-105">Parts</span></span>  
 <span data-ttu-id="bc0be-106">对象</span><span class="sxs-lookup"><span data-stu-id="bc0be-106">*object*</span></span>  
 <span data-ttu-id="bc0be-107">一个表示实例上的服务器设置的[SInstance 类](sinstance-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="bc0be-107">An [SInstance Class](sinstance-class.md) object that represents the server setting on an instance of [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].</span></span>  
  
#### <a name="parameters"></a><span data-ttu-id="bc0be-108">参数</span><span class="sxs-lookup"><span data-stu-id="bc0be-108">Parameters</span></span>  
  
|<span data-ttu-id="bc0be-109">参数</span><span class="sxs-lookup"><span data-stu-id="bc0be-109">Parameter</span></span>|<span data-ttu-id="bc0be-110">说明</span><span class="sxs-lookup"><span data-stu-id="bc0be-110">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="bc0be-111">*SHA*</span><span class="sxs-lookup"><span data-stu-id="bc0be-111">*SHA*</span></span>|<span data-ttu-id="bc0be-112">一个指定当前安全证书的字符串值。</span><span class="sxs-lookup"><span data-stu-id="bc0be-112">A string value that specifies the current security certificate.</span></span>|  
  
## <a name="property-valuereturn-value"></a><span data-ttu-id="bc0be-113">属性值/返回值</span><span class="sxs-lookup"><span data-stu-id="bc0be-113">Property Value/Return Value</span></span>  
 <span data-ttu-id="bc0be-114">一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。</span><span class="sxs-lookup"><span data-stu-id="bc0be-114">A `uint32` value, which is 0 if the service was successfully modified, 1 if the request is not supported, and any other number to indicate an error.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="bc0be-115">备注</span><span class="sxs-lookup"><span data-stu-id="bc0be-115">Remarks</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bc0be-116">另请参阅</span><span class="sxs-lookup"><span data-stu-id="bc0be-116">See Also</span></span>  
 <span data-ttu-id="bc0be-117">[配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)</span><span class="sxs-lookup"><span data-stu-id="bc0be-117">[Configuring Server Network Protocols and Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)</span></span>  
  
  
