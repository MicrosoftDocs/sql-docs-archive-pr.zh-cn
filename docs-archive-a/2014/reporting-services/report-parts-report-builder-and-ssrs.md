---
title: 报表部件（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10543"
ms.assetid: 957f664c-8a7a-4532-b5a6-5f859c5840bd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb709f33b208f5bef56cbd6bf5ebf72e735d9433
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690367"
---
# <a name="report-parts-report-builder-and-ssrs"></a>报表部件（报表生成器和 SSRS）
   表、矩阵、图表和图像等报表项可以作为“报表部件”发布。 报表部件是单独发布到报表服务器上并且可以在其他报表中重复使用的报表项。 报表部件具有 .rsc 文件扩展名。  
  
 通过报表部件，工作组现在可以充分利用其团队成员的不同特长和角色。 例如，如果您负责创建图表，则可以将您的图表保存为您和您的同事可以在其他报表中重复使用的单独的部件。 您可以将报表部件发布到报表服务器或者与报表服务器相集成的 SharePoint 站点上。 您可以在多个报表中重复使用这些报表部件，也可以在服务器上更新它们。  
  
 您添加到报表中的报表部件将按唯一 ID 维持与站点或服务器上报表部件实例的关系。 在您将报表部件从站点或服务器添加到报表后，可以对这些报表部件进行修改，而与站点或服务器上的原始报表部件无关。 您可以接受他人对站点或服务器上报表部件的更新，并且可以将修改后的报表部件保存回站点或服务器，以及添加新报表部件或改写原始报表部件（如果您具有足够的权限）。  
  
 若要快速开始使用报表部件，请参阅视频[报表生成器3报表部件 SQL Server 2008 R2](https://technet.microsoft.com/edge/Video/ff711300)和[如何实现：使用 SQL Server 报表生成器创建可重复使用的报表部件](https://technet.microsoft.com/sqlserver/ff634166.aspx)。  
  
##  <a name="life-cycle-of-a-report-part"></a><a name="ComponentWorkflow"></a> 报表部件的生命周期  
 ![rs_ComponentCreation](media/rs-componentcreation.gif "rs_ComponentCreation")  
  
1.  人员 A 创建一个含图表的报表，该图表依赖于某一嵌入数据集。  
  
2.  人员 A 选择将该图表发布到报表服务器。 报表生成器向已发布的图表分配一个唯一的 ID。 人员 A 未选择共享该数据集，因此数据集保持嵌入在图表中。  
  
3.  人员 B 创建一个空白报表，搜索报表部件库，查找图表，并将其添加到报表中。 该图表现在是人员 B 的报表部件，同时嵌入数据集也是报表部件。 人员 B 可以修改位于报表中的该图表和数据集的实例。 这将不会对报表服务器上图表和数据集的实例产生影响，并且不会破坏报表和报表服务器上实例之间的关系。  
  
     ![rs_componentupdate](media/rs-componentupdate.gif "rs_componentupdate")  
  
4.  人员 C 将图表添加到报表，并且将报表中的此图表从条形图更改为饼图。  
  
5.  人员 C 有权覆盖服务器上的图表并且这样做了，而且还将它重新发布到服务器。 这将更新服务器上图表的已发布副本。 人员 C 未选择共享该数据集，因此数据集保持嵌入在图表中。  
  
6.  人员 B 接受来自服务器的更新的图表。 这将覆盖人员 B 已对人员 B 的报表中的图表所做的更改。  

##  <a name="publishing-report-parts"></a><a name="PublishingComponents"></a>发布报表部件  
 在您发布报表部件时，报表生成器会向其分配一个不同于报表部件名称的唯一 ID。 报表生成器将保持该 ID，无论您对该报表部件进行何种更改。 该 ID 将您的报表中的原始报表项链接到该报表部件。 在其他报表作者重复使用该报表部件时，该 ID 也将其报表中的报表部件链接到报表服务器上的报表部件。  
  
 以下是您可以作为报表部件发布的报表项：  
  
-   图表  
  
-   仪表  
  
-   映像  
  
-   Maps  
  
-   参数  
  
-   矩形  
  
-   表  
  
-   矩阵  
  
-   列表  
  
 在您发布显示数据（例如表、矩阵或图表）的某一报表项时，该报表项所依赖的数据集将作为嵌入在其中的数据集与该报表项一起保存。 您还可以单独保存该数据集，作为您和他人可用作其他报表部件基础的共享数据集。 有关详细信息，请参阅 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)。  
  
 某些报表部件可以包含其他报表项。 例如，表可以包含图表，并且矩形可以包含矩阵和图表。 当您发布包含其他报表项的报表项时，它们将作为一个单位保存。 所保存的其他报表项将嵌入在容器报表部件中。 您不能单独更新它们，并且不能将容器中的项作为单独的报表部件保存。  
  
 有关发布报表部件的详细信息，请参阅 [发布和重新发布报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)。  
  
