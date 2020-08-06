---
title: 在90或更高版本的兼容模式下，大常量被类型化为大值类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 58acde8aaebdcac629463edcfb565eed13355ad4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578013"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>在 90 或更高的兼容模式下，大的常量作为大值类型键入
  升级顾问检测到有大的常量存在。 大小大于 8,000 个字节的字符串常量和二进制常量在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中被视为大型对象数据类型。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，大型字符、Unicode 和二进制常量作为大值类型键入。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 当字符串函数（如 CHARINDEX 和 PATINDEX）与超过 8,000 个字节的字符串常量或二进制常量一起使用时，[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 将返回错误号 8116，而 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本将返回错误号 8152。  
  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，当字符串函数与 `text`、`ntext` 和 `image` 数据类型一起使用时，将返回错误 8116。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，大的常量被分别视为 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 数据类型。 这些数据类型均与字符串函数兼容。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本中，字符串函数（如 CHARINDEX 和 PATINDEX）假定包含要查找的字符序列的字符串少于 8,000 个字节。 因此，对于 CHARINDEX 和 PATINDEX，将引发错误 8152。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
