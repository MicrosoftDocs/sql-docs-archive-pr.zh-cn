---
title: Azure 存储连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 47580d8d1d961df9fbcbed0bd7164f1c54792b86
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586927"
---
# <a name="azure-storage-connection-manager"></a>Azure 存储连接管理器
  Azure 存储连接管理器使一个 SSIS 包可使用你指定的属性值连接到 Azure 存储帐户：存储帐户名称和帐户密钥。  
  
1.  在“添加 SSIS 连接管理器” **** 对话框中，选择“AzureStorage” ****，然后单击“添加” ****。  
  
2.  在“Azure 存储连接管理器编辑器”对话框中，选择“使用 Azure 帐户” **** 以通过 Internet 连接到 Azure 存储服务，或选择“使用本地开发人员帐户” **** 以连接到 Azure 存储模拟器承载的本地服务。  
  
3.  如果选择了“使用 Azure 帐户” **** 选项，请执行以下操作：  
  
    1.  为“存储帐户名称” **** 和“帐户密钥” **** 字段指定值。 这些值将存储为 SSIS 包中的敏感数据。  
  
    2.  如果你想要使用 HTTPS 而不是 HTTP 来连接到 Azure 存储服务，请选择“使用 HTTPS” **** 。  
  
4.  单击 **“确定”** 关闭对话框。  
  
5.  你可以看到你在“属性” **** 窗口中创建的连接管理器的属性。  
  
  
