---
title: 打开知识库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.openkb.f1
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f727a5ab75a60d29c830403892c56c87fc6d4ebf
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691874"
---
# <a name="open-a-knowledge-base"></a>打开知识库
  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中打开现有的知识库，以及如何准备知识库以用于域管理、知识发现或添加匹配策略。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 若要打开知识库，该知识库必须已创建，并且已发布（如果另一个人创建了此知识库）或已关闭（如果您创建了该知识库）。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能打开知识库。  
  
##  <a name="open-a-knowledge-base"></a><a name="Open"></a>打开知识库  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开知识库”**。  
  
3.  在表中选择知识库。 将在该页的右侧窗格中显示知识库中的域和匹配规则。  
  
    > [!NOTE]  
    >  可以通过在表中右键单击知识库对其执行操作。 您可以打开知识库、用其他名称保存它、对其解除锁定、放弃操作、重命名或显示其属性。  
  
4.  在 **“选择活动”** 中，选择要对知识库执行的活动：  
  
    -   选择 **“域管理”** 可进入您用来修改知识库中的域的屏幕。  
  
    -   选择 **“知识发现”** 可以进入一个向导，您可以使用该向导分析数据样本并用分析结果填充知识库的各个域。  
  
    -   选择 **“匹配策略”** 可以创建匹配策略，并将其添加到知识库。  
  
5.  单击 **“打开”** 。  
  
    > [!NOTE]  
    >  还可以通过右键单击知识库，然后单击“打开”来打开该知识库。 上下文菜单中的其他命令支持用其他名称保存它、对其解除锁定、放弃操作、重命名或显示其属性。  
  
    > [!NOTE]  
    >  如果您因为该知识库已锁定而无法打开，则请参阅下一节。  
  
## <a name="open-a-recent-knowledge-base"></a>打开最近的知识库  
 将在 DQS 主页的 **“最近的知识库”** 列表中显示 5 个最近打开的知识库。 这使您可以打开最近使用的知识库，而无需通过 **“打开知识库”** 页面。  
  
-   若要打开“最近”列表中没有锁定的知识库，请单击该知识库的右箭头，然后选择要在其中打开该知识库的活动。  
  
-   若要打开“最近”列表中已锁定的知识库，请单击该知识库，此时将在括号中标明的活动和页面中打开该知识库。  
  
-   若要打开“最近”列表中已被其他成员锁定的知识库，请联系相关人员，让他们解除对该知识库的锁定。  
  
##  <a name="follow-up-after-opening-a-knowledge-base"></a><a name="FollowUp"></a>跟进：打开知识库后  
 打开知识库之后，该知识库将进入在“知识库”表的“状态”列中指示的状态。 对于知识发现和匹配策略活动，将在特定向导页中打开该知识库。 对于域管理活动，将在域管理页面中打开知识库。 有关状态的详细信息，请参阅[执行知识发现](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理域](../../2014/data-quality-services/managing-a-domain.md)或[创建匹配策略](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="if-the-knowledge-base-is-locked"></a><a name="Locked"></a>如果知识库已锁定  
 第一列中的锁图标显示是否已锁定知识库。 锁定的知识库名称将以红色字体显示。 特定用户正在通过知识库活动修改的知识库将标记为锁定。 任何其他用户都不能对锁定的知识库执行操作。 对知识库执行操作的用户可以在“打开知识库”页上通过右键单击表中的知识库，然后单击 **“解锁”**，或通过发布该知识库，对其解除锁定。 当游标位于锁定的知识库上时，DQS 将显示提示，以显示锁定该知识库的人员以及何时锁定了此知识库。  
  
##  <a name="state-of-a-knowledge-base"></a><a name="State"></a>知识库的状态  
 “状态”字段指示知识库处于活动的哪个阶段。 如果您打开知识库，则打开此知识库的该阶段。  
  
-   **\<Empty>**：如果已通过在 "域管理" 活动中单击 "**发布**" 发布知识库，并单击 **"是-发布知识库并退出**"，则知识库的 "状态" 字段为空。  
  
-   **工作中**：通过在域管理活动中单击 "**发布**"，然后单击 "**否" 保存对知识库所做的工作并退出**。  
  
-   **域管理**：已为知识库中的域输入数据，但尚未发布该知识库，工作仍保留在域管理活动中。 知识发现活动不可用。 在 **“域管理”** 屏幕中单击 **“关闭”** 后出现此状态。  
  
-   **发现 - 映射**：在 **“知识库管理: 映射”** 页上关闭了知识库。 该知识库已锁定，且域管理活动和匹配活动不可用。  
  
-   **发现 - 发现**：在 **“知识库管理: 分析”** 页上关闭了知识库。 知识库已锁定，且域管理活动不可用。  
  
-   **发现-值管理**：在 "**知识库管理：管理域字词**" 页上关闭了知识库。 知识库已锁定，且域管理活动不可用。  
  
-   **匹配策略-匹配策略**：在 "**匹配策略-匹配策略**" 页上关闭了知识库。 该知识库已锁定，且知识发现和域管理活动不可用。  
  
-   **匹配策略-匹配结果**：在 "**匹配策略-匹配结果**" 页上关闭了知识库。 该知识库已锁定，且知识发现和域管理活动不可用。  
  
  
