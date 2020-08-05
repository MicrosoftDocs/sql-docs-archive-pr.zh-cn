---
title: MSSQLSERVER_33128 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33128 (Database Engine error)
ms.assetid: 12c1096f-d120-439b-85f3-f794859503c9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 158cc609a18cf3fe7b76708e351b78263cd80a9e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581251"
---
# <a name="mssqlserver_33128"></a>MSSQLSERVER_33128
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33128|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_DEPRECATED_ALGO|  
|消息正文|加密失败。 密钥使用了不推荐使用的算法“%.*ls”，这不再受支持。|  
  
## <a name="explanation"></a>说明  
 引用 RC4（或 RC4_128）加密算法时，就会出现此消息。 RC4 和 RC4_128 是弱算法，不推荐使用它们。 请改用一种较强的算法，如某个 AES 算法。  
  
 数据库兼容级别为 90 或 100 时，该操作成功，引发不推荐使用事件，该消息仅在环形缓冲区中显示。  
  
 数据库兼容级别为 110 或更高时，解密操作成功，引发不推荐使用事件，该消息仅在环形缓冲区中显示。 加密操作将失败，引发不推荐使用事件，对用户显示该消息并在环形缓冲区中显示它。  
  
> [!NOTE]  
>  环形缓冲区是未完全介绍的内部组件，不计划提供给客户使用。 与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客户支持联系时，来自环形缓冲区的消息很有用。 若要查看环形缓冲区，请查询 sys.dm_os_ring_buffers 动态管理视图。  
  
|状态|说明|  
|-----------|-----------------|  
|1|RC4 密钥在内置的 encryptbykey() 函数使用。 内置函数返回 NULL。 此消息仅显示在环形缓冲区中。|  
|2|RC4 密钥在内置的 decryptbykey() 函数中使用。 此消息仅显示在环形缓冲区中。|  
|3|对称密钥正在对不推荐使用的 RC4 密钥加密。 显示给用户和在环形缓冲区中显示。 不能在兼容级别 110 中更改不推荐使用的 RC4 对称密钥。 尝试使用非 RC4 密钥进行加密操作。 如果需要，将向后兼容级别设置为 90 或 100。|  
|4|不推荐使用的 RC4 对称密钥正在对非 RC4 密钥加密。 显示给用户和在环形缓冲区中显示。 修改应用程序以使用非 RC4 对称密钥或将向后兼容级别设置为 90 或 100。|  
|5|对称密钥正在对不推荐使用的 RC4 密钥解密。 此消息仅显示在环形缓冲区中。|  
|6|RC4 对称密钥正在对非 RC4 密钥解密。 此消息仅显示在环形缓冲区中。|  
|7|证书正在对 RC4 对称密钥加密。 显示给用户和在环形缓冲区中显示。|  
|8|证书正在对 RC4 对称密钥解密。 此消息仅显示在环形缓冲区中。|  
|9|EKM 密钥正在对 RC4 对称密钥加密。|  
|10|EKM 密钥正在对 RC4 对称密钥解密。 此消息仅显示在环形缓冲区中。|  
  
## <a name="user-action"></a>用户操作  
 请改用一种较强的算法，如某个 AES 算法。 （建议）  
  
 使用 ALTER DATABASE SET COMPATIBILITY_LEVEL 将数据库兼容级别设置为 100。 （建议不要使用。）  
  
  
