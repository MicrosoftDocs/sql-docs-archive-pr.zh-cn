---
title: Azure 订阅连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpsubscrconn.f1
- sql11.dts.designer.afpsubscrconn.f1
ms.assetid: e1225327-c308-4c50-8f44-c411f52ef378
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bff1286525983b32c2191f1f8864a0f2bef0e6b0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586922"
---
# <a name="azure-subscription-connection-manager"></a>Azure 订阅连接管理器
  通过使用你为以下属性指定的值，Azure HDInsight 连接管理器使 SSIS 包能够连接到 Azure 订阅：Azure 订阅 ID 和管理证书。

1.  在如上所示的“添加 SSIS 连接管理器” **** 对话框中，选择“Azure 订阅” ****，然后单击“添加” ****。  你应该会看到 **** “Azure 订阅连接管理器编辑器”对话框。

     ![SSIS-AzureSubscriptionManager](../media/ssis-azuresubscriptionmanager.png "SSIS-AzureSubscriptionManager")

2.  为“Azure 订阅 ID” **** 输入你的 Azure 订阅 ID，它可以唯一标识 Azure 订阅。  可以在“设置” **** 页下的 [Azure 管理门户](https://manage.windowsazure.com) 上找到这些值：

     ![SSIS-AzureSettings-SubscriptionID](../media/ssis-azuresettings-subscriptionid.png "SSIS-AzureSettings-SubscriptionID")

3.  从下拉列表中选择“管理证书存储位置”**** 和“管理证书存储名称”****。

4.  输入“管理证书指纹”或单击“浏览…”，从所选存储中选择一个证书********。 必须将证书作为订阅的管理证书上载。 为此，请在以下 Azure 门户页上单击“上传”****（请参阅这篇 [MSDN 帖子](https://msdn.microsoft.com/library/azure/gg551722.aspx)以了解详细信息）。

     ![SSIS-AzureSettings-ManagementCertificate](../media/ssis-azuresettings-managementcertificate.png "SSIS-AzureSettings-ManagementCertificate")

5.  单击 "**测试连接**" 以测试连接。

6.  单击 **“确定”** 关闭对话框。


