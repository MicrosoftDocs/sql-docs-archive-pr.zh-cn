---
title: CLR 用户定义函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: ba7a4a983ec0cb36ef0fd79df44491f7f23f7648
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589148"
---
# <a name="clr-user-defined-functions"></a>CLR 用户定义函数
  用户定义函数是可采用参数、执行计算或其他操作并返回结果的例程。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，可以使用任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 编程语言（例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#）编写用户定义函数。  
  
 有两种类型的函数：标量，用于返回单个值；表值，用于返回一组行。  
  
 下表列出了本节的主题。  
  
 [CLR 标量值函数](clr-scalar-valued-functions.md)  
 包含标量值函数的实现要求和示例。  
  
 [CLR 表值函数](clr-table-valued-functions.md)  
 讨论如何实现和使用表值函数 (TVF)，以及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和公共语言运行时 (CLR) TVF 的区别。  
  
 [CLR 用户定义聚合](clr-user-defined-aggregates.md)  
 说明如何实现和使用用户定义聚合。  
  
## <a name="see-also"></a>另请参阅  
 [用户定义函数](../user-defined-functions/user-defined-functions.md)  
  
  
