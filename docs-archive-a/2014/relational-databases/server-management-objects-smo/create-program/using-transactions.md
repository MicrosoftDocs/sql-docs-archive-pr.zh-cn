---
title: 使用事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: stevestein
ms.author: sstein
ms.openlocfilehash: a075719c8ed31ffcc1c34f2d013a8beb0ae40dae
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587762"
---
# <a name="using-transactions"></a><span data-ttu-id="70fb8-102">使用事务</span><span class="sxs-lookup"><span data-stu-id="70fb8-102">Using Transactions</span></span>
  <span data-ttu-id="70fb8-103">在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，通过使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 对象连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例，进而实现事务处理。</span><span class="sxs-lookup"><span data-stu-id="70fb8-103">In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), transaction processing is achieved through the connection to the instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] by using the <xref:Microsoft.SqlServer.Management.Common.ServerConnection> object.</span></span> <span data-ttu-id="70fb8-104"><xref:Microsoft.SqlServer.Management.Common.ServerConnection>建立连接后，对象由 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 对象的属性引用 <xref:Microsoft.SqlServer.Management.Smo.Server> 。</span><span class="sxs-lookup"><span data-stu-id="70fb8-104">The <xref:Microsoft.SqlServer.Management.Common.ServerConnection> object is referenced by the <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> property of the <xref:Microsoft.SqlServer.Management.Smo.Server> object when the connection is established.</span></span> <span data-ttu-id="70fb8-105"><xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>、<xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> 等方法均属于 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 对象属性。</span><span class="sxs-lookup"><span data-stu-id="70fb8-105">Methods such as <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A>, and <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> belong to the <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> object property.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="70fb8-106">另请参阅</span><span class="sxs-lookup"><span data-stu-id="70fb8-106">See Also</span></span>  
 [<span data-ttu-id="70fb8-107">创建 SMO 程序</span><span class="sxs-lookup"><span data-stu-id="70fb8-107">Creating SMO Programs</span></span>](creating-smo-programs.md)  
  
  
