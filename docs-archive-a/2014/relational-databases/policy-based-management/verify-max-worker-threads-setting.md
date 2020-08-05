---
title: 验证最大工作线程数设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5dbffb87f58d2beb633f43ff18680222ea62cf5e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580178"
---
# <a name="verify-max-worker-threads-setting"></a>验证最大工作线程数设置
  此规则检查 max worker threads 服务器选项中是否存在可能不正确的设置。 如果将 max worker threads 选项设置为较小的值，则可能会使过多的线程无法及时为传入的客户端请求提供服务，并且可能会导致“线程资源不足”。 但是，如果将此选项设置为较大的值，则由于每个活动线程在 32 位服务器上占用 512 KB，在 64 位服务器上最多占用 4 MB，因此可能会浪费地址空间。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 max worker threads 选项设置为 0。 这样 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就能够根据用户请求自动确定正确的活动工作线程数。  
  
## <a name="for-more-information"></a>有关详细信息  
 [配置 max worker threads 服务器配置选项](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
