---
title: Azure Blob 目标 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdest.f1
- sql11.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fb406d38b17748e8284acee4b2849a9fd99e53ac
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692464"
---
# <a name="azure-blob-destination"></a>Azure blob 目标
  “Azure blob 目标”  组件允许 SSIS 包将数据写入 Azure blob。 支持的文件格式：CSV 和 AVRO。 拖-将 " **Azure Blob 目标**" 拖放到数据流设计器，然后双击它以查看编辑器) 。  
  
1.  对于“Azure 存储空间连接管理器” **** 字段，请指定一个现有的 Azure 存储空间连接管理器，或新建一个引用 Azure 存储空间帐户的连接管理器。  
  
2.  对于“blob 容器名称” **** 字段，请指定包含源文件的 blob 容器的名称。  
  
3.  对于“blob 名称” **** 字段，请指定 blob 的路径。  
  
4.  对于“blob 文件格式” **** 字段，请指定要使用的 blob 格式。  
  
5.  如果文件格式是 CSV，你必须指定“列分隔符字符” **** 值。 如果文件中的第一行包含列名称，则还应选择**第一个数据行中的列名称**。  
  
6.  指定连接信息后，切换到“列” **** 页，将源列映射到 SSIS 数据流的目标列。  
  
  
