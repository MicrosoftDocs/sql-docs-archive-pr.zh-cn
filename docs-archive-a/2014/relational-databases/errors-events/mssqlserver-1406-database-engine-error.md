---
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: adaa0084b875f720c477189e0e8e085af124f4cb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690631"
---
# <a name="mssqlserver_1406"></a>MSSQLSERVER_1406
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|1406|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBM_BADSTATEFORFORCESERVICE|  
|消息正文|无法安全地强制执行服务。 请删除数据库镜像并恢复数据库 "%.*ls" 以获得访问权。|  
  
## <a name="explanation"></a>说明  
 由于镜像状态不能保证强制服务过程正确进行，所以 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 不能强制服务。  
  
## <a name="user-action"></a>用户操作  
 删除数据库镜像。 然后可以恢复该镜像数据库以获得它的访问权。  
  
## <a name="see-also"></a>另请参阅  
 [在数据库镜像会话中强制服务 (Transact-SQL)](../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)   
 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
