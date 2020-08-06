---
title: 配置 For 循环容器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9cb33ea5b7f3f59baad3c94f6bc845c281613ec9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578363"
---
# <a name="configure-a-for-loop-container"></a><span data-ttu-id="0d1bf-102">配置 For 循环容器</span><span class="sxs-lookup"><span data-stu-id="0d1bf-102">Configure a For Loop Container</span></span>
  <span data-ttu-id="0d1bf-103">此过程介绍如何使用 **“For 循环编辑器”** 对话框配置 For 循环容器。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-103">This procedure describes how to configure a For Loop container by using the **For Loop Editor** dialog box.</span></span>  
  
### <a name="to-configure-the-for-loop-container"></a><span data-ttu-id="0d1bf-104">配置 For 循环容器</span><span class="sxs-lookup"><span data-stu-id="0d1bf-104">To configure the For Loop container</span></span>  
  
1.  <span data-ttu-id="0d1bf-105">在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，双击 For 循环容器，打开“For 循环编辑器”  。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-105">In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], double-click the For Loop container to open the **For Loop Editor**.</span></span>  
  
2.  <span data-ttu-id="0d1bf-106">根据需要，修改 For 循环容器的名称和说明。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-106">Optionally, modify the name and description of the For Loop container.</span></span>  
  
3.  <span data-ttu-id="0d1bf-107">根据需要，在 **InitExpression** 文本框中键入初始化表达式。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-107">Optionally, type an initialization expression in the **InitExpression** text box.</span></span>  
  
4.  <span data-ttu-id="0d1bf-108">在 **EvalExpression** 文本框中键入求值表达式。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-108">Type an evaluation expression in the **EvalExpression** text box.</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="0d1bf-109">表达式的计算结果必须为布尔值。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-109">The expression must evaluate to a Boolean.</span></span> <span data-ttu-id="0d1bf-110">当表达式的计算结果为 `false` 时，循环停止运行。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-110">When the expression evaluates to `false`, the loop stops running.</span></span>  
  
5.  <span data-ttu-id="0d1bf-111">根据需要，在 **AssignExpression** 文本框中键入赋值表达式。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-111">Optionally, type an assignment expression in the **AssignExpression** text box.</span></span>  
  
6.  <span data-ttu-id="0d1bf-112">根据需要，单击 **“表达式”** ，并在 **“表达式”** 页上为 For 循环容器的属性创建属性表达式。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-112">Optionally, click **Expressions** and, on the **Expressions** page, create property expressions for the properties of the For Loop container.</span></span> <span data-ttu-id="0d1bf-113">有关详细信息，请参阅 [添加或更改属性表达式](expressions/add-or-change-a-property-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-113">For more information, see [Add or Change a Property Expression](expressions/add-or-change-a-property-expression.md).</span></span>  
  
7.  <span data-ttu-id="0d1bf-114">单击 **“确定”** ，关闭 **“For 循环编辑器”** 。</span><span class="sxs-lookup"><span data-stu-id="0d1bf-114">Click **OK** to close the **For Loop Editor**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0d1bf-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0d1bf-115">See Also</span></span>  
 <span data-ttu-id="0d1bf-116">[For 循环容器](control-flow/for-loop-container.md) </span><span class="sxs-lookup"><span data-stu-id="0d1bf-116">[For Loop Container](control-flow/for-loop-container.md) </span></span>  
 <span data-ttu-id="0d1bf-117">[Integration Services &#40;SSIS&#41; 表达式](expressions/integration-services-ssis-expressions.md) </span><span class="sxs-lookup"><span data-stu-id="0d1bf-117">[Integration Services &#40;SSIS&#41; Expressions](expressions/integration-services-ssis-expressions.md) </span></span>  
 [<span data-ttu-id="0d1bf-118">在包中使用属性表达式</span><span class="sxs-lookup"><span data-stu-id="0d1bf-118">Use Property Expressions in Packages</span></span>](expressions/use-property-expressions-in-packages.md)  
  
  
