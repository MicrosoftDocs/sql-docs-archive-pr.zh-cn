---
title: MSSQLSERVER_1461 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6667728b2cc134632ddc538b662d73533ee4d6ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589649"
---
# <a name="mssqlserver_1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1461|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_SAFETY_MISMATCH|  
|消息正文|在服务器中检测到数据库"%.*ls"的不同数据库镜像安全级别。 将使用 FULL 安全级别。|  
  
## <a name="explanation"></a>说明  
 修改事务安全级别时镜像连接断开，因为事务安全设置在主体数据库和镜像数据库中不一致。 将使用完全事务安全的默认安全设置。 会话将在高安全模式下运行。  
  
## <a name="user-action"></a>用户操作  
 若要关闭事务安全，请对主体数据库重新运行 ALTER DATABASE *database_name* SET PARTNER SAFETY OFF 语句。  
  
  
