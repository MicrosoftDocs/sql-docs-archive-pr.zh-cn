---
title: Foreach 循环编辑器 (的 "变量映射" 页) |Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd37c8c6c00f18d8b5493a058239cc880ecc1f5e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694527"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Foreach 循环编辑器（“变量映射”页）
  可以使用 **“Foreach 循环编辑器”** 对话框的 **“变量映射”** 页，将变量映射到集合值。 循环每次迭代时，都会用集合值更新变量的值。  
  
 若要了解如何在 Integration Services 包中使用 Foreach 循环容器，请参阅 [Foreach Loop Container](control-flow/foreach-loop-container.md) 。 若要了解如何配置该循环容器，请参阅 [配置 Foreach 循环容器](../../2014/integration-services/configure-a-foreach-loop-container.md)。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 教程“创建简单 ETL 包教程”包括一节介绍如何添加和配置 Foreach 循环的课程。  
  
## <a name="options"></a>选项  
 **变量**  
 选择现有变量或单击 \<**New variable...**> 以创建新变量。  
  
> [!NOTE]  
>  映射一个变量之后，“变量”  列表中会自动增加一行。  
  
 **相关主题**：[Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、[添加变量](../../2014/integration-services/add-variable.md)  
  
 **Index**  
 如果使用的是 Foreach Item 枚举器，请指定集合值中要映射到变量的列的索引。 对于其他枚举器类型，索引是只读的。  
  
> [!NOTE]  
>  索引以 0 为基数。  
  
 **相关主题**： [使用 Foreach 循环容器循环遍历 Excel 文件和表](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **删除**  
 选择一个变量，再单击“删除”  。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 循环编辑器 &#40;常规页&#41;](general-page-of-integration-services-designers-options.md)   
 [Foreach 循环编辑器 &#40;收集页面&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [For 循环容器](control-flow/for-loop-container.md)  
  
  
