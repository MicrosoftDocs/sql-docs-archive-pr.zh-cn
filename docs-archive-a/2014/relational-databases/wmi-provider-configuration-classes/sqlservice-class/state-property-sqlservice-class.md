---
title: State 属性 (SqlService 类) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- State Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a7456113d9ec4444507d1057892a65adf241992f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690429"
---
# <a name="state-property-sqlservice-class"></a>State 属性（SqlService 类）
  获取或设置服务的当前状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.State [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务状态的 uint32 值。  
  
 可以是下列值之一。  
  
 1  
 已停止。 服务已停止。  
  
 2  
 启动挂起。 服务正在等待启动。  
  
 3  
 停止挂起。 服务正在等待停止。  
  
 4  
 正在运行。 服务正在运行。  
  
 5  
 继续挂起。 服务正在等待继续。  
  
 6  
 暂停挂起。 服务正在等待暂停。  
  
 7  
 已暂停。 服务已暂停。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
