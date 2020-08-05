---
title: 更改域值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.values.f1
ms.assetid: 8c90ab70-3aea-4eaf-a174-4159485c87d3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 12ceac1f8614b05c5efe1de447a30916292beec3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580896"
---
# <a name="change-domain-values"></a><span data-ttu-id="0301a-102">更改域值</span><span class="sxs-lookup"><span data-stu-id="0301a-102">Change Domain Values</span></span>
  <span data-ttu-id="0301a-103">本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中更改和增加知识库中的元数据。</span><span class="sxs-lookup"><span data-stu-id="0301a-103">This topic describes how to change and augment the metadata in a knowledge base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).</span></span> <span data-ttu-id="0301a-104">通过知识发现生成知识，将知识导入到知识库或域中，或者使知识基于其他知识库之后，您可以通过交互方式更改数据值。</span><span class="sxs-lookup"><span data-stu-id="0301a-104">After you generate knowledge by knowledge discovery, import knowledge into the knowledge base or domains, or base a knowledge base upon another knowledge base, you can interactively change the data values.</span></span> <span data-ttu-id="0301a-105">知识库生成不仅利用计算机辅助过程，而且向您提供了一种方法，供您使用您的知识来验证数据值和按以下方式更改数据值：</span><span class="sxs-lookup"><span data-stu-id="0301a-105">Knowledge base generation not only leverages computer-assisted processes, but gives you the means to use your own knowledge to verify data values and change them in the following ways:</span></span>  
  
-   <span data-ttu-id="0301a-106">将域值添加到值列表中，或者选择一个值并且从列表中删除它</span><span class="sxs-lookup"><span data-stu-id="0301a-106">Add a domain value to the value list, or select a value and delete it from the list</span></span>  
  
-   <span data-ttu-id="0301a-107">将域值的状态从 DQS 发现过程所指定的状态更改为正确、错误或无效状态</span><span class="sxs-lookup"><span data-stu-id="0301a-107">Change the status of a domain value from what the DQS discovery process designates it as, changing it to correct, in-error, or not valid</span></span>  
  
-   <span data-ttu-id="0301a-108">为错误或无效的值输入替换值。</span><span class="sxs-lookup"><span data-stu-id="0301a-108">Enter a replacement value for a value that is in error or not valid.</span></span> <span data-ttu-id="0301a-109">如果某个值不属于某个域（例如，它不符合域数据类型或域规则失败），则该值无效。</span><span class="sxs-lookup"><span data-stu-id="0301a-109">A value is invalid if it does not belong in the domain, for example, if it does not conform to the domain data type or fails a domain rule.</span></span> <span data-ttu-id="0301a-110">如果某个值属于某个域，但有语法错误，则该值是错误的。</span><span class="sxs-lookup"><span data-stu-id="0301a-110">A value is in error if it belongs in the domain, but has a syntax error.</span></span>  
  
-   <span data-ttu-id="0301a-111">如果在创建域时设置了 **“使用前导值”** 属性，则将两个或更多的值设置为同义词，并更改发现过程所设置的前导值，结果是前导值将替换同义词值。</span><span class="sxs-lookup"><span data-stu-id="0301a-111">Set two or more values as synonyms and change the leading value as set by the discovery process, with the result that the leading value will replace the synonym value if the **Use Leading Value** property was set when you created the domain</span></span>  
  
-   <span data-ttu-id="0301a-112">从 Excel 文件导入域值</span><span class="sxs-lookup"><span data-stu-id="0301a-112">Import domain values from an Excel file</span></span>  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> <span data-ttu-id="0301a-113">开始之前</span><span class="sxs-lookup"><span data-stu-id="0301a-113">Before You Begin</span></span>  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a><span data-ttu-id="0301a-114">先决条件</span><span class="sxs-lookup"><span data-stu-id="0301a-114">Prerequisites</span></span>  
 <span data-ttu-id="0301a-115">若要更改域值，您必须具有知识库以及在域管理活动中打开了某个域。</span><span class="sxs-lookup"><span data-stu-id="0301a-115">To change a domain value, you must have a knowledge base and a domain opened in the Domain Management activity.</span></span>  
  
###  <a name="security"></a><a name="Security"></a> <span data-ttu-id="0301a-116">Security</span><span class="sxs-lookup"><span data-stu-id="0301a-116">Security</span></span>  
  
