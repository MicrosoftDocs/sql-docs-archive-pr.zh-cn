---
title: SetNumValue 方法 (ClientNetworkProtocolProperty 类) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetNumValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetNumValue method
ms.assetid: c292e2ae-6d0a-44ad-ba54-5b0bd705ef37
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82a5474c2330d0d5bc0ed8766614773ceb899bf9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586559"
---
# <a name="setnumvalue-method-clientnetworkprotocolproperty-class"></a>SetNumValue 方法（ClientNetworkProtocolProperty 类）
  设置 PropertyIdx 属性引用的当前属性的数值) 值[ (ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetNumValue [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 表示客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|value|一个指定所引用属性的数值的 `uint32` 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
