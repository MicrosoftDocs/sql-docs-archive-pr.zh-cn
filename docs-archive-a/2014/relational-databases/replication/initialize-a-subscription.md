---
title: 初始化订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], initializing subscriptions
- transactional replication, initializing subscriptions
- initializing subscriptions [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], about initializing subscriptions
- merge replication [SQL Server replication], initializing subscriptions
ms.assetid: d6013845-cb7a-4203-8e21-edce32f1d330
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1f024d360fdeab477ace09970b4f140a97696c2c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578074"
---
# <a name="initialize-a-subscription"></a>初始化订阅
  必须初始化复制拓扑中的订阅服务器，以使其具有来自它们所订阅的发布中各项目的架构副本以及全部所需复制对象（如存储过程、触发器和元数据表）。 另外，订阅服务器通常接收初始数据集。 默认的初始化方法使用完整的快照，其中包含架构、复制对象和数据；但没有完整的快照也可以初始化发布。  
  
 有关详细信息，请参阅 [Initialize a Subscription with a Snapshot](initialize-a-subscription-with-a-snapshot.md) 和 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
  
