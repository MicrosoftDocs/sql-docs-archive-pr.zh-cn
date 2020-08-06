---
title: " (SSAS 表格) 的表属性 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.tableprop.f1
ms.assetid: 16d3347b-7e43-4a6b-9956-fdd6ede092e6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9613609c42de8fd3a4aab7aec3208dfe3d31be4a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692551"
---
# <a name="table-properties-ssas-tabular"></a>表属性（SSAS 表格）
  本主题介绍表格模型表属性。 此处所述的属性不同于“编辑表属性”对话框中的那些属性，后者可以定义从源导入哪些列。  
  
 本主题的内容：  
  
-   [表属性](#bkmk_properties)  
  
-   [配置表属性设置](#bkmk_config_prop)  
  
##  <a name="table-properties"></a><a name="bkmk_properties"></a>表属性  
 **基本**  
  
|属性|默认设置|说明|  
|--------------|---------------------|-----------------|  
|**连接名称**|\<connection name>|与表的数据源的连接的名称。<br /><br /> 若要编辑连接，请单击该按钮。|  
|**Hidden**|错误|指定是否在报表客户端字段列表中隐藏表。|  
|**分区**||表的分区不能显示在 **“属性”** 窗口中。 若要查看、创建或编辑分区，请单击该按钮以打开分区管理器。|  
|**源数据**||表的源数据不能显示在 **“属性”** 窗口中。 若要查看或编辑源数据，请单击该按钮以打开“编辑表属性”对话框。|  
|**表说明**||表的文本说明。<br /><br /> 在 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]中，如果最终用户将光标置于字段列表的此表上方，则说明将以工具提示的形式出现。|  
|**表名**|\<friendly name>|指定表的友好名称。 当您使用“表导入向导”导入表时或在导入后的任意时间，可以指定表名。 模型中的表名可以不同于源的相关表名。 表的友好名称显示在报表客户端应用程序的字段列表以及 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的模型数据库中。|  
  
 **报表属性**  
  
 有关报表属性的详细说明和配置信息，请参阅 [Power View 报表属性（SSAS 表格）](properties-ssas-tabular.md)。  
  
|属性|默认设置|说明|  
|--------------|---------------------|-----------------|  
|**默认字段集**|||  
|表行为|||  
  
###  <a name="to-configure-table-property-settings"></a><a name="bkmk_config_prop"></a>配置表属性设置  
  
1.  在模型设计器中的数据视图中，单击某个表（选项卡）；或在关系图视图中，单击某个表头。  
  
2.  在 **“属性”** 窗口中，单击某个属性，然后键入值或单击其他配置选项的按钮。  
  
  
