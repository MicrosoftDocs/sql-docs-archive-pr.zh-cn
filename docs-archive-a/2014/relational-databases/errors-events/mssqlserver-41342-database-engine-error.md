---
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c0269322b30cee88e5ba3d50b6d391464b735f54
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588572"
---
# <a name="mssqlserver_41342"></a>MSSQLSERVER_41342
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41342|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_HW_NOT_SUPPORTED|  
|消息正文|系统上的处理器型号不支持创建 *construct*。 较早的处理器通常会出现此错误。 有关支持的型号的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。|  
  
## <a name="explanation"></a>说明  
 内存优化的表要求处理器型号支持对 128 位值执行原子比较和交换操作，这要求装配说明 CMPXCHG16B。 一些较旧的 AMD 处理器型号不支持 CMPXCHG16B 指令。 此外，默认情况下，某些虚拟化环境不启用此指令。  
  
## <a name="user-action"></a>用户操作  
 升级您的处理器。 如果您的处理器支持该指令并且您正在虚拟机中运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则更改配置以便支持指令 CMPXCHG16B。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
