---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 224317e290ce15aaed979129733b6273b3b663df
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589585"
---
# <a name="mssqlserver_5237"></a>MSSQLSERVER_5237
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5237|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|消息正文|由于内部查询错误，对对象 'NAME' (对象 ID 为 O_ID)进行的 DBCC 跨行集检查失败。|  
  
## <a name="explanation"></a>说明  
 因出现内部错误，DBCC 无法通过执行查询来检查索引视图。  
  
## <a name="user-action"></a>用户操作  
 重新运行 DBCC 命令。  
  
  
