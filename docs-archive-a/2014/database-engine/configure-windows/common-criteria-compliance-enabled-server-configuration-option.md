---
title: common criteria compliance enabled 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6722d05351b8b9e80240abb4edef0633a97b6da0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87577846"
---
# <a name="common-criteria-compliance-enabled-server-configuration-option"></a>common criteria compliance enabled 服务器配置选项
  common criteria compliance enabled 选项用于启用通用准则所需的下列元素：  
  
|条件|说明|  
|--------------|-----------------|  
|残留信息保护 (RIP)|RIP 要求将内存重新分配给新资源之前，用已知的位模式覆盖内存分配。 满足 RIP 标准有助于提高安全性；然而，覆盖内存分配会使性能降低。 启用 common criteria compliance enabled 选项之后，将执行覆盖操作。|  
|查看登录统计信息的能力|启用 common criteria compliance enabled 选项之后，将启用登录审核。 用户每次成功登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，系统都会提供有关上一次成功登录的时间、上一次登录失败的时间以及上一次成功登录时间和当前登录时间之间尝试登录的次数的信息。 可以通过查询 [sys.dm_exec_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) 动态管理视图来查看这些登录统计信息。|  
|GRANT 列不应覆盖 DENY 表|启用 common criteria compliance enabled 后，表级 DENY 将优先于列级 GRANT。 未启用该选项时，列级 GRANT 则优先于表级 DENY。|  
  
 common criteria compliance enabled 选项是高级选项。 通用准则仅针对 Enterprise Edition 和 Datacenter Edition 进行评估和认证。 有关通用准则认证的最新状态，请参阅 [Microsoft SQL Server 通用准则](https://go.microsoft.com/fwlink/?LinkId=616319) 网站。  
  
> [!IMPORTANT]  
>  除启用“common criteria compliance enabled”选项以外，还必须下载和运行一个版本，该版本可完成对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的配置以便符合通用准则评估保证级别 4 (EAL4+)。 可以从 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) （Microsoft SQL Server 通用准则）网站下载此脚本。  
  
 如果使用 sp_configure 系统存储过程来更改该设置，则只有在“show advanced options”设置为 1 时才能更改“common criteria compliance enabled”。 该设置在服务器重新启动后生效。 可能的值为 0 和 1：  
  
-   0 表示未启用符合通用准则。 这是默认值。  
  
-   1 表示启用了符合通用准则。  
  
## <a name="examples"></a>示例  
 以下示例启用符合通用准则。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
