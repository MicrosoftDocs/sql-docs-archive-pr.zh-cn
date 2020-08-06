---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04d4cbdd2197745d2d795814d88c4f7bc28eb90e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576667"
---
# <a name="mssql_eng014121"></a>MSSQL_ENG014121
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14121|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|无法删除分发服务器 '%s'。 此分发服务器与分发数据库相关联。|  
  
## <a name="explanation"></a>说明  
 配置为分发服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例无法从分发服务器的角色中删除，因为存在与此实例相关联的分发数据库。 如果试图删除与一个或多个发布服务器相关联的分发数据库，将发生此错误。  
  
## <a name="user-action"></a>用户操作  
 若要查找与此分发服务器关联的任何发布服务器和分发数据库的名称，请从分发服务器上的任何数据库中执行 [sp_helpdistpublisher (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql)。  
  
 对与此分发服务器关联的任何分发数据库，执行 [sp_dropdistributiondb (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql)。 删除所有分发数据库关联后，才可以禁用分发。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [配置分发](configure-distribution.md)  
  
  
