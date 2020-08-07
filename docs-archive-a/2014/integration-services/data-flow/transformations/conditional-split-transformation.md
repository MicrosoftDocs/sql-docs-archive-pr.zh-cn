---
title: 有条件拆分转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittrans.f1
helpviewer_keywords:
- Conditional Split transformation
- route rows to different outputs [Integration Services]
ms.assetid: 3f8b5825-226f-413c-ba8f-0bb931ca3770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 96ff4b177992c329908ebc93df8f6220168e634d
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587941"
---
# <a name="conditional-split-transformation"></a><span data-ttu-id="bfc8e-102">有条件拆分转换</span><span class="sxs-lookup"><span data-stu-id="bfc8e-102">Conditional Split Transformation</span></span>
  <span data-ttu-id="bfc8e-103">有条件拆分转换可以根据数据内容将数据行路由到不同的输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-103">The Conditional Split transformation can route data rows to different outputs depending on the content of the data.</span></span> <span data-ttu-id="bfc8e-104">有条件拆分转换的实现类似于编程语言中的 CASE 决策结构。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-104">The implementation of the Conditional Split transformation is similar to a CASE decision structure in a programming language.</span></span> <span data-ttu-id="bfc8e-105">此转换将计算表达式，并且根据结果将数据行定向到指定输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-105">The transformation evaluates expressions, and based on the results, directs the data row to the specified output.</span></span> <span data-ttu-id="bfc8e-106">此转换还提供默认输出，因此，如果某行与任何表达式都不匹配，它会被定向到默认输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-106">This transformation also provides a default output, so that if a row matches no expression it is directed to the default output.</span></span>  
  
## <a name="configuration-of-the-conditional-split-transformation"></a><span data-ttu-id="bfc8e-107">有条件拆分转换的配置</span><span class="sxs-lookup"><span data-stu-id="bfc8e-107">Configuration of the Conditional Split Transformation</span></span>  
 <span data-ttu-id="bfc8e-108">可以按照下列方式配置有条件拆分转换：</span><span class="sxs-lookup"><span data-stu-id="bfc8e-108">You can configure the Conditional Split transformation in the following ways:</span></span>  
  
-   <span data-ttu-id="bfc8e-109">提供一个表达式，此表达式将转换要测试的每个条件都计算为一个布尔值。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-109">Provide an expression that evaluates to a Boolean for each condition you want the transformation to test.</span></span>  
  
-   <span data-ttu-id="bfc8e-110">指定计算条件的顺序。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-110">Specify the order in which the conditions are evaluated.</span></span> <span data-ttu-id="bfc8e-111">顺序很重要，因为行将被发送到对应于第一个计算结果为 true 的条件的输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-111">Order is significant, because a row is sent to the output corresponding to the first condition that evaluates to true.</span></span>  
  
