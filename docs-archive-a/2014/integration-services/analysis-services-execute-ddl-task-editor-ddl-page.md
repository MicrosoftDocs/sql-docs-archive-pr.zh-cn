---
title: Analysis Services (DDL 页上执行 DDL 任务编辑器) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asexecuteddltask.ddl.f1
helpviewer_keywords:
- Analysis Services Execute DDL Task Editor
ms.assetid: f21bf8d0-ec5f-4c18-9de0-8875addb927b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d207afe666e582c44f1014a6c80f4f4984fd5410
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579716"
---
# <a name="analysis-services-execute-ddl-task-editor-ddl-page"></a>Analysis Services 执行 DDL 任务编辑器（DDL 页）
  可以使用“Analysis Services 执行 DDL 任务编辑器”对话框的 **DDL** 页指定与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的连接，以及提供有关数据定义语言 (DDL) 语句的源的信息。  
  
 若要了解此任务，请参阅 [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md)。  
  
## <a name="static-options"></a>静态选项  
 **Connection**  
 在列表中选择 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 连接管理器，或者单击“\<**New connection...**>”并使用“添加 Analysis Services 连接管理器”对话框创建新的连接。  
  
 **相关主题：** [“添加 Analysis Services 连接管理器”对话框 UI 参考](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)、[Analysis Services 连接管理器](connection-manager/analysis-services-connection-manager.md)  
  
 **SourceType**  
 指定 DDL 语句的源类型。 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**直接输入**|将源设置为 **SourceDirect** 文本框中存储的 DDL 语句。 选择此值将显示以下部分中的动态选项。|  
|**文件连接**|将源设置为包含 DDL 语句的文件。 选择此值将显示以下部分中的动态选项。|  
|**变量**|将源设置为变量。 选择此值将显示以下部分中的动态选项。|  
  
## <a name="dynamic-options"></a>动态选项  
  
### <a name="sourcetype--direct-input"></a>SourceType = 直接输入  
 **数据源**  
 键入 DDL 语句，或单击省略号 (…)，然后在“DDL 语句”对话框中键入语句   。  
  
### <a name="sourcetype--file-connection"></a>SourceType = 文件连接  
 **数据源**  
 在列表中选择“文件连接”，或单击“\<**New connection...**>”并使用“文件连接管理器”对话框创建新的连接。  
  
 **相关主题：** [文件连接管理器](connection-manager/file-connection-manager.md)  
  
### <a name="sourcetype--variable"></a>SourceType = 变量  
 **数据源**  
 在列表中选择一个变量，或单击“\<**New variable...**>”并使用“添加变量”对话框创建新的变量。  
  
 **相关主题：** [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Analysis Services 在 "常规" 页上执行 DDL 任务编辑器 &#40;&#41;](general-page-of-integration-services-designers-options.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [控制流](control-flow/control-flow.md)   
 [Analysis Services 脚本语言 &#40;ASSL&#41; 参考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [XML for Analysis (XMLA) 参考](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference)  
  
  
