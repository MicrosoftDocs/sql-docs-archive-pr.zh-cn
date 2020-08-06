---
title: 钻取、深化、子报表和嵌套数据区域 (报表生成器和 SSRS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4791a157-b028-4698-905d-f1dd0887aa0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6c6923d012f6f3deef094e5d8ca3d4b21627f6b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691618"
---
# <a name="drillthrough-drilldown-subreports-and-nested-data-regions-report-builder-and-ssrs"></a>钻取、深化、子报表和嵌套数据区域（报表生成器和 SSRS）
  可以通过多种方法组织数据，以显示一般信息与详细信息之间的关系。  您可以将所有数据都放在报表中，但将这些数据设置为在用户单击以显示详细信息之前处于隐藏状态，这就是“深化”  操作。 可以在“嵌套”  在其他数据区域（例如表或矩阵）内的一个数据区域（例如表或图表）内显示数据。 还可以在完全包含在主报表内的“子报表”  中显示数据。 或者，可以将详细信息数据放在“钻取”  报表中，钻取报表是在用户单击链接时显示的单独报表。  
  
 ![rs_DrillThruDrilldownEtc](../media/rs-drillthrudrilldownetc.gif "rs_DrillThruDrilldownEtc")  
  
 A. 钻取报表  
  
 B. 子报表  
  
 C. 嵌套的数据区域  
  
 D. 深化操作  
  
 上述所有数据组织方式具有共性，但它们用于不同的目的，并且具有不同的功能。 其中两种方式（即钻取报表和子报表）实际上是单独的报表。 嵌套就是将一个数据区域放到另一个数据区域中。 深化是一种可应用于任何报表项的操作，其目的是隐藏和显示其他报表项。 它们都是组织和显示数据的方式，可以帮助用户更好地了解报表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="summary-of-characteristics"></a><a name="SummaryCharacteristics"></a> 特征摘要  
 下表汇总了各种不同的特征。 详细信息将在本主题后面的单独章节中提供。 由于您可以将深化的显示和隐藏操作应用于任何报表项，因此我们未在比较范围内包括深化。  
  
|特征|子报表|钻取|嵌套|  
|-----------|---------------|------------------|------------|  
|使用主报表的数据集|相同或不同|相同或不同|相同|  
|检索数据|与主报表同时检索数据|通过一个钻取报表一次性检索数据|始终与主报表同时检索数据|  
|处理和呈现方式|与主报表一起|单击链接时|与主报表一起。|  
|执行速度|较慢（但与主报表一起检索所有数据）|较快（但不与主报表一起检索所有数据）|较快（且与主报表一起检索所有数据）|  
|是否使用参数|是|是|否|  
|可以重复使用|作为其他报表中的报表、子报表或钻取报表|作为其他报表中的报表、子报表或钻取报表|不能重复使用。|  
|位置|位于主报表外部，与主报表位于相同或不同的报表服务器|位于主报表外部，与主报表位于相同的报表服务器|位于主报表内部|  
|显示位置|主报表中|其他报表中|主报表中|  
  

  
##  <a name="details-of-characteristics"></a><a name="Details"></a> 特征的详细信息  
  
###  <a name="datasets-they-use"></a><a name="Datasets"></a> 它们使用的数据集  
 子报表和钻取报表可以使用主报表中的同一数据集，也可以使用不同的数据集。 嵌套数据区域使用同一数据集。  
  
###  <a name="retrieving-data"></a><a name="RetrieveData"></a> 检索数据  
 子报表和嵌套数据区域与主报表同时检索数据。 钻取报表不与主报表同时检索数据。 每个钻取报表都会在用户单击其对应的链接时检索数据。 在必须同时检索主报表和从属报表的数据时，这一点非常重要。  
  
###  <a name="processing-and-rendering"></a><a name="ProcessRender"></a> 处理和呈现  
 子报表作为主报表的一部分进行处理。 例如，如果一个显示订单详细信息的子报表添加到详细信息行的一个表单元中，则该子报表只按该表的每行处理一次，并呈现为主报表的一部分。 钻取报表仅在用户单击汇总主报表中的钻取链接时才进行处理和呈现。  
  
###  <a name="performance"></a><a name="Performance"></a> 性能  
 在确定使用哪种数据组织方式时，请考虑使用数据区域而不是子报表，尤其是在多个报表都不使用子报表的情况下。 由于报表服务器将子报表的每个实例作为独立的报表来处理，因此性能可能会受到影响。 数据区域的功能和灵活性与子报表相差无几，但性能更佳。 钻取报表的性能也优于子报表，因为它们不与主报表同时检索所有数据。  
  
###  <a name="use-of-parameters"></a><a name="Parameters"></a> 是否使用参数  
 钻取报表和子报表通常包含用于指定要显示的报表数据的报表参数。 例如，当单击主报表中的销售订单号时，将打开一个钻取报表，该报表接受销售订单号作为参数，然后显示该销售订单的所有数据。 在主报表中创建链接时，您应指定要作为参数传递到钻取报表的值。  
  
 若要创建钻取报表或子报表，必须首先设计目标钻取报表或子报表，然后创建钻取操作或添加对主报表的引用。  
  
###  <a name="reusability"></a><a name="Reusability"></a> 可重用性  
 子报表和钻取报表是单独的报表。 因此，它们既可以用于一些报表中，也可以显示为单独的报表。 嵌套数据区域不具有可重用性。 由于它们嵌套在数据区域中，因此不能另存为报表部件。 可以将包含嵌套数据区域的数据区域另存为报表部件，但不能将嵌套数据区域本身另存为报表部件。  
  
###  <a name="location"></a><a name="Location"></a> 位置  
 子报表和钻取报表均为单独的报表，因此它们存储在主报表外部。 子报表既可与主报表位于同一报表服务器上，也可在不同的报表服务器上，但钻取报表必须与主报表位于同一报表服务器上。 嵌套数据区域是主报表的一部分。  
  
###  <a name="display"></a><a name="Display"></a> 显示位置  
 子报表和嵌套数据区域显示在主报表中。 钻取报表单独显示。  
  

  
##  <a name="in-this-section"></a><a name="InThisSection"></a> 本节内容  
 [钻取报表（报表生成器和 SSRS）](drillthrough-reports-report-builder-and-ssrs.md)  
 介绍在用户单击主报表中的链接时打开的报表。  
  
 [子报表（报表生成器和 SSRS）](subreports-report-builder-and-ssrs.md)  
 介绍在主报表的表体中显示的报表。  
  
 [嵌套数据区域（报表生成器和 SSRS）](nested-data-regions-report-builder-and-ssrs.md)  
 介绍在一个数据区域中嵌套另一个数据区域，如在矩阵中嵌套图表。  
  
 [深化操作（报表生成器和 SSRS）](drilldown-action-report-builder-and-ssrs.md)  
 介绍使用深化操作来隐藏和显示报表项。  
  
 [指定外部项的路径（报表生成器和 SSRS）](specifying-paths-to-external-items-report-builder-and-ssrs.md)  
 介绍如何引用报表定义文件外部的项。  
  
## <a name="see-also"></a>另请参阅  
 [报表参数（报表生成器和报表设计器）](report-parameters-report-builder-and-report-designer.md)  
  
  