####  <a name="permissions"></a><a name="Permissions"></a> <span data-ttu-id="0301a-117">权限</span><span class="sxs-lookup"><span data-stu-id="0301a-117">Permissions</span></span>  
 <span data-ttu-id="0301a-118">您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能更改域值。</span><span class="sxs-lookup"><span data-stu-id="0301a-118">You must have the dqs_kb_editor or the dqs_administrator role on the DQS_MAIN database to change domain values.</span></span>  
  
##  <a name="change-domain-values"></a><a name="Change"></a><span data-ttu-id="0301a-119">更改域值</span><span class="sxs-lookup"><span data-stu-id="0301a-119">Change Domain Values</span></span>  
 <span data-ttu-id="0301a-120">**“值”** 表显示添加到某个单一域的知识库的知识。</span><span class="sxs-lookup"><span data-stu-id="0301a-120">The **Value** table displays knowledge added to the knowledge base for a single domain.</span></span> <span data-ttu-id="0301a-121">您可以随时在域列表中选择不同的域，以显示该域的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-121">You can select a different domain in the domain list at any time to display the values for that domain.</span></span> <span data-ttu-id="0301a-122">该字段中的列如下所示：</span><span class="sxs-lookup"><span data-stu-id="0301a-122">The columns in the field are the following:</span></span>  
  
-   <span data-ttu-id="0301a-123">**“值”** 列显示发现过程从数据样本中的字段添加到所选域的所有值。</span><span class="sxs-lookup"><span data-stu-id="0301a-123">The **Value** column displays all values that the discovery process added to the selected domain from a field in the data sample.</span></span> <span data-ttu-id="0301a-124">估测为错误的所有值都将显示为估测为正确的值的同义词。</span><span class="sxs-lookup"><span data-stu-id="0301a-124">Any value that is projected as an error will be shown as a synonym to a value that is projected as correct.</span></span>  
  
-   <span data-ttu-id="0301a-125">**“类型”** 列显示值的状态，该状态由发现过程确定。</span><span class="sxs-lookup"><span data-stu-id="0301a-125">The **Type** column displays the status of the value, as determined by the discovery process.</span></span> <span data-ttu-id="0301a-126">绿色对勾指示该值是正确的或已更正；红叉指示该值有误；带有感叹号的橙色三角形指示该值无效。</span><span class="sxs-lookup"><span data-stu-id="0301a-126">A green check indicates that the value is correct or corrected; a red cross indicates that the value is in error; and an orange triangle with an exclamation point indicates that the value is not valid.</span></span> <span data-ttu-id="0301a-127">无效的值不符合对该域的数据要求。</span><span class="sxs-lookup"><span data-stu-id="0301a-127">A value that is not valid does not conform to the data requirements for the domain.</span></span> <span data-ttu-id="0301a-128">有错误的值可能有效，但不是针对数据原因的正确值。</span><span class="sxs-lookup"><span data-stu-id="0301a-128">A value that is in error can be valid, but is not the correct value for data reasons.</span></span>  
  
-   <span data-ttu-id="0301a-129">**“更正为”** 列显示标记为错误或无效的原始值将更改为的正确值。</span><span class="sxs-lookup"><span data-stu-id="0301a-129">The **Correct To** column shows a correct value that the original value, marked as in error or not valid, will be changed to.</span></span> <span data-ttu-id="0301a-130">DQS 可将正确值作为发现过程的结果提出。</span><span class="sxs-lookup"><span data-stu-id="0301a-130">DQS can propose the correct value as a result of the discovery process.</span></span>  
  
 <span data-ttu-id="0301a-131">若要更改值，请继续执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0301a-131">To change values, proceed as follows:</span></span>  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)]<span data-ttu-id="0301a-132">[运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-132">[Run the Data Quality Client Application](../../2014/data-quality-services/run-the-data-quality-client-application.md).</span></span>  
  