### <a name="modifying-report-part-metadata"></a>修改报表部件元数据  
 您可以使用默认设置将报表部件发布到默认位置，或者可以将各报表部件保存到不同的位置，并且修改元数据，例如标题和说明。  
  
 在您发布报表部件时最好为报表部件提供一个明确的名称和说明，以便在搜索时帮助用户识别它。 您最终可能会得到在您的站点或服务器上具有类似名称的许多报表部件。 请考虑使用命名约定来说明报表部件及其依赖项之间的关系。  
  
 此外，请考虑在同一个文件夹中保存共享数据源、共享数据集和依赖于它们的报表部件。  
  
 您还可以在“属性”窗格中编辑说明。  

##  <a name="reusing-report-parts"></a><a name="ReusingComponents"></a>重复使用报表部件  
 创建报表的最简单方式是从报表部件库将现有报表部件（如表或图表）添加到您的报表。 将报表部件添加到您的报表后，可以根据需要进行修改，或者接受来自服务器的更新。 更改您的报表中的报表项将不会对站点或服务器上发布的报表部件的实例产生影响，并且不会破坏报表中的实例与站点或服务器上的实例之间的关系 如果您具有足够的权限，则可以将更新的副本保存回站点或服务器。 如果其他人修改站点或服务器上的副本，您可以决定是将您的副本保持原样，还是更新该副本以便与站点或服务器上的副本相符。  
  
### <a name="searching-for-report-parts"></a>搜索报表部件  
 您可以在报表部件库中查找要添加到您的报表中的报表部件。 可以按照报表部件的全名或部分名称、创建者、最后修改者、最后修改时间、存储位置以及报表部件的类型，对报表部件进行筛选。 例如，您可以搜索由您的同事之一在上周创建的所有图表。  
  
 您可以采用缩略图或列表的形式查看搜索结果，并且可以按名称、创建日期和修改日期以及创建者对搜索结果进行排序。 有关详细信息，请参阅 [浏览查找报表部件和设置默认文件夹（报表生成器和 SSRS）](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)。  
  
### <a name="what-comes-with-a-report-part"></a>报表部件所附带的内容  
 将报表部件添加到报表时，还将添加它正常工作所需的所有内容。 例如，显示数据的任何对象依赖于一个数据集，即对某数据源的查询和连接。 它可能还具有一个或多个参数。 ** 它所依赖的所有项是其“依赖项”，并且在您将某一报表部件添加到报表时，所有这些依赖项或者指向它们的指针都将与该报表部件一起包括。 数据集和参数将在您的报表的“报表数据”窗格中列出。  
  
 报表部件的数据集可嵌入在报表部件中，或者可以是报表部件指向的单独的共享数据集。 如果该数据集嵌入在报表部件中，则可以对其进行修改。 如果该数据集是共享数据集，则它是您需要具有相应权限的单独对象。 有关共享数据集和嵌入数据集的详细信息，请参阅[将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。  
  
### <a name="resolving-naming-conflicts"></a>解决命名冲突  
 在您添加某一报表部件时，报表生成器会解决所有名称冲突。 例如，如果您在报表中已具有 Chart1，并且添加一个名为 Chart1 的报表部件，则报表生成器会自动将这个新报表部件重命名为 Chart2。 如果您在报表中已具有 Dataset1，并且添加一个报表部件，该报表部件引用也名为 Dataset1 的其他数据集，则报表生成器会自动将这个新数据集重命名为 Dataset2 并且更新引用。  
  
### <a name="adding-more-than-one-report-part"></a>添加多个报表部件  
 可以在报表中添加数目不限的报表部件。 但是，一次只能添加一个报表部件。 您甚至可以将一个报表部件的多个实例添加到同一个报表中。 它们将全都具有唯一名称，但将全都是服务器上同一报表部件的实例并具有相同的唯一 ID。  
  
 在您添加另一个报表部件时，如果该报表部件使用的数据集与您的报表中已存在的某一数据集完全相同，则向导不会将该数据集的其他版本添加到您的报表；它会重定向该报表部件中的引用以便转到现有数据集。 有关详细信息，请参阅 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)。  

