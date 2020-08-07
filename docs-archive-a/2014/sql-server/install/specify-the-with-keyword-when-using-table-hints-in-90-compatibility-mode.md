---
title: 在90兼容性模式下使用表提示时指定 WITH 关键字 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH keyword
- table hints [SQL Server]
ms.assetid: 7636cc85-5155-44db-baf6-df807761adb8
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0ecd13475395cef4257d97eb7480f32420932e22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586146"
---
# <a name="specify-the-with-keyword-when-using-table-hints-in-90-compatibility-mode"></a>在 90 兼容模式下使用表提示时指定 WITH 关键字
  除了一些例外情况之外，仅当使用 WITH 关键字指定了表提示时，查询的 FROM 子句中才支持这些提示。 有关详细信息，请参阅 [!INCLUDE[tsql](../../includes/tsql-md.md)] 联机丛书中的“FROM ([!INCLUDE[tsql](../../includes/tsql-md.md)])”和“表提示 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])”。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 通过在表提示之前包括 WITH 关键字来修改在 FROM 子句中包含表提示的查询。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
