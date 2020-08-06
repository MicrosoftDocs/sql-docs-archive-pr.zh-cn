---
title: StartMode 属性 (SqlService 类) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- StartMode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- StartMode property
ms.assetid: c0c2c7f8-d4ae-44f2-ad8e-aecfcb7c2878
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bafffcc3c8f82f69896d0a22e9b0a9060e04cd10
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690435"
---
# <a name="startmode-property-sqlservice-class"></a>StartMode 属性（SqlService 类）
  获取服务的启动模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.StartMode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务模式的 uint32 值。  
  
 可以是下列值之一。  
  
 启动  
 值 = 0。 服务由操作系统加载程序启动。 此选项只对驱动程序服务有效。  
  
 System  
 值 = 1。 服务由 `IoInitSystem` 方法启动。 此选项只对驱动程序服务有效。  
  
 自动  
 值 = 2。 服务将在系统启动期间由服务控制管理器自动启动。  
  
 手动  
 值 = 3。 服务将在进程调用 `StartService` 方法时由计算机管理器启动。  
  
 已禁用  
 值 = 4。 无法启动服务。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
