---
title: “数据集属性”对话框 ->“参数”| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10150"
- sql12.rtp.rptdesigner.datasetproperties.parameters.f1
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0073971de373321ce347f416657671e1f497dd1f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694283"
---
# <a name="dataset-properties-dialog-box-parameters"></a>“数据集属性”对话框 ->“参数”
  选择 **“数据集属性”** 对话框中的 **“参数”** 可以添加、更改和删除查询参数，包括链接到报表参数的查询参数。  
  
 无论何时在查询选项卡上更改查询，都会对查询命令进行分析。 对标识的每个查询参数，将创建其名称完全相同且区分大小写的报表参数。 默认情况下，查询参数将自动添加到查询参数列表中并链接到相应的报表参数。  
  
 如果某个报表参数的默认值与另一个链接到查询参数的报表参数存在依赖关系，则报表参数的顺序（即其在“报表参数属性”对话框中显示的顺序）十分重要  。 列表中后面的报表参数可以引用列表中前面的参数。 有关报表参数的详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="options"></a>选项  
 **添加**  
 将新的参数添加到列表。  
  
 **删除**  
 从列表中删除所选参数。  
  
 **参数名称**  
 键入添加到“数据集属性”  对话框“查询”  选项卡上数据集中的查询参数的名称。  
  
 **参数值**  
 输入查询参数的值。 此值既可以是静态值，也可以是引用报表内对象的表达式（但不能引用任何报表项或字段）。 默认情况下， **“值”** 中包含指向报表参数的表达式。  
  
 **向上键**  
 在列表中向上移动所选的参数。  
  
 **向下键**  
 在列表中向下移动所选的参数。  
  
## <a name="see-also"></a>另请参阅  
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)   
 [更改报表参数的顺序（报表生成器和 SSRS）](../report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
