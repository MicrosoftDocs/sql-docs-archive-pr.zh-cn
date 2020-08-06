---
title: 即使触发器嵌套处于关闭状态，嵌套的 AFTER 触发器也会激发 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- DML triggers, nested
- nested triggers option
- triggers [SQL Server], nested
ms.assetid: 94d72960-676e-40d9-81bc-08bffe778110
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f91c04e8d69880b451c1479e2907cd1910e8f9c1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694246"
---
# <a name="nested-after-trigger-fires-even-when-trigger-nesting-is-off"></a>即使触发器嵌套功能设置为 OFF，也会触发嵌套的 AFTER 触发器
  升级顾问检测到一个嵌套在一个或多个表中定义的 INSTEAD OF 触发器中的 AFTER 触发器。 即使在 `nested triggers` 服务器配置选项设置为 0 时，也可能会激发嵌套 AFTER 触发器。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 即使 `nested triggers` 服务器配置选项设置为 0，也会激发嵌套在 INSTEAD OF 触发器内的第一个 AFTER 触发器。 但是，在此设置下，不会激发后续的 AFTER 触发器。  
  
## <a name="corrective-action"></a>纠正措施  
 检查嵌套触发器的应用程序以确定当 `nested triggers` 服务器配置选项设置为 0 时，应用程序是否仍然遵循有关此新行为的业务规则，然后进行适当的修改。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