##  <a name="updating-report-parts-with-changes-from-the-server"></a><a name="UpdatingComponents"></a> 通过来自服务器的更改更新报表部件  
 每次打开报表时，报表生成器都检查该报表中各报表部件的服务器实例是否已在服务器上进行了更新。 它还将检查报表部件的依赖项（如数据集和参数）的更改。 如果任何已发布的报表部件或其依赖关系已在服务器上进行了更新，则报表中的信息栏将显示已更新的数量。 您可以选择查看并接受或拒绝更新，或关闭信息栏。 如果您选择查看更新，则可以看到报表部件的缩略图、最后修改者以及最后修改时间。 然后，您可以接受任何或所有更新项。  
  
> [!NOTE]  
>  您可以禁用信息栏，这样，当更改报表部件时系统将不会通知您。 您可以在向报表中添加报表部件时设置此选项。 即使已禁用信息栏，也仍可以检查更新。 有关详细信息，请参阅[检查更新或关闭更新 &#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)。  
  
 报表生成器检查在服务器上最后一次更新报表部件的日期与您最后将报表部件与服务器同步的日期之间的差异。 它不检查您在报表中修改报表部件的日期。 因此，您的报表中的报表部件和服务器上的报表部件可能差别很大，但在报表生成器检查更新时，它将不会发现任何差异。  
  
### <a name="accepting-updates"></a>接受更新  
 在您接受针对报表部件的更新后，它将完全替代已在您的报表中的报表部件的副本。 您无法将报表中报表部件的功能与服务器上已发布报表部件的功能组合在一起。 但是，如果您已更改了报表部件的依赖项之一，例如嵌入的数据集，则报表生成器在复制时将不会覆盖已在您的报表中的依赖项。 它将下载依赖项的新副本，并且更新报表部件以便指向该新副本。  
  
### <a name="reverting-to-a-previous-version-of-a-report-part"></a>还原到报表部件的以前版本  
 如果您已在报表中更改了报表部件的某一版本，并且决定要用服务器上的版本替换该版本，则无法使用 **“更新”** 对话框执行此操作。 更新仅针对自您下载报表部件后在服务器上已更改的报表部件。  
  
 若要还原到服务器上的版本，只需删除在您的报表中具有的版本并且再次添加它。  

##  <a name="updating-report-parts-already-on-the-server"></a><a name="RepublishingComponents"></a> 更新已在服务器上的报表部件  
 您可以选择更新服务器上的现有报表部件，或者将其作为新的报表部件发布而不替换现有的报表部件。 在您更新服务器上的报表部件时，它并不自动修改该报表部件在其他报表中的副本。 如果其他报表作者已将该报表部件添加到某一报表，则在他们下次打开该报表时向他们通知所做的更改。 他们可以选择接受或拒绝您的更改。  
  
 如果您选择将该报表部件作为新的报表部件发布，则报表生成器将为其提供一个新的唯一 ID，并且它将不再链接到原始报表部件。  
  
 如果数据集嵌入在该报表部件中，则每次您发布该报表部件时，该数据集都将显示在 **“发布报表部件”** 对话框中。 共享数据集不显示在 **“发布报表部件”** 对话框中。  

##  <a name="working-with-report-parts-in-report-designer"></a><a name="RptPartsRptDesigner"></a> 在报表设计器中使用报表部件  
 报表部件的工作方式与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的报表设计器稍有不同。 在报表设计器中，发布是单向的：您可以从报表设计器发布报表部件，但不能在报表设计器中重复使用现有报表部件。 有关详细详细信息，请参阅[报表设计器中的报表部件 (SSRS)](report-design/report-parts-in-report-designer-ssrs.md)。  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a>操作指南主题  
 [发布和重新发布报表部件（报表生成器和 SSRS）](report-parts-report-builder-and-ssrs.md)  
  
 [浏览查找报表部件和设置默认文件夹（报表生成器和 SSRS）](report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
 [检查更新或关闭更新 &#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另请参阅  
 [报表生成器中的报表部件和数据集](report-data/report-parts-and-datasets-in-report-builder.md)   
 [&#40;报表生成器和 SSRS 的报表部件疑难解答&#41;](../../2014/reporting-services/troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [管理报表部件](report-design/managing-report-parts.md)   
 [SQL Server 2008 R2 () 视频中报表生成器3个报表部件](https://technet.microsoft.com/edge/Video/ff711300)   
 [如何实现：使用 SQL Server 报表生成器创建可重复使用的报表部件（视频）](https://technet.microsoft.com/sqlserver/ff634166.aspx)  
  
  
