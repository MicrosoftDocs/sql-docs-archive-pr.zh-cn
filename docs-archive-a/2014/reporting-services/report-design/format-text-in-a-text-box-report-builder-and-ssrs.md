---
title: 设置文本框中文本的格式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 522bc420f77b2e5e9d2163c28d3d688b7c47883c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580579"
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>设置文本框中文本的格式（报表生成器和 SSRS）
  可以单独设置文本框中任何一部分文本的格式，并在一个文本框中混合使用占位符文本和静态文本。 这种混合格式并添加占位符文本的功能可使您能够为报表中的文本创建邮件合并或模板。 使用占位符可以单独定义任何表达式并设置其格式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>在一个文本框中组合多种格式  
  
1.  在 **“插入”** 选项卡上，单击 **“文本框”** 。 单击设计图面，然后拖动鼠标根据所需大小创建一个文本框。  
  
2.  在文本框内，选择要为其设置格式的文本。  
  
3.  右键单击所选文本，然后单击“文本属性”  。  
  
4.  设置格式设置选项。 例如，在 **“常规”** 选项卡上：  
  
    -   **工具提示** 键入文本或计算结果为工具提示的表达式。 当用户将鼠标指针停在报表中该项的上方时，便会显示此工具提示  
  
    -   **标记类型** 选择一个选项以指示所选文本的呈现方式：  
  
         **纯文本** ：将所选文本显示为简单文本。 HTML 将被视为文字文本。  
  
         **HTML**  ：将所选文本显示为 HTML。 如果占位符的表达式值包含有效的 HTML 标记，则这些标记将呈现为 HTML。 有关详细信息，请参阅[将 HTML 导入报表（报表生成器和 SSRS）](importing-html-into-a-report-report-builder-and-ssrs.md)。  
  
5.  单击“确定”。   
  
6.  对要为其设置格式的其余文本，重复步骤 2 到步骤 5。  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>在同一文本框中以不同方式设置文本和占位符的格式  
  
1.  在 **“插入”** 选项卡上，单击 **“列表”** 。 单击设计图面，然后拖动鼠标根据所需大小创建一个文本框。 此时将打开 **“数据集属性”** 对话框。 可以使用共享数据集或嵌入在报表中的数据集。 有关详细信息，请单击[“数据集属性”对话框 ->“查询”（报表生成器）](../report-data/dataset-properties-dialog-box-query-report-builder.md)或[“数据集属性”对话框 ->“查询”](../dataset-properties-dialog-box-query.md)。  
  
2.  在 **“插入”** 选项卡上，单击 **“文本框”** 。 在列表中单击，然后拖动鼠标根据所需大小创建一个文本框。  
  
3.  在文本框中键入一个标签，如 My Field:  。  
  
4.  将字段从数据集拖到文本框中。 此时将为您的字段创建一个占位符。  
  
5.  对于基本格式设置，请选择占位符文本，然后在 **“开始”** 选项卡上的 **“字体”** 组中，单击其中一个格式设置选项。例如，单击“加粗”  按钮。  
  
     要获得更多格式设置选项，请右键单击占位符文本，然后单击“占位符属性”  。  
  
6.  单击“确定”。  在报表设计视图中，文本框应包含“**My Field**: [*FieldName*]”，其中 *FieldName* 是你的字段的名称。  
  
7.  单击 **“运行”** 。  
  
 列表会将字段中的每个值重复一次，每次重复时， *FieldName* 占位符都会由数据集中该字段的值替换。  
  
## <a name="see-also"></a>另请参阅  
 [文本框（报表生成器和 SSRS）](text-boxes-report-builder-and-ssrs.md)   
 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [向报表添加 HTML（报表生成器和 SSRS）](add-html-into-a-report-report-builder-and-ssrs.md)   
 [列出 &#40;报表生成器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [设置数字和日期格式（报表生成器和 SSRS）](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [“占位符属性”对话框 ->“常规”（报表生成器和 SSRS）](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
