---
title: 查找转换编辑器 (常规页) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa178118f7e090b6a3c15c7ab9347f322461f07b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688024"
---
# <a name="lookup-transformation-editor-general-page"></a>查找转换编辑器（“常规”页）
  可以使用“查找转换编辑器”对话框的 **“常规”** 页，选择缓存模式，选择连接类型以及指定如何处理没有匹配项的行。  
  
 若要了解有关查找转换的详细信息，请参阅 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)。  
  
## <a name="options"></a>选项  
 **完全缓存**  
 在执行查找转换前，生成引用数据集并将其加载到缓存中。  
  
 **部分缓存**  
 在执行查找转换的过程中生成引用数据集。 将在引用数据集内有匹配项的行加载到缓存中，并将数据集内没有匹配项的行加载到缓存中。  
  
 **无缓存**  
 在执行查找转换的过程中生成引用数据集。 不向缓存中加载任何数据。  
  
 **缓存连接管理器**  
 将查找转换功能配置为使用缓存连接管理器。 只有当选择了“完全缓存”选项时，此选项才可用。  
  
 **“无缓存”**  
 将查找转换功能配置为使用 OLE DB 连接管理器。  
  
 **指定如何处理无匹配项的行**  
 选择一个选项来处理在引用数据集内没有任何匹配项的行。  
  
 如果选中 **“将行重定向到无匹配输出”**，则行将重定向到无匹配输出，并且将不作为错误处理。 **“查找转换编辑器”** 对话框的 **“错误输出”** 页上的 **“错误”** 选项不可用。  
  
 如果选中 **“指定如何处理无匹配项的行”** 列表框中的任何其他选项，则行将作为错误处理。 **“错误输出”** 页上的 **“错误”** 选项不可用。  
  
## <a name="external-resources"></a>外部资源  
 blogs.msdn.com 上的博客文章： [查找缓存模式](https://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>另请参阅  
 [缓存连接管理器](connection-manager/cache-connection-manager.md)   
 [查找转换编辑器 &#40;连接页&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [查找转换编辑器 &#40;列 "页&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [查找转换编辑器 &#40;高级页面&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [查找转换编辑器（“错误输出”页）](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
