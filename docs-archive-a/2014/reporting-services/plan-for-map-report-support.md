---
title: 规划地图报表支持 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f3d1e1774e44ae879b8c01e66289cefd4d42ee1c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692778"
---
# <a name="plan-for-map-report-support"></a>计划地图报表支持
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]支持使用空间数据源的地图报表。 空间数据可来自 SQL Server 数据库或 ESRI 形状文件，或者来自随 Reporting Services 或报表生成器一起安装的地图库。 地图还可以显示 Bing 地图图块的背景。 报表作者可以创建一个报表，该报表可以将空间数据或 Bing 地图图块指定为动态的和在运行时检索的，也可以指定为静态的和嵌入在报表定义中的。  
  
## <a name="support-for-bing-maps"></a>支持 Bing 地图  
 地图可以包括显示 Bing 地图图块的背景层。 若要查看具有地图图块层的已发布报表，报表服务器必须配置为从 Bing 地图 Web 服务检索图块。 有关详细信息，请参阅 [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)。  
  
 在各报表中，报表作者可以指定是否使用安全套接字层 (SSL) 连接从图块服务器中检索图块。 为此，必须在图块层的属性窗格中将布尔属性 UseSecureConnection 设置为 `true` 。  
  
> [!NOTE]  
>  有关在报表中使用 Bing 地图图块的详细信息，请参阅 [其他使用条款](https://go.microsoft.com/fwlink/?LinkId=151371) 和 [隐私声明](https://go.microsoft.com/fwlink/?LinkId=151372)。  
  
## <a name="report-design-recommendations"></a>报表设计建议  
 地图报表的优秀报表设计要求报表作者在静态和动态空间数据之间权衡利弊，找出满足报表用户需要的平衡点。 嵌入的地图元素可能会显著增加报表定义的大小，但会减少查看地图报表所需的时间。 动态地图元素会减少报表定义大小，但会增加处理和查看地图所需的时间。 报表作者必须在这些对立的问题之间找到恰当的平衡点。  
  
 在报表定义大小是问题所在时，作为报表服务器管理员，您可以鼓励报表设计者减少报表定义中的空间数据量。  
  
 在以下情况下，地图元素嵌入在报表定义中：  
  
-   在创建报表时，空间数据源位于本地文件系统上。 这包括来自已在本地安装的地图库或 ESRI 形状文件的空间数据。 默认情况下，地图向导和地图层向导嵌入来自本地文件系统上的数据源的空间数据。  
  
-   报表作者选择该选项可以手动在报表中嵌入空间数据。  
  
 为了有助于减少具有地图的报表定义的大小，报表作者可以使用以下选项中的一个或多个：  
  
-   从报表设计器的中 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ，将 ESRI 形状文件的空间数据源添加到 Report Server 项目。 在您部署该项目时，这些 ESRI 形状文件将发布到报表服务器以及报表上。 在报表作者运行地图向导时，他们可以从 Report Server 项目指定空间数据源，并且地图元素默认情况下不嵌入在报表定义中。  
  
-   从报表生成器中，通过从 Report Server 中选择 "形状文件" 来添加 ESRI 形状文件的空间数据源。 在报表作者运行地图向导时，他们可以从报表服务器中浏览并选择一个空间数据源，并且地图元素默认情况下不嵌入在报表定义中。  
  
-   在地图数据必须嵌入地图数据时，调整视区中心和缩放级别以便只包括报表所需的地图数据。  
  
 有关详细信息，请[&#40;报表生成器和 SSRS&#41;的映射](report-design/maps-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [报表故障排除：地图报表（报表生成器和 SSRS）](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
