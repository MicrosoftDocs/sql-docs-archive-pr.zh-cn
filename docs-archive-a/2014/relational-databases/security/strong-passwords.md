---
title: 强密码 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5e878e0de5ee1f496dcc981182d42f5898838c64
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688707"
---
# <a name="strong-passwords"></a>强密码
  在服务器安全部署中，密码可能是最薄弱的一个环节。 请务必在选择密码时保持高度谨慎。 强密码有以下特征：  
  
-   长度至少有 8 个字符。  
  
-   密码中组合使用字母、数字和符号字符。  
  
-   字典中查不到。  
  
-   不是命令名。  
  
-   不是人名。  
  
-   不是用户名。  
  
-   不是计算机名。  
  
-   定期更改。  
  
-   与以前的密码明显不同。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密码最多可包含 128 个字符，其中包括字母、符号和数字。 由于在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中经常使用登录名、用户名、角色和密码，所以必须用英文双引号 (") 或方括号 ([ ]) 括起某些符号。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 登录名、用户、角色或密码具有以下特征，请在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句中使用以下分隔符：  
  
-   含有空格或以空格开头。  
  
-   以 $ 或 \@ 字符开头。  
  
 如果用于 OLE DB 或 ODBC 连接字符串，则登录名或密码不能包含以下字符：[] {}() , ; ? * ! \@. 这些字符用于初始化连接或分隔连接值。  
  
## <a name="related-content"></a>相关内容  
 [密码策略](password-policy.md)  
  
  
