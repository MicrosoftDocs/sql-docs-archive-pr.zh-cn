---
title: 警报属性： "新建警报 (选项" 页面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4a1507372aa1516c2a88b8682faa77a7d57e58f9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692111"
---
# <a name="alert-properties-new-alert-options-page"></a>警报属性：新建警报（“选项”页）
  使用此页可以查看和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报的选项。  
  
## <a name="options"></a>选项  
 **电子邮件**  
 在电子邮件通知中包括事件错误文本（如果有的话）。  
  
 **寻呼程序**  
 在寻呼程序通知中包括事件错误文本（如果有的话）。  
  
 **Net send**  
 在 net send 通知中包括事件错误文本（如果有的话）。  
  
 **要发送的其他通知消息**  
 键入要包括在通知消息中的任何其他文本。  
  
 **两次响应之间的延迟时间**  
 为重复发生的事件指定延迟时间。 某些事件可能会在短期内频繁发生。 在这种情况下，您可能需要知道事件已经发生，但不希望针对每一事件做出响应。 使用此选项可以指定超时。有一段延迟，在警报响应事件之后， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理将等待指定的延迟后再次响应，而不管该事件是否在延迟期间发生。  
  
 **）**  
 指定延迟时间（分钟）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
 **计算**  
 指定延迟时间（秒）。 若要在每次发生事件时均予以响应，请指定 0 分和 0 秒。  
  
## <a name="see-also"></a>另请参阅  
 [警报](alerts.md)  
  
  
