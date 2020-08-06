---
title: Azure HDInsight 创建群集任务 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpcreatecltask.f1
- sql11.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e4029e3a01cbcfe04be5f2879a9b60866bfc867a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688112"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 创建群集任务
“Azure HDInsight 创建群集任务”  启用一个 SSIS 包来创建指定的 Azure 订阅和资源组中的一个 Azure HDInsight 群集。
  
> [!NOTE]  
> - 新建 HDInsight 群集可能需要花费 10~20 分钟。  
> - 这里存在与创建和运行 Azure HDInsight 群集相关的成本。 有关详细信息，请参阅 [HDInsight 定价](https://azure.microsoft.com/pricing/details/hdinsight/)。  
  
若要添加“Azure HDInsight 创建群集任务”****，可将其拖放到 SSIS 设计器，然后双击或右键单击，再单击“编辑”**** 以查看以下“Azure HDInsight 创建群集任务编辑器”**** 对话框。  
  
下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**说明**|  
|AzureResourceManagerConnection|选择一个现有的 Azure 资源管理器连接管理器，或创建一个用于创建 HDInsight 群集的新连接管理器。|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器；或者创建一个新的连接管理器，该管理器引用将与 HDInsight 群集关联的 Azure 存储帐户。|
|SubscriptionId|指定将在其中创建 HDInsight 群集的订阅的 ID。|
|ResourceGroup|指定将在其中创建 HDInsight 群集的 Azure 资源组。|
|位置|指定 HDInsight 群集的位置。 必须在与指定的 Azure 存储账户相同的位置创建群集。|  
|ClusterName|指定要创建的 HDInsight 群集的名称。|  
|clusterSize|指定要在群集中创建的节点数。|  
|BlobContainer|指定要与 HDInsight 群集相关联的默认存储容器的名称。|  
|UserName|指定用于连接到 HDInsight 群集的用户名。|  
|密码|指定用于连接到 HDInsight 群集的密码。|
|SshUserName|指定使用 SSH 远程访问 HDInsight 群集时使用的用户名称。|
|SshPassword|指定使用 SSH 远程访问 HDInsight 群集的密码。|
|FailIfExists|指定如果群集已存在时任务是否失败。|  
  
> [!NOTE]  
> HDInsight 群集和 Azure 存储帐户的位置必须相同。
