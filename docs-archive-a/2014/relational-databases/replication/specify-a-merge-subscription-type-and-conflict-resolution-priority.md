---
title: 指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], merge subscription resolvers
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 2b828d83-2341-4924-b92a-4f81a22246c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a19ae6246fe59308283fbaf2f35e2c49f96b140c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694442"
---
# <a name="specify-a-merge-subscription-type-and-conflict-resolution-priority-sql-server-management-studio"></a>指定合并订阅类型和冲突解决优先级 (SQL Server Management Studio)
  可以在新建订阅向导的 **“订阅类型”** 页上指定合并订阅类型和冲突解决优先级。 有关使用此向导的详细信息，请参阅 [Create a Pull Subscription](create-a-pull-subscription.md) 和 [Create a Push Subscription](create-a-push-subscription.md)。  
  
 创建订阅后订阅类型无法修改，但对于“订阅属性 - \<Publisher>: \<PublicationDatabase>”对话框中的服务器订阅类型来说，优先级可以修改。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)。  
  
### <a name="to-specify-a-merge-subscription-type-and-conflict-resolution-priority"></a>指定合并订阅类型和冲突解决优先级  
  
1.  在新建订阅向导的 **“订阅类型”** 页上，为 **“订阅类型”** 选项选择 **“客户端”** 或 **“服务器”** 。  
  
2.  如果选择 **“服务器”** 订阅类型，还要输入 **“冲突解决的优先级”** 选项的值（0.00 到 99.99）。  
  
### <a name="to-modify-the-conflict-resolution-priority"></a>修改冲突解决优先级  
  
1.  在发布服务器的“订阅属性 - \<Publisher>: \<PublicationDatabase>”中，输入“优先级”选项的值（0.00 到 99.99）。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
