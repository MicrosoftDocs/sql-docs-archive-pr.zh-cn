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
# <a name="setcurrentcertificate-method-sinstance-class"></a>SetCurrentCertificate 方法（SInstance 类）
  设置当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示实例上的服务器设置的[SInstance 类](sinstance-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*SHA*|一个指定当前安全证书的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
