---
title: OLE 自动化结果集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- data types [SQL Server], OLE Automation
- two-dimensional arrays
- one-dimensional arrays
- result sets [SQL Server], OLE Automation
- OLE Automation [SQL Server], result sets
- arrays [SQL Server]
ms.assetid: b2f99e33-2303-427c-94b9-9d55f8e2a6ab
author: stevestein
ms.author: sstein
ms.openlocfilehash: f7c9bdc4d51d989db2d4d676b29e0824c0e5b59a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591863"
---
# <a name="ole-automation-result-sets"></a>OLE 自动化结果集
  如果 OLE 自动化属性或方法返回的数据是一维或二维数组，则该数组将作为结果集返回到客户端：  
  
-   一维数组作为单行结果集返回给客户端，其中的列数与数组中的元素数相等。 例如，array(10) 作为 10 列单行返回。  
  
-   二维数组作为结果集返回给客户端，其中的列数与数组第一维中的元素数相同，行数与数组第二维中的元素数相同。 例如，array(2,3) 作为 2 列 3 行返回。  
  
 当属性返回值或方法返回值是数组时，sp_OAGetProperty 或 sp_OAMethod 将向客户端返回结果集。 （方法输出参数不能是数组。这些过程可扫描数组中的所有数据值，以确定用于结果集中各列的相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和数据长度。 对于某个特定的列，这些过程将使用显示该列中的所有数据值所需要的数据类型和长度。  
  
 如果一列中的所有数据值具有相同的数据类型，此数据类型将用于整个列。 当一个列中的数据值的数据类型不同时，将根据下表选择整个列的数据类型。 若要使用下表，请沿着左侧行轴找到一种数据类型，再沿着最上面的列轴找到第二种数据类型。 行和列的交点会说明结果集这一列的数据类型。  
  
||||||||  
|-|-|-|-|-|-|-|  
||`int`|`float`|`money`|`datetime`|`varchar`|`nvarchar`|  
|`int`|`int`|`float`|`money`|`varchar`|`varchar`|`nvarchar`|  
|`float`|`float`|`float`|`money`|`varchar`|`varchar`|`nvarchar`|  
|`money`|`money`|`money`|`money`|`varchar`|`varchar`|`nvarchar`|  
|`datetime`|`varchar`|`varchar`|`varchar`|`datetime`|`varchar`|`nvarchar`|  
|`varchar`|`varchar`|`varchar`|`varchar`|`varchar`|`varchar`|`nvarchar`|  
|`nvarchar`|`nvarchar`|`nvarchar`|`nvarchar`|`nvarchar`|`nvarchar`|`nvarchar`|  
  
## <a name="related-content"></a>相关内容  
 [OLE 自动存储过程 (Transact-SQL)](/sql/relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql)  
  
 [Ole Automation Procedures 服务器配置选项](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  