-   <span data-ttu-id="bfc8e-112">指定转换的默认输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-112">Specify the default output for the transformation.</span></span> <span data-ttu-id="bfc8e-113">此转换要求指定默认输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-113">The transformation requires that a default output be specified.</span></span>  
  
 <span data-ttu-id="bfc8e-114">每个输入行只能被发送到一个输出，即第一个计算结果为 true 的条件的输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-114">Each input row can be sent to only one output, that being the output for the first condition that evaluates to true.</span></span> <span data-ttu-id="bfc8e-115">例如，下列条件将 **FirstName** 列中以字母 *A* 开头的所有行定向到一个输出，将以字母 *B* 开头的行定向到另一个输出，将所有其他行定向到默认输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-115">For example, the following conditions direct any rows in the **FirstName** column that begin with the letter *A* to one output, rows that begin with the letter *B* to a different output, and all other rows to the default output.</span></span>  
  
 <span data-ttu-id="bfc8e-116">输出 1</span><span class="sxs-lookup"><span data-stu-id="bfc8e-116">Output 1</span></span>  
  
 `SUBSTRING(FirstName,1,1) == "A"`  
  
 <span data-ttu-id="bfc8e-117">输出 2</span><span class="sxs-lookup"><span data-stu-id="bfc8e-117">Output 2</span></span>  
  
 `SUBSTRING(FirstName,1,1) == "B"`  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] <span data-ttu-id="bfc8e-118">包含的函数和运算符可用于创建计算输入数据并定向输出数据的表达式。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-118">includes functions and operators that you can use to create the expressions that evaluate input data and direct output data.</span></span> <span data-ttu-id="bfc8e-119">有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../../expressions/integration-services-ssis-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-119">For more information, see [Integration Services &#40;SSIS&#41; Expressions](../../expressions/integration-services-ssis-expressions.md).</span></span>  
  
 <span data-ttu-id="bfc8e-120">有条件拆分转换包括 `FriendlyExpression` 自定义属性。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-120">The Conditional Split transformation includes the `FriendlyExpression` custom property.</span></span> <span data-ttu-id="bfc8e-121">加载包时，可以通过属性表达式更新此属性。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-121">This property can be updated by a property expression when the package is loaded.</span></span> <span data-ttu-id="bfc8e-122">有关详细信息，请参阅 [在包中使用属性表达式](../../expressions/use-property-expressions-in-packages.md) 和 [转换自定义属性](transformation-custom-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-122">For more information, see [Use Property Expressions in Packages](../../expressions/use-property-expressions-in-packages.md) and [Transformation Custom Properties](transformation-custom-properties.md).</span></span>  
  
 <span data-ttu-id="bfc8e-123">此转换具有一个输入、一个或多个输出和一个错误输出。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-123">This transformation has one input, one or more outputs, and one error output.</span></span>  
  
 <span data-ttu-id="bfc8e-124">可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-124">You can set properties through [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer or programmatically.</span></span>  
  
 <span data-ttu-id="bfc8e-125">有关可以在 **“有条件拆分转换编辑器”** 对话框中设置的属性的详细信息，请参阅 [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md)。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-125">For more information about the properties that you can set in the **Conditional Split Transformation Editor** dialog box, see [Conditional Split Transformation Editor](../../conditional-split-transformation-editor.md).</span></span>  
  
 <span data-ttu-id="bfc8e-126">**“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。</span><span class="sxs-lookup"><span data-stu-id="bfc8e-126">The **Advanced Editor** dialog box reflects the properties that can be set programmatically.</span></span> <span data-ttu-id="bfc8e-127">有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：</span><span class="sxs-lookup"><span data-stu-id="bfc8e-127">For more information about the properties that you can set in the **Advanced Editor** dialog box or programmatically, click one of the following topics:</span></span>  
  
-   [<span data-ttu-id="bfc8e-128">Common Properties</span><span class="sxs-lookup"><span data-stu-id="bfc8e-128">Common Properties</span></span>](../../common-properties.md)  
  
-   [<span data-ttu-id="bfc8e-129">转换自定义属性</span><span class="sxs-lookup"><span data-stu-id="bfc8e-129">Transformation Custom Properties</span></span>](transformation-custom-properties.md)  
  
 <span data-ttu-id="bfc8e-130">有关如何设置属性的详细信息，请单击下列主题之一：</span><span class="sxs-lookup"><span data-stu-id="bfc8e-130">For more information about how to set properties, click one of the following topics:</span></span>  
  
-   [<span data-ttu-id="bfc8e-131">使用有条件拆分转换拆分数据集</span><span class="sxs-lookup"><span data-stu-id="bfc8e-131">Split a Dataset by Using the Conditional Split Transformation</span></span>](conditional-split-transformation.md)  
  
-   [<span data-ttu-id="bfc8e-132">设置数据流组件的属性</span><span class="sxs-lookup"><span data-stu-id="bfc8e-132">Set the Properties of a Data Flow Component</span></span>](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a><span data-ttu-id="bfc8e-133">Related Tasks</span><span class="sxs-lookup"><span data-stu-id="bfc8e-133">Related Tasks</span></span>  
 [<span data-ttu-id="bfc8e-134">使用有条件拆分转换拆分数据集</span><span class="sxs-lookup"><span data-stu-id="bfc8e-134">Split a Dataset by Using the Conditional Split Transformation</span></span>](conditional-split-transformation.md)  
  
## <a name="see-also"></a><span data-ttu-id="bfc8e-135">另请参阅</span><span class="sxs-lookup"><span data-stu-id="bfc8e-135">See Also</span></span>  
 <span data-ttu-id="bfc8e-136">[数据流](../data-flow.md) </span><span class="sxs-lookup"><span data-stu-id="bfc8e-136">[Data Flow](../data-flow.md) </span></span>  
 [<span data-ttu-id="bfc8e-137">Integration Services 转换</span><span class="sxs-lookup"><span data-stu-id="bfc8e-137">Integration Services Transformations</span></span>](integration-services-transformations.md)  
  
  