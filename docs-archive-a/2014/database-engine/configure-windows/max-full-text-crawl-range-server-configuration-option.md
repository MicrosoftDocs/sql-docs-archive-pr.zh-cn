---
title: max full-text crawl range 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- crawls [full-text search]
- max full-text crawl range option
ms.assetid: a49de86b-0891-4dcd-89c0-ead30aab00e0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e1dbd9e44518b6e849a06a76e21fc605172fd2ff
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87683054"
---
# <a name="max-full-text-crawl-range-server-configuration-option"></a>max full-text crawl range 服务器配置选项
  使用 **max full-text crawl range** 选项可以优化 CPU 使用率，从而提高完全爬网时的爬网性能。 使用此选项，可以指定索引完全爬网时 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的分区数。 例如，如果有许多 CPU 且它们的使用率并非最佳，则可以增加此选项的最大值。 除了此选项以外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还使用众多其他因素（如表中的行数和 CPU 数）来确定应该使用的实际分区数。  
  
 此选项的默认值是 4；最小值是 1，最大值是 256。 对此选项所做的更改只会影响后续的爬网。 不会影响正在进行的爬网。  
  
 **max full-text crawl range** 选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则仅当 **显示高级选项** 设置为 1 时才能更改 **max full-text crawl range** （全文爬网最大范围）。 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
