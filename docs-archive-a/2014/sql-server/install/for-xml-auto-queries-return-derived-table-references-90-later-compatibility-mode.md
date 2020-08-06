---
title: FOR XML AUTO 查询在90或更高版本的兼容模式下返回派生表引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- FOR XML AUTO [SQL Server]
ms.assetid: 10c32f06-f7e1-40e0-8f79-6d921f2bef1d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 702cb2ca1d437dff03cee09c98d72082500709d2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591745"
---
# <a name="for-xml-auto-queries-return-derived-table-references-in-90-or-later-compatibility-modes"></a>在 90 或更高的兼容模式下，FOR XML AUTO 查询返回派生表引用
  当数据库兼容级别设置为 90 或更高时，在 AUTO 模式下执行的 FOR XML 查询将返回针对派生表别名的引用。 当兼容级别设置为 80 时，FOR XML AUTO 查询将返回针对定义派生表的基表的引用。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 例如，请考虑下表：  
  
```  
CREATE TABLE Test(id int);  
INSERT INTO Test VALUES(1);  
INSERT INTO Test VALUES(2);  
```  
  
 下面包括派生表的查询在兼容级别分别为 80、90 或更高时产生不同的结果：  
  
```  
SELECT * FROM   
   (SELECT a.id AS a, b.id AS b   
    FROM Test a JOIN Test b ON a.id=b.id)  
AS DerivedTest   
FOR XML AUTO;  
```  
  
 当兼容级别为 80 时，查询返回以下结果。 结果引用派生表的基表别名 `a` 和 `b`，而非派生表别名。  
  
```  
<a a="1"><b b="1"/></a><a a="2"><b b="2"/></a>  
```  
  
 当兼容级别为 90 或更高时，查询返回针对派生表别名 `DerivedTest` 的引用，而非针对派生表基表的引用。  
  
```  
<DerivedTest a="1" b="1"/><DerivedTest a="2" b="2"/>  
```  
  
## <a name="corrective-action"></a>纠正措施  
 根据要求修改应用程序，以解决 FOR XML AUTO 查询（包括派生表并且在 90 或更高的兼容级别下运行）的结果发生变化这一问题。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
