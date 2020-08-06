---
title: 结论 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1e6fde6-c3a7-4b91-b176-fa465325dd21
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 906f9f10c541e7662d5573fd242a84f37483166e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691399"
---
# <a name="conclusion"></a>结论
  在本教程中，您已学习了如何一起使用 SQL Server Integration Services (SSIS)、Master Data Services (MDS) 和 Data Quality Services (DQS) 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您使用数据质量客户端工具创建了一个包含与供应商有关知识的 DQS 知识库，对照该知识库清理了一个 excel 文件中的输入供应商数据，然后通过使用该知识库中的匹配策略对供应商数据进行了匹配，以便标识并删除数据中的重复项。 接下来，通过使用用于 Excel 的 MDS 外接程序，您将已清理和已匹配的供应商列表存储到 MDS 中。 最后，您通过创建一个 SSIS 解决方案，将接收输入数据、清理和匹配数据以及将主数据存储于 MDS 中的整个过程自动化。  
  
## <a name="for-more-information"></a>更多相关信息：  
  
 [企业信息管理 (EIM)：将 SSIS、DQS 和 MDS 融汇在一起（视频）](https://go.microsoft.com/fwlink/?LinkId=258672)  
  
  
