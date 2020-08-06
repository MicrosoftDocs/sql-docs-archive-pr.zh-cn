---
title: "\"平面文件目标编辑器\" (连接管理器页) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfiledestadapter.connection.f1
helpviewer_keywords:
- Flat File Destination Editor
ms.assetid: b01571fa-bc19-4742-8eed-ac163172a919
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6997b72851c2b7bfc56445e6ddb01cfe6e9b04cd
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578344"
---
# <a name="flat-file-destination-editor-connection-manager-page"></a>平面文件目标编辑器（“连接管理器”页）
  可以使用 **“平面文件目标编辑器”** 对话框的 **“连接管理器”** 页为目标选择平面文件连接，以及指定是覆盖现有目标文件还是追加到现有目标文件。 平面文件目标可以将数据写入文本文件。 该文本文件可以采用带分隔符、固定宽度、带有行分隔符的固定宽度或右边未对齐的格式。  
  
 若要了解有关平面文件目标的详细信息，请参阅 [Flat File Destination](data-flow/flat-file-destination.md)。  
  
## <a name="options"></a>选项  
 **平面文件连接管理器**  
 使用列表框选择现有的连接管理器，或单击“新建”  创建新的连接管理器。  
  
 **新建**  
 使用“平面文件格式”和“平面文件连接管理器编辑器”   对话框创建新的连接。  
  
 **“平面文件格式”** 对话框中除了提供带分隔符、固定宽度和右边未对齐这三种标准的平面文件格式外，还提供了第四个选项： **“固定宽度并使用行分隔符”** 。 此选项表示右边未对齐格式的一种特殊情况，在这种格式下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将添加一个虚列作为最后一个数据列。 此虚列可确保最后一列具有固定宽度。  
  
 **“固定宽度并使用行分隔符”** 选项在 **“平面文件连接管理器编辑器”** 中不可用。 如果需要，可以在该编辑器中模拟此选项。 若要模拟此选项，请在 **“平面文件连接管理器编辑器”** 的 **“常规”** 页上，为 **“格式”** 选择 **“右边未对齐”** 。 然后在该编辑器的 **“高级”** 页上，添加一个新的虚列作为最后一个数据列。  
  
 **覆盖文件中的数据**  
 指示是覆盖现有文件还是向现有文件中追加数据。  
  
 **标头**  
 键入在向文件中写入任何数据之前插入到该文件中的文本块。 使用此选项可以包括其他信息，如列标题。  
  
 **预览**  
 通过使用“数据视图”  对话框预览结果。 预览最多可以显示 200 行。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [平面文件目标编辑器（“映射”页）](../../2014/integration-services/flat-file-destination-editor-mappings-page.md)  
  
  
