---
title: 使用数据库邮件而不是 SQL Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b08df7be-d8be-4184-a661-38ec0ac85cd1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a6a957b65975645bdeb9f55faee4e650b53718b8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580180"
---
# <a name="use-database-mail-instead-of-sql-mail"></a>使用数据库邮件而不是 SQL Mail
  此规则检查 sys.configurations 目录视图以确定 SQL Mail XPs 服务器范围配置选项是否已设置为 ON。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的将来版本中将删除 SQL Mail。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 要发送邮件，请使用“数据库邮件”。  
  
 SQL Mail 在进程内运行到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 如果 SQL Mail 关闭，服务器也会关闭。 数据库邮件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外的单独进程内运行，它是可伸缩的，并且不需要在生产服务器上安装扩展 MAPI 客户端组件。  
  
## <a name="for-more-information"></a>有关详细信息  
 [数据库邮件](../database-mail/database-mail.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
