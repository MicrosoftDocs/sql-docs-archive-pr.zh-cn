---
title: 使用 XMLA 创建数据挖掘查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content queries [DMX]
ms.assetid: 8f6b6008-006c-4792-9bd1-64c30dc3fd41
author: minewiskan
ms.author: owend
ms.openlocfilehash: d0e85b17db0781671fab0874706f12fdac95b30b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590448"
---
# <a name="create-a-data-mining-query-by-using-xmla"></a>使用 XMLA 创建数据挖掘查询
  可以使用 AMO、DMX 或 XML/A 创建针对数据挖掘对象的各种查询。  
  
 XML 用于 Analysis Services 服务器和所有客户端之间的通信。 因此，尽管使用 DMX 创建内容查询通常会更轻松，但还可使用 XML/A 中的 DISCOVER 和 COMMAND 语句编写这些查询，其间您既可以使用支持 SOAP 协议的客户端，也可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中创建 XML/A 查询。  
  
 本主题说明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的 XML/A 模板来创建针对当前服务器中存储的挖掘模型的模型内容查询。  
  
## <a name="querying-data-mining-schema-rowsets-by-using-xmla"></a>使用 XML/A 查询数据挖掘架构行集  
  
#### <a name="to-open-an-xmla-template"></a>打开 XML/A 模板  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的“视图”  菜单上，单击“模板资源管理器” 。  
  
2.  单击多维数据集图标以打开 Analysis Server 模板列表。  
  
3.  在模板类别列表中，展开 **XMLA**，再展开“架构行集”****，然后双击“发现架构行集”****，在合适的代码编辑器中打开该模板。  
  
4.  在 **“连接到 Analysis Services”** 对话框中，填写连接信息，再单击 **“连接”**。 此时将打开一个新的查询编辑器窗口，其中包含 **“发现架构行集”** 模板。  
  
#### <a name="to-discover-column-names-from-the-mining-model-content-schema-rowset"></a>从 MINING MODEL CONTENT 架构行集中发现列名  
  
1.  打开 **“发现架构行集”** 模板后，单击 **“执行”**。  
  
     **“结果”** 窗格中将显示返回的架构行集列表，该列表中包含当前实例中可用的所有行集的名称和行集列。  
  
2.  在**查询**窗格中，将光标置于后， **\<Restriction List>** 按 enter 添加新行。  
  
3.  将光标置于空行上，然后键入** \<SchemaName> DMSCHEMA_MINING_MODEL_CONTENT \</SchemaName> **  
  
     完整的限制部分应如下所示：  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<SchemaName>DMSCHEMA_MINING_MODEL_CONTENT</SchemaName>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
4.  单击“执行” 。  
  
     **“结果”** 窗格将显示指定架构行集的列名列表。  
  
#### <a name="to-create-a-content-query-using-the-mining-model-content-schema-rowset"></a>使用 MINING MODEL CONTENT 架构行集创建内容查询  
  
1.  在 **“发现架构行集”** 模板中，通过替换请求类型标记内的文本来更改请求类型。  
  
     将以下行：  
  
     `<RequestType>DISCOVER_SCHEMA_ROWSETS</RequestType>`  
  
     替换为以下行：  
  
     **\<RequestType>DMSCHEMA_MINING_MODEL_CONTENT\</RequestType>**  
  
2.  向限制列表添加新条件，将限制列表更改为按名称指定挖掘模型。  
  
3.  在模板中，将光标置于 `<Restriction List>` 之后，然后按 Enter 键以添加新行。  
  
4.  将光标置于空行上，然后键入 **<MODEL_NAME>My model name</MODEL_NAME>**  
  
     完整的限制部分应如下所示：  
  
     `<Restrictions>`  
  
     `<RestrictionList>`  
  
     `<MODEL_NAME>My model name</MODEL_NAME>`  
  
     `</RestrictionList>`  
  
     `</Restrictions>`  
  
5.  单击“执行” 。  
  
     “结果”窗格将显示架构定义以及指定模型的值。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型内容 &#40;Analysis Services 数据挖掘&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Data Mining Schema Rowsets](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
  
