---
title: 服务器 public 权限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7913c4715f47b8105b72b1c817dbe77e52d40539
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693266"
---
# <a name="server-public-permissions"></a>服务器 public 权限
  此规则确定 public 服务器角色是否具有服务器权限。 在服务器上创建的每个登录名都是 public 服务器角色的成员。 如果满足此条件，则服务器上的每个登录名都将具有服务器权限。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿为服务器 public 角色授予服务器权限。  
  
> [!IMPORTANT]  
>  安装完成后，**公共**角色对 `CONNECT` 所有终结点都有权限，**专用管理员连接**除外。 这很正常，通常不应更改。 （通过使用 `CONNECT SQL` 权限来控制访问，该权限是在创建新登录名时自动授予的。）  
  
### <a name="for-more-information"></a>更多信息  
 [保护 SQL Server](../security/securing-sql-server.md)  
  
  
