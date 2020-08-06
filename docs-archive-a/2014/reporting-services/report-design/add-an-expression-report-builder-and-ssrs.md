---
title: 添加表达式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 16f414bfad47ae92681de50eb576a6ac2cb3f5fe
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687456"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>添加表达式（报表生成器和 SSRS）
  可在整个报表中使用表达式来定义报表项属性、筛选器、组、排序顺序、连接字符串和参数值。 表达式通常以等号 (=) 开头，以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 语言编写。 它们由报表处理器在运行时进行计算，报表处理器会将计算结果和报表布局元素相结合。  
  
 表达式可以是简单的，也可以是复杂的。 简单表达式引用内置集合中的单个项。 复杂表达式可以包括常量、运算符、全局集合项和函数调用。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>向文本框添加表达式  
  
-   在 **“设计”** 视图中，在设计图面上单击要向其添加表达式的文本框。  
  
    -   对于简单表达式，在文本框中键入该表达式的显示文本。 例如，对于数据集字段 Sales，键入 `[Sales]`。  
  
    -   对于复杂表达式，右键单击文本框，然后选择 **“表达式”** 。 此时将打开 **“表达式”** 对话框。 在“表达式”窗格中，在等号“=”后键入或交互方式创建表达式，然后单击“确定”。  
  
         该表达式将在设计图面上显示为 `<<Expr>>`。  
  
## <a name="see-also"></a>另请参阅  
 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [文本框（报表生成器和 SSRS）](text-boxes-report-builder-and-ssrs.md)   
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [筛选器公式示例（报表生成器和 SSRS）](filter-equation-examples-report-builder-and-ssrs.md)   
 [组表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [“表达式”对话框（报表生成器）](../expression-dialog-box-report-builder.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [向报表添加代码 (SSRS)](add-code-to-a-report-ssrs.md)  
  
  
