---
title: RemoveCertificate 方法 (SInstance 类) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- RemoveCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b876cd75778d1da9c9a46f65f39b915ebee0552
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687635"
---
# <a name="removecertificate-method-sinstance-class"></a>RemoveCertificate 方法（SInstance 类）
  从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例中删除当前安全证书。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.RemoveCertificate()  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示 [实例上的服务器设置的](sinstance-class.md) SInstance 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
