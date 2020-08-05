---
title: 创建一个递归层次结构组（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf86c3989170ed8cd452168a558ead348258331e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580625"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>创建一个递归层次结构组（报表生成器和 SSRS）
  递归层次结构组可组织来自包含多个层次结构级别的单个报表数据集的数据。例如，表示组织层次结构中的经理－雇员关系的报告结构。  
  
 必须具有一个包含所有分层数据的数据集，并且要分组的项和作为分组依据的项都必须具有单独字段，才能将表中的数据组织为递归层次结构组。 例如，数据集可能包含姓名、雇员姓名、雇员 ID 和经理 ID，您希望以递归方式对经理级别以下的雇员进行分组。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>创建递归层次结构组  
  
1.  在“设计”视图中，添加一个表，然后拖动要显示的数据集字段。 通常，要显示为层次结构的字段位于第一列中。  
  
2.  右键单击表中的任意位置以选择该表。 “分组”窗格将显示所选表的详细信息组。 在“行组”窗格中，右键单击“详细信息”  ，然后单击“编辑组”  。 此时将打开 **“组属性”** 对话框。  
  
3.  在 **“组表达式”** 中，单击 **“添加”** 。 此时将在网格中显示一个新行。  
  
4.  在 **“分组方式”** 列表中，键入或选择要分组的字段。  
  
5.  单击“高级”。   
  
6.  在 **“递归父级”** 列表中，输入或选择要作为分组依据的字段。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     运行报表。 该报表将显示递归层次结构组，尽管并没有为显示该层次结构而进行缩进  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>使用缩进级别设置递归层次结构组的格式  
  
1.  单击包含特定字段的文本框，要向该字段添加缩进级别来显示层次结构格式。 该文本框的属性显示在“属性”窗格中。  
  
    > [!NOTE]  
    >  如果看不到“属性”窗格，请单击“视图”选项卡上的“属性”。    
  
2.  在 "属性" 窗格中，展开 `Padding` 节点，单击 "**左**"，然后从下拉列表中选择 **\<Expression...>** 。  
  
3.  在“表达式”窗格中，键入以下表达式：  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     “填充”属性需要  nnyy 格式的字符串，其中  nn 是一个数字，而  yy 是度量单位。 该示例表达式将生成一个字符串，该字符串使用 `Level` 函数根据递归级别增加填充的大小。 例如，级别为 1 的行会产生 (2 + (1\*10))=12pt 的填充，而级别为 3 的行会产生 (2 + (3\*10))=32pt 的填充。 有关函数的信息 `Level` ，请参阅[Level](report-builder-functions-level-function.md)。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     运行报表。 该报表将显示分组数据的层次结构视图。  
  
## <a name="see-also"></a>另请参阅  
 [创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)   
 [表（报表生成器和 SSRS）](tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
