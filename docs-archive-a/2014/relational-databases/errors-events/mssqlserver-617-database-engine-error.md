---
title: MSSQLSERVER_617 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 617 (Database Engine error)
ms.assetid: 213545d9-08a7-4427-bfd1-8b7e16644281
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 88e9feb7c3ac5d8cf646d2243319b2b160b7757e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690613"
---
# <a name="mssqlserver_617"></a>MSSQLSERVER_617
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|617|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|NODESHASH|  
|消息正文|尝试对数据库 ID %d 中的对象 ID %ld 的描述符进行解哈希运算时，在哈希表中没有找到该描述符。 工作表缺少条目。 请重新运行查询。 如果涉及到游标，请关闭游标，然后重新打开。|  
  
## <a name="explanation"></a>说明  
 SQL Server 在工作表中找不到特定项。  
  
## <a name="user-action"></a>用户操作  
  
1.  如果涉及到游标，请关闭游标，然后重新打开。  
  
2.  再次运行查询。  
  
  
