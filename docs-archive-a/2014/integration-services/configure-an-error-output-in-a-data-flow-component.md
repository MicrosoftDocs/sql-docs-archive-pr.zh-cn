---
title: 在数据流组件中配置错误输出 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ebd44383e27daa465576bb056a67f6dacad87b0a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693436"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>在数据流组件中配置错误输出
  很多数据流组件支持错误输出，根据组件的不同， [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器提供几种不同的错误输出配置方法。 除了配置错误输出外，您还可以配置错误输出的列。 其中包括配置由该组件添加的 **ErrorCode** 和 **ErrorColumn** 列。  
  
## <a name="configuring-an-error-output"></a>配置错误输出  
 若要配置错误输出，您有两种选择：  
  
-   使用 **“配置错误输出”** 对话框。 可以使用此对话框，在支持错误输出的任意数据流组件中配置错误输出。  
  
-   使用组件的编辑器对话框。 某些组件允许您直接从其编辑器对话框配置错误输出。 但是，您不能从以下组件的编辑器对话框配置错误输出：ADO NET 源、导入列转换、OLE DB 命令转换或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 目标。  
  
 下面的过程介绍如何使用这些对话框来配置错误输出。  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>使用“配置错误输出”对话框配置错误输出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“数据流”** 选项卡。  
  
4.  将红色箭头表示的错误输出从错误源组件拖到数据流中的另一个组件。  
  
5.  在 **“配置错误输出”** 对话框中，为组件输入中的每列在 **“错误”** 列和 **“截断”** 列中选择一个操作。  
  
6.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”** 。  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>使用组件的编辑器对话框添加错误输出  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“数据流”** 选项卡。  
  
4.  双击要在其中配置错误输出的数据流组件，然后根据不同组件，执行下列步骤之一：  
  
    -   单击 **“配置错误输出”** 。  
  
    -   单击 **“错误输出”** 。  
  
5.  为每列设置 **“错误”** 选项。  
  
6.  为每列设置 **“截断”** 选项。  
  
7.  单击“确定”。  
  
8.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”** 。  
  
## <a name="configuring-error-output-columns"></a>配置错误输出列  
 若要配置错误输出列，必须使用 **“高级编辑器”** 对话框中的 **“输入属性和输出属性”** 选项卡。  
  
#### <a name="to-configure-error-output-columns"></a>配置错误输出列  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，单击 **“数据流”** 选项卡。  
  
4.  右键单击要配置其错误输出列的组件，再单击“显示高级编辑器”  。  
  
5.  单击“输入和输出属性”选项卡并展开“\<component name> 错误输出”，然后展开“输出列”  。  
  
6.  单击某列，然后更新其属性。  
  
    > [!NOTE]  
    >  列的列表中包括组件输入中的列、由以前的错误输出添加的 **ErrorCode** 和 **ErrorColumn** 列，以及由此组件添加的 **ErrorCode** 和 **ErrorColumn** 列。  
  
7.  单击“确定” **。**  
  
8.  若要保存已更新的包，请在 **“文件”** 菜单中单击 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [数据中的错误处理](data-flow/error-handling-in-data.md)  
  
  
