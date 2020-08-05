---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c34ebc7c682d2ffe8bc0205565f5dfd44fdd5b66
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581229"
---
# <a name="mssqlserver_9532"></a>MSSQLSERVER_9532
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9532|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|消息正文|在涉及列集 '%.*ls' 的查询/DML 操作中，将列 '%.\*ls' 从数据类型 '%ls' 转换为数据类型 '%ls' 时转换失败。|  
  
## <a name="explanation"></a>说明  
 列集是一种非类型化的 XML 表示形式，它将表的某些列组合成为结构化的输出。 通过 XML 列集插入或更新稀疏列值时，插入基础稀疏列的值从 `xml` 数据类型隐式转换为另一种类型。 所提供的值无法转换为列的数据类型。  
  
## <a name="user-action"></a>用户操作  
 由于无法对提供的值进行隐式转换，因此该值可能是一个无效项。 更正该错误，然后重试。 如果该值正确，修改该语句以使用单个列而不使用列集。 通过此操作可将该值显式转换为正确的数据类型。  
  
  
