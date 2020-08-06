---
title: "\"列可见性\" 对话框 (报表生成器) |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10127"
ms.assetid: 0c030cab-6087-45a5-99f0-c7bd693f20a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c775734a4dbba2120a2af86e35a3872f5fff718
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688624"
---
# <a name="column-visibility-dialog-box-report-builder"></a><span data-ttu-id="03164-102">“列可见性”对话框（报表生成器）</span><span class="sxs-lookup"><span data-stu-id="03164-102">Column Visibility Dialog Box (Report Builder)</span></span>
  <span data-ttu-id="03164-103">在报表首次运行时使用 **“列可见性”** 对话框来显示或隐藏选中的列，其他时候可通过此对话框使用另一报表项来切换该列的可见性。</span><span class="sxs-lookup"><span data-stu-id="03164-103">Use the **Column Visibility** dialog box to show or hide the selected column when the report is first run or to use another report item to toggle the visibility of the column.</span></span>  
  
## <a name="options"></a><span data-ttu-id="03164-104">选项</span><span class="sxs-lookup"><span data-stu-id="03164-104">Options</span></span>  
 <span data-ttu-id="03164-105">**在报表最初运行时**</span><span class="sxs-lookup"><span data-stu-id="03164-105">**When the report is initially run**</span></span>  
 <span data-ttu-id="03164-106">选择一个选项以指示报表项在报表中的初始显示方式。</span><span class="sxs-lookup"><span data-stu-id="03164-106">Select an option to indicate how the report item is initially displayed in the report.</span></span>  
  
 <span data-ttu-id="03164-107">**显示**</span><span class="sxs-lookup"><span data-stu-id="03164-107">**Show**</span></span>  
 <span data-ttu-id="03164-108">选择此选项可显示列。</span><span class="sxs-lookup"><span data-stu-id="03164-108">Choose this option to show the column.</span></span>  
  
 <span data-ttu-id="03164-109">**Hide**</span><span class="sxs-lookup"><span data-stu-id="03164-109">**Hide**</span></span>  
 <span data-ttu-id="03164-110">选择此选项可隐藏列。</span><span class="sxs-lookup"><span data-stu-id="03164-110">Choose this option to hide the Column.</span></span>  
  
 <span data-ttu-id="03164-111">**基于表达式显示或隐藏**</span><span class="sxs-lookup"><span data-stu-id="03164-111">**Show or hide based on an expression**</span></span>  
 <span data-ttu-id="03164-112">选择此选项可以使初始可见性根据表达式相应变化。</span><span class="sxs-lookup"><span data-stu-id="03164-112">Choose this option to vary the initial visibility using an expression.</span></span>  
  
 <span data-ttu-id="03164-113">键入计算结果为 `Boolean` 值的表达式，值为 `True` 时表示隐藏该项，值为 `False` 时表示显示该项。</span><span class="sxs-lookup"><span data-stu-id="03164-113">Type an expression that evaluates to a `Boolean` value of `True` to hide the item and `False` to show the item.</span></span> <span data-ttu-id="03164-114">单击“表达式” (*fx*) 按钮可编辑表达式。</span><span class="sxs-lookup"><span data-stu-id="03164-114">Click the Expression (*fx*) button to edit the expression.</span></span>  
  
 <span data-ttu-id="03164-115">**可以通过此报表项切换显示**</span><span class="sxs-lookup"><span data-stu-id="03164-115">**Display can be toggled by this report item**</span></span>  
 <span data-ttu-id="03164-116">选择此选项可以显示一个切换图像，用户可以使用该图像在 HTML 报表查看器中显示或隐藏此列。</span><span class="sxs-lookup"><span data-stu-id="03164-116">Choose this option to display a toggle image that enables the user to show or hide this column in an HTML report viewer.</span></span>  
  
 <span data-ttu-id="03164-117">您需要键入或选择报表中要用来显示切换图像的文本框的名称；例如，Textbox1。</span><span class="sxs-lookup"><span data-stu-id="03164-117">Type or select the name of a text box in the report in which to display a toggle image; for example, Textbox1.</span></span> <span data-ttu-id="03164-118">所选择的文本框必须在此报表项的当前或包含作用域中。</span><span class="sxs-lookup"><span data-stu-id="03164-118">The text box that you choose must be in the current or containing scope for this report item.</span></span> <span data-ttu-id="03164-119">例如，若要切换与子组关联的行的可见性，请在与父组关联的行中选择一个文本框。</span><span class="sxs-lookup"><span data-stu-id="03164-119">For example, to toggle visibility of rows associated with a child group, select a text box in a row associated with the parent group.</span></span> <span data-ttu-id="03164-120">若要切换图表的可见性，请选择一个与该图表位于同一包含作用域中的文本框；例如，表体或矩形。</span><span class="sxs-lookup"><span data-stu-id="03164-120">To toggle visibility of a chart, select a text box that is in the same containing scope as the chart; for example, the report body or a rectangle.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="03164-121">另请参阅</span><span class="sxs-lookup"><span data-stu-id="03164-121">See Also</span></span>  
 <span data-ttu-id="03164-122">[表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="03164-122">[Expression Examples &#40;Report Builder and SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="03164-123">[向项 &#40;报表生成器和 SSRS 添加展开或折叠操作&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="03164-123">[Add an Expand or Collapse Action to an Item &#40;Report Builder and SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="03164-124">[映像 &#40;报表生成器和 SSRS&#41;](report-design/images-report-builder-and-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="03164-124">[Images &#40;Report Builder and SSRS&#41;](report-design/images-report-builder-and-ssrs.md) </span></span>  
 <span data-ttu-id="03164-125">[报表生成器对话框、窗格和向导的帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md) </span><span class="sxs-lookup"><span data-stu-id="03164-125">[Report Builder Help for Dialog Boxes, Panes, and Wizards](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md) </span></span>  
 [<span data-ttu-id="03164-126">“图像属性”对话框 ->“常规”（报表生成器和 SSRS）</span><span class="sxs-lookup"><span data-stu-id="03164-126">Image Properties Dialog Box, General &#40;Report Builder and SSRS&#41;</span></span>](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