2.  <span data-ttu-id="0301a-133">在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。</span><span class="sxs-lookup"><span data-stu-id="0301a-133">In the [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] home screen, open or create a knowledge base.</span></span> <span data-ttu-id="0301a-134">选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。</span><span class="sxs-lookup"><span data-stu-id="0301a-134">Select **Domain Management** as the activity, and then click **Open** or **Create**.</span></span> <span data-ttu-id="0301a-135">有关详细信息，请参阅 [创建知识库](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../../2014/data-quality-services/open-a-knowledge-base.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-135">For more information, see [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md) or [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="0301a-136">域管理在 Data Quality Service 客户端页面中执行，该页面包含用于单独域管理操作的五个选项卡。</span><span class="sxs-lookup"><span data-stu-id="0301a-136">Domain management is performed in a page of the Data Quality Service client that contains five tabs for separate domain management operations.</span></span> <span data-ttu-id="0301a-137">它不是一个向导驱动的过程；任何管理操作都可以单独执行。</span><span class="sxs-lookup"><span data-stu-id="0301a-137">It is not a wizard-driven process; any management operation can be performed separately.</span></span>  
  
3.  <span data-ttu-id="0301a-138">从 **“域管理”** 页上的 **“域列表”** 中，选择您要在其中更改值的域或创建一个新域。</span><span class="sxs-lookup"><span data-stu-id="0301a-138">From the **Domain list** on the **Domain Management** page, select the domain that you want to change values in or create a new domain.</span></span> <span data-ttu-id="0301a-139">如果您必须创建新域，请参阅 [创建域](../../2014/data-quality-services/create-a-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-139">If you have to create a new domain, see [Create a Domain](../../2014/data-quality-services/create-a-domain.md).</span></span> <span data-ttu-id="0301a-140">单击 **“域值”** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="0301a-140">Click the **Domain Values** tab.</span></span>  
  
4.  <span data-ttu-id="0301a-141">在 **“值”** 表中显示需要修改的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-141">Display the values that you need to modify in the **Value** table.</span></span> <span data-ttu-id="0301a-142">有关详细信息，请参阅下方的 [如何显示适当的值](#Display) 。</span><span class="sxs-lookup"><span data-stu-id="0301a-142">For more information, see [How to Display the Appropriate Values](#Display) below.</span></span>  
  
5.  <span data-ttu-id="0301a-143">若要更改某个值的状态，请继续执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0301a-143">To change a value's state, proceed as follows:</span></span>  
  
    -   <span data-ttu-id="0301a-144">**将所选域值设为已更正**：若要将某个值的状态从 "错误" 或 "无效" 更改为 "正确"，请选择该值，然后单击 "**将所选域值设为已更正**" (从图标栏中的向下箭头或从 "类型" 下拉列表中选中) 。</span><span class="sxs-lookup"><span data-stu-id="0301a-144">**Set selected domain values as corrected**: To change a value's state from Error or Invalid to Correct, select the value, and then click the **Set selected domain values as corrected** (check) from the down-arrow in the icon bar or from the Type drop-down list.</span></span> <span data-ttu-id="0301a-145">如果有错误或无效的值与某一正确值组合在一起，则在该操作后删除该值。</span><span class="sxs-lookup"><span data-stu-id="0301a-145">If the in-error or invalid value is grouped with a correct value, delete that value after the operation.</span></span>  
  
    -   <span data-ttu-id="0301a-146">**将所选域值设为错误**：若要将某个值的状态从 "正确" 或 "无效" 更改为 "错误"，请选择该值，然后单击 "**将所选域值设为错误**" (跨图标栏中的向下箭头或从 "类型" 下拉列表中) 图标。</span><span class="sxs-lookup"><span data-stu-id="0301a-146">**Set selected domain values as errors**: To change a value's state from Correct or Invalid to Error, select the value, and then click the **Set selected domain values as errors** (cross) icon from the down-arrow in the icon bar or from the Type drop-down list.</span></span> <span data-ttu-id="0301a-147">您可以在 **“更正为”** 列中输入更正值，或者将其保留为空白。</span><span class="sxs-lookup"><span data-stu-id="0301a-147">You can either enter a correction in the **Correct to** column, or leave it blank.</span></span>  
  
    -   <span data-ttu-id="0301a-148">**将所选域值设为无效**：若要将某个值的状态从 "正确" 或 "错误" 更改为 "无效"，请选择该值，然后单击图标栏中的向下箭头或从 "类型" 下拉列表中的 "**将所选域值设为无效** (三角形) 图标。</span><span class="sxs-lookup"><span data-stu-id="0301a-148">**Set selected domain values as invalid**: To change a value's state from Correct or Error to Invalid, select the value, and then click the **Set selected domain values as invalid** (triangle) icon from the down-arrow in the icon bar or from the Type drop-down list.</span></span> <span data-ttu-id="0301a-149">您可以在 **“更正为”** 列中输入更正值，或者将其保留为空白。</span><span class="sxs-lookup"><span data-stu-id="0301a-149">You can either enter a correction in the **Correct to** column, or leave it blank.</span></span>  
  
    -   <span data-ttu-id="0301a-150">**更正为**：在将某个值设置为有错误或无效后，在 **“更正为”** 列中输入一个新值。</span><span class="sxs-lookup"><span data-stu-id="0301a-150">**Correct to**: After setting a value as in error or invalid, enter a new value in the **Correct To** column.</span></span> <span data-ttu-id="0301a-151">DQS 将为更换值添加一个新行，将其指定为正确，然后组合这两个值。</span><span class="sxs-lookup"><span data-stu-id="0301a-151">DQS will add a new row for the replacement value, designate it as correct, and then group the two values.</span></span> <span data-ttu-id="0301a-152">这个新值将显示为前导值，前导值为粗体，而有错误或无效值是缩进的。</span><span class="sxs-lookup"><span data-stu-id="0301a-152">The new value will be shown as the leading value, with the leading value in bold and the in-error or invalid value indented.</span></span>  
  
6.  <span data-ttu-id="0301a-153">若要将值指定为一组同义词，则选择正确的多个值，然后继续如下操作：</span><span class="sxs-lookup"><span data-stu-id="0301a-153">To designate values as a group of synonyms, select multiple values that are correct, and then proceed as follows:</span></span>  
  
    -   <span data-ttu-id="0301a-154">**将所选域值设为同义词**：若要设置同义词，请选择多个正确的值，然后单击 **“将所选域值设为同义词”** 图标。</span><span class="sxs-lookup"><span data-stu-id="0301a-154">**Set selected domain values as synonyms**: To set synonyms, select multiple values that are correct, and then click the **Set selected domain values as synonyms** icon.</span></span> <span data-ttu-id="0301a-155">DQS 将对值进行分组，然后将这些值之一指定为将用来替换其他值的前导值。</span><span class="sxs-lookup"><span data-stu-id="0301a-155">DQS will group the values and designate one of the values as the leading value that the others will be replaced with.</span></span> <span data-ttu-id="0301a-156">注意，如果对两个值分组，但组中的一个值是错误的或无效，则值不是同义词。</span><span class="sxs-lookup"><span data-stu-id="0301a-156">Note that if two values are grouped, but one of the group is in-error or invalid, the values are not synonyms.</span></span>  
  
        > [!NOTE]  
        >  <span data-ttu-id="0301a-157">如果您在一个组中选择两个或更多值，并且在该组之外选择另一个值，然后将它们设置为同义词，则系统将会向您显示不正确的错误消息。</span><span class="sxs-lookup"><span data-stu-id="0301a-157">If you select two or more values in a group and another value outside the group, and then set them as synonyms, you will get an incorrect error message.</span></span> <span data-ttu-id="0301a-158">在关闭错误消息弹出窗口后，这些值将正确设置为同义词。</span><span class="sxs-lookup"><span data-stu-id="0301a-158">After closing the error message popup, the values will be set correctly as synonyms.</span></span>  
  
    -   <span data-ttu-id="0301a-159">**断开所选同义词之间的关系**：若要撤消针对两个或更多值的同义词指定，请选择这些值，然后单击 **“断开所选同义词之间的关系”** 图标。</span><span class="sxs-lookup"><span data-stu-id="0301a-159">**Break relation between selected synonyms**: To undo the synonym designation for two or more values, select the values and then click the **Break relation between selected synonyms** icon.</span></span> <span data-ttu-id="0301a-160">值必须进行分组并必须都是正确的，才能取消同义词的分组。</span><span class="sxs-lookup"><span data-stu-id="0301a-160">The values must be grouped and must both be correct for the ungrouping of synonyms to work.</span></span>  
  
    -   <span data-ttu-id="0301a-161">**将所选域值设为其组的前导值**：若要更改该组的前导值，请在组中选择未指定为前导值的一个值，然后单击 **“将所选域值设为其组的前导值”** 按钮。</span><span class="sxs-lookup"><span data-stu-id="0301a-161">**Set selected domain value as a leading value of its group**: To change the leading value of the group, select a value in the group that is not designated as the leading value, and then click the **Set selected domain value as a leading value of its group** button.</span></span> <span data-ttu-id="0301a-162">这会将前导值设置为另一个值的替代值。</span><span class="sxs-lookup"><span data-stu-id="0301a-162">This will set the leading value as a replacement for the other value.</span></span> <span data-ttu-id="0301a-163">只有将两个或更多属于组的值设置为同义词，并且您要更改 DQS 所指定的主导值时，此操作才有效。</span><span class="sxs-lookup"><span data-stu-id="0301a-163">This operation works only if you have set two or more values that are group, and you want to change the leading value from the value designated by DQS.</span></span> <span data-ttu-id="0301a-164">请注意，前导值由蓝色行且值由粗体显示来指示。</span><span class="sxs-lookup"><span data-stu-id="0301a-164">Note that the leading value is designated by a blue row with the value in bold.</span></span>  
  
7.  <span data-ttu-id="0301a-165">**拼写检查器**：如果值有红色的波浪下划线，则拼写检查器正在建议对值的更正。</span><span class="sxs-lookup"><span data-stu-id="0301a-165">**Speller**: If a value has a wavy red underscore, the Speller is suggesting a correction to the value.</span></span> <span data-ttu-id="0301a-166">右键单击带下划线的值，然后选择一个更正值（如果有适用的更正）。</span><span class="sxs-lookup"><span data-stu-id="0301a-166">Right-click the value with the underscore, and select a correction if one applies.</span></span> <span data-ttu-id="0301a-167">值类型变为（或仍保持为）错误，并且更正将被添加到 **“更正为”** 列。</span><span class="sxs-lookup"><span data-stu-id="0301a-167">The value type becomes (or stays as) error, and the correction will be added to the **Correct to** column.</span></span> <span data-ttu-id="0301a-168">单击向下箭头可查看其他建议的更正。</span><span class="sxs-lookup"><span data-stu-id="0301a-168">Click the down arrow to see additional proposed corrections.</span></span> <span data-ttu-id="0301a-169">手动输入一个更正并且将其添加到拼写检查器字典，并且能够将其作为更正选择。</span><span class="sxs-lookup"><span data-stu-id="0301a-169">Enter a correction manually to add it to the Speller dictionary, and be able to select it as a correction.</span></span> <span data-ttu-id="0301a-170">有关详细信息，请参阅 [使用 DQS 拼写检查器](../../2014/data-quality-services/use-the-dqs-speller.md) 和 [设置域属性](../../2014/data-quality-services/set-domain-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-170">For more information, see [Use the DQS Speller](../../2014/data-quality-services/use-the-dqs-speller.md) and [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).</span></span>  
  
    > [!NOTE]  
    >  <span data-ttu-id="0301a-171">若要使用拼写检查器，您或者可以在 **“域属性”** 页中启用它，或者如果已在 **“域属性”** 页中禁用它，则可以在 **“域值”** 页中单击 **“启用/禁用拼写检查器”** 图标以便在该页上启用它。</span><span class="sxs-lookup"><span data-stu-id="0301a-171">To use the Speller, you can either enable it in the **Domain Properties** page, or if it is disabled in the **Domain Properties** page, you can click the **Enable/Disable Speller** icon on the **Domain Values** page to enable it on that page.</span></span>  
  
8.  <span data-ttu-id="0301a-172">**添加新的域值**：单击以在行尾添加一行。</span><span class="sxs-lookup"><span data-stu-id="0301a-172">**Add new domain value**: Click to add a row at the end of the table.</span></span> <span data-ttu-id="0301a-173">在输入值后，该行将以字母顺序重新定位，并将通过在前面加上星号字符定义为新条目。</span><span class="sxs-lookup"><span data-stu-id="0301a-173">After you enter a value, the row will be repositioned in alphabetical order, and will be identified as a new entry by a preceding star symbol.</span></span>  
  
9. <span data-ttu-id="0301a-174">**从 Excel 导入域值**：若要从 Excel 电子表格添加新值，请单击 **“导入值”** 图标的向下箭头，然后选择 **“从 Excel 导入域值”**，。</span><span class="sxs-lookup"><span data-stu-id="0301a-174">**Import domain values from Excel**: To add new values from an Excel spreadsheet, click the down arrow for the **Import Values** icon, and then select **Import domain values from Excel**.</span></span> <span data-ttu-id="0301a-175">输入文件名，根据需要选择 **“将第一行用作标头”** ，然后单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0301a-175">Enter the file name, select **Use first row as header** if appropriate, and then click **OK**.</span></span> <span data-ttu-id="0301a-176">有关详细信息，请参阅 [将值从 Excel 文件导入到域](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-176">For more information, see [Import Values from an Excel File into a Domain](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md).</span></span>  
  
10. <span data-ttu-id="0301a-177">**从 Excel 导入项目值**：若要从数据质量项目添加新值，请单击 **“导入值”** 图标的向下箭头，然后选择 **“从 Excel 导入项目值”**。</span><span class="sxs-lookup"><span data-stu-id="0301a-177">**Import project values**: To add new values from a Data Quality Project by clicking the down arrow for the **Import Values** icon, and selecting **Import project values**.</span></span> <span data-ttu-id="0301a-178">输入文件名，根据需要选择 **“将第一行用作标头”** ，然后单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0301a-178">Enter the file name, select **Use first row as header** if appropriate, and then click **OK**.</span></span> <span data-ttu-id="0301a-179">选择您从中导入值的项目，然后单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="0301a-179">Select the project that you want to import values from, and then click **OK**.</span></span> <span data-ttu-id="0301a-180">将显示导入的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-180">The imported values will be displayed.</span></span> <span data-ttu-id="0301a-181">单击“完成”。</span><span class="sxs-lookup"><span data-stu-id="0301a-181">Click **Finish**.</span></span> <span data-ttu-id="0301a-182">有关详细信息，请参阅“将项目值导入到域中”。</span><span class="sxs-lookup"><span data-stu-id="0301a-182">For more information, see Import Project Values into a Domain.</span></span>  
  
11. <span data-ttu-id="0301a-183">**删除所选域值**：若要从域中删除一个或多个现有值，请在“值”表中选择值，然后单击 **“删除所选域值”** 图标。</span><span class="sxs-lookup"><span data-stu-id="0301a-183">**Delete selected domain value(s)**: To remove one or more existing values from the domain, select the values in the Value table, and then click the **Delete selected domain value(s)** icon.</span></span> <span data-ttu-id="0301a-184">无法删除 DQS_NULL 的项，因此，如果您选择要删除的多个值，并且 DQS_NULL 的项是其中之一，则操作将失败。</span><span class="sxs-lookup"><span data-stu-id="0301a-184">An entry of DQS_NULL cannot be deleted, so if you choose multiple values to delete, and an entry of DQS_NULL is one of them, the operation will fail.</span></span>  
  
12. <span data-ttu-id="0301a-185">单击 **“完成”** 以完成域管理活动，如 [结束域管理活动](../../2014/data-quality-services/end-the-domain-management-activity.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="0301a-185">Click **Finish** to complete the domain management activity, as described in [End the Domain Management Activity](../../2014/data-quality-services/end-the-domain-management-activity.md).</span></span>  
  
##  <a name="follow-up-after-changing-domain-values"></a><a name="FollowUp"></a> <span data-ttu-id="0301a-186">跟进：更改域值后</span><span class="sxs-lookup"><span data-stu-id="0301a-186">Follow Up: After Changing Domain Values</span></span>  
 <span data-ttu-id="0301a-187">在更改域值后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。</span><span class="sxs-lookup"><span data-stu-id="0301a-187">After you change domain values, you can perform other domain management tasks on the domain, you can perform knowledge discovery to add knowledge to the domain, or you can add a matching policy to the domain.</span></span> <span data-ttu-id="0301a-188">有关详细信息，请参阅[执行知识发现](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理域](../../2014/data-quality-services/managing-a-domain.md)或[创建匹配策略](../../2014/data-quality-services/create-a-matching-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="0301a-188">For more information, see [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md), [Managing a Domain](../../2014/data-quality-services/managing-a-domain.md), or [Create a Matching Policy](../../2014/data-quality-services/create-a-matching-policy.md).</span></span>  
  
##  <a name="the-meaning-of-correct-error-and-invalid-values"></a><a name="Meaning"></a> <span data-ttu-id="0301a-189">正确、错误和无效值的含义</span><span class="sxs-lookup"><span data-stu-id="0301a-189">The Meaning of Correct, Error, and Invalid Values</span></span>  
 <span data-ttu-id="0301a-190">**“域值”** 页的 **“值”** 表中的每个值都将被分配 **“正确”** 、 **“错误”** 或 **“无效”** 的 **“类型”** 设置。</span><span class="sxs-lookup"><span data-stu-id="0301a-190">Each value in the **Value** table of the **Domain Values** page is assigned a **Type** setting of **Correct**, **Error**, or **Invalid**.</span></span> <span data-ttu-id="0301a-191">值的类型最初由知识发现活动生成，并且您可以在适合时更改该值。</span><span class="sxs-lookup"><span data-stu-id="0301a-191">The type of the value is generated initially by the knowledge discovery activity, and you can change it as you see fit.</span></span> <span data-ttu-id="0301a-192">清理活动将基于知识发现和交互更改生成最终类型。</span><span class="sxs-lookup"><span data-stu-id="0301a-192">The final type, based upon both discovery and interactive changes, is generated by the cleansing activity.</span></span> <span data-ttu-id="0301a-193">这些设置将具有以下含义：</span><span class="sxs-lookup"><span data-stu-id="0301a-193">These settings have the following meanings:</span></span>  
  
-   <span data-ttu-id="0301a-194">**正确：** 这是属于域并且没有任何语法错误的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-194">**Correct:** This is a value that belongs to the domain and does not have any syntax errors.</span></span> <span data-ttu-id="0301a-195">例如，City 域中的“Chicago”是正确的。</span><span class="sxs-lookup"><span data-stu-id="0301a-195">For example, "Chicago" in a City domain is correct.</span></span>  
  
-   <span data-ttu-id="0301a-196">**错误：** 这是属于域但不正确的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-196">**Error:** This is a value that belongs to the domain, but is an incorrect value.</span></span> <span data-ttu-id="0301a-197">例如，City 域中的“Shicago”（而非“Chicago”）是有错误的。</span><span class="sxs-lookup"><span data-stu-id="0301a-197">For example, "Shicago" instead of "Chicago" in a City domain is in error.</span></span> <span data-ttu-id="0301a-198">DQS 将其检测到有语法错误的值指定为有错误并且在发现过程中指定关联的更正。</span><span class="sxs-lookup"><span data-stu-id="0301a-198">DQS designates a value as in error it detects a syntax error and an associated correction in the discovery process.</span></span> <span data-ttu-id="0301a-199">语法错误包括拼写错误。</span><span class="sxs-lookup"><span data-stu-id="0301a-199">Syntax errors include misspellings.</span></span>  
  
-   <span data-ttu-id="0301a-200">**无效：** 这是不属于域并且没有更正的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-200">**Invalid:** This is a value that does not belong to the domain, and does not have a correction.</span></span> <span data-ttu-id="0301a-201">例如，City 域中的“12345”无效。</span><span class="sxs-lookup"><span data-stu-id="0301a-201">For example, the value "12345" in a City domain is invalid.</span></span> <span data-ttu-id="0301a-202">DQS 在某个值未能通过域规则时将其指定为无效。</span><span class="sxs-lookup"><span data-stu-id="0301a-202">DQS designates a value as invalid when it fails a domain rule.</span></span>  
  
 <span data-ttu-id="0301a-203">您可以手动将某个值的类型更改为两个其他值之一。</span><span class="sxs-lookup"><span data-stu-id="0301a-203">You can manually change the Type of a value to either of the two other values.</span></span> <span data-ttu-id="0301a-204">DQS 对手动操作不强制有效性和错误语义。</span><span class="sxs-lookup"><span data-stu-id="0301a-204">DQS does not enforce validity and error semantics on manual operations.</span></span> <span data-ttu-id="0301a-205">您可以为无效值输入更正而不更改其状态。</span><span class="sxs-lookup"><span data-stu-id="0301a-205">You can enter a correction for an Invalid value without changing its status.</span></span> <span data-ttu-id="0301a-206">即使某个值未通过域规则，您也可以将其指定为无效。</span><span class="sxs-lookup"><span data-stu-id="0301a-206">You can designate a value as invalid even if it did not fail a domain rule.</span></span> <span data-ttu-id="0301a-207">即使发现过程未指示某个值具有语法错误，您也可以将其指定为存在错误。</span><span class="sxs-lookup"><span data-stu-id="0301a-207">You can designate a value as in error even if the discovery process did not indicate that it has a syntax error.</span></span> <span data-ttu-id="0301a-208">您也可以删除对错误值的更正（这将标记为正确），而不更改其状态。</span><span class="sxs-lookup"><span data-stu-id="0301a-208">You can also remove a correction to an Error value, which is marked as Correct, without changing its status.</span></span>  
  
 <span data-ttu-id="0301a-209">当您在 **“清理”** 活动的 **“管理和查看结果”** 页中执行交互式数据清理时，无效和有错误的值都将包含在 **“管理和查看结果”** 页的 **“无效”** 选项卡上。</span><span class="sxs-lookup"><span data-stu-id="0301a-209">When you are performing interactive data cleansing in the **Manage and View Results** page of the **Cleansing** activity, both invalid and in-error values are included in the **Invalid** tab on the **Manage and View Results** page.</span></span>  
  
##  <a name="how-to-display-the-appropriate-values"></a><a name="Display"></a> <span data-ttu-id="0301a-210">如何显示适当的值</span><span class="sxs-lookup"><span data-stu-id="0301a-210">How to Display the Appropriate Values</span></span>  
 <span data-ttu-id="0301a-211">您可以按如下所示修改显示：</span><span class="sxs-lookup"><span data-stu-id="0301a-211">You can modify the display as follows:</span></span>  
  
-   <span data-ttu-id="0301a-212">通过在 **“筛选器”** 下拉列表中选择状态，基于其状态筛选 **“筛选器”** 要处于表中的结果。</span><span class="sxs-lookup"><span data-stu-id="0301a-212">**Filter** the results that you want in the table, based on their status, by selecting the status in the **Filter** drop-down list.</span></span>  
  
-   <span data-ttu-id="0301a-213">通过在 **“查找”** 文本框中输入要搜索的一个或多个字母，查找 **“查找”** 要检查或修改的数据。</span><span class="sxs-lookup"><span data-stu-id="0301a-213">**Find** the data that you want to check or modify by entering one more letters to search for in the **Find** text box.</span></span> <span data-ttu-id="0301a-214">这将突出显示在显示的任何值中出现的那些字母。</span><span class="sxs-lookup"><span data-stu-id="0301a-214">This will highlight have those letters wherever they occur in any value that is displayed.</span></span>  
  
-   <span data-ttu-id="0301a-215">单击 **“仅显示新内容”** 会将在表中显示的值限制为仅限在当前会话（而非之前的会话）中发现的值。</span><span class="sxs-lookup"><span data-stu-id="0301a-215">Click **Show Only New** to restrict the values displayed in the table only to values that were discovered in the current session, not previous sessions.</span></span>  
  
-   <span data-ttu-id="0301a-216">单击 **“全部展开”** 按钮可在折叠当前状态时显示任何同义词组中的所有值。</span><span class="sxs-lookup"><span data-stu-id="0301a-216">Click the **Expand All** button to display all values in any group of synonyms when the current state is collapsed.</span></span>  
  
-   <span data-ttu-id="0301a-217">单击 **“全部折叠”** 按钮可在展开当前状态时隐藏任何同义词组中除前导值之外的所有值。</span><span class="sxs-lookup"><span data-stu-id="0301a-217">Click the **Collapse All** button to hide all but the leading value in any group of synonyms when the current state is expanded.</span></span>  
  
-   <span data-ttu-id="0301a-218">单击 **“显示/隐藏域值更改历史记录面板”** 按钮可在值表的底部显示一个预览弹出窗口，该窗口显示对域值集合的最近更改。</span><span class="sxs-lookup"><span data-stu-id="0301a-218">Click the **Show/Hide the Domain Values Changes History Panel** button to display a preview popup at the bottom of the values table that shows recent changes to the domain values collection.</span></span>  
  
##  <a name="how-to-handle-null-equivalents"></a><a name="Null"></a> <span data-ttu-id="0301a-219">如何处理 Null 等效项</span><span class="sxs-lookup"><span data-stu-id="0301a-219">How to Handle Null Equivalents</span></span>  
 <span data-ttu-id="0301a-220">**“域值”** 选项卡中的每个值表都包含一个 DQS_NULL 值。</span><span class="sxs-lookup"><span data-stu-id="0301a-220">Each value table in the **Domain Values** tab includes a DQS_NULL value.</span></span> <span data-ttu-id="0301a-221">在值表中，数据源中的 Null 将显示为 SQL_NULL。</span><span class="sxs-lookup"><span data-stu-id="0301a-221">A null in a data source will appear as SQL_NULL in the value table.</span></span> <span data-ttu-id="0301a-222">您可以将一个或多个 null 等效值设置为 DQS_NULL 的同义词。</span><span class="sxs-lookup"><span data-stu-id="0301a-222">You can set one or more null equivalents as synonyms to DQS_NULL.</span></span> <span data-ttu-id="0301a-223">这样，所有 Null 和 Null 等效值都将处理为 DQS_NULL。</span><span class="sxs-lookup"><span data-stu-id="0301a-223">When you do so, all nulls and null equivalents will be processed as DQS_NULL.</span></span>  
  
  