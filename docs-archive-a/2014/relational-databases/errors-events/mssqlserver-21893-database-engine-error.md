---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92479d7727ac2300d6a60d02492667d99a69b022
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589135"
---
# <a name="mssqlserver_21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21893|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21893|  
|消息正文|订阅服务器 (%s)（属于原始发布服务器“%s”）在重定向的发布服务器“%s”中不显示为远程服务器。 `sp_addlinkedserver`在重定向的发布服务器上运行，以将这些订阅服务器添加为远程服务器。|  
  
## <a name="explanation"></a>说明  
 `sp_validate_redirected_publisher`在远程服务器上， 使用发布服务器数据库的订阅元数据表来确定其关联的订阅服务器，并验证在订阅服务器的 master.dbo.sysservers 中具有关联的条目。 如果任何标识的订阅服务器不存在，则会返回此错误。  
  
 该错误不被视为严重错误。 遇到该错误的代理将此错误记录为信息性消息，但不会终止，因为在新发布服务器上无法具有适当的订阅服务器条目对复制的影响很有限。 如果在 sysservers 中没有相应的订阅服务器条目，则在通过 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 执行时，某些订阅管理活动可能会失败。 但是，可以通过显式执行管理存储过程成功地执行这些相同的活动。  
  
## <a name="user-action"></a>用户操作  
 在重定向的发布服务器上为每个标识的订阅服务器运行 `sp_addlinkedserver`，以将这些订阅服务器添加为远程服务器。 然后，运行 `sp_serveroption` 以设置该服务器的订阅服务器位。  
  
  
