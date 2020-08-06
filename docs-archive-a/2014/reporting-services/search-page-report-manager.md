---
title: 搜索页 (报表管理器) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 51ffdc07-e1b9-4ed7-acb3-dd98d7cce273
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2528133f5b2ecc4bed4c16fdd476591b3bab52d2
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587187"
---
# <a name="search-page-report-manager"></a>“搜索”页（报表管理器）
  使用“搜索结果”页可以查看为报表、链接报表、报表模型、共享数据源、文件夹或资源指定的搜索操作的结果。 搜索结果按字母顺序列出。 您可以按照类型、名称或说明进行排序。  
  
 搜索操作中不包含下列各项：报表历史记录中包含的报表快照、订阅和共享计划。 同样，如果查看文件夹或报表时不具有足够的权限，则无法在搜索中包含相关项。  
  
 您不能在报表或模型中搜索文本。 若要在报表中搜索特定文本，请使用报表顶部的工具栏。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-search-results-page"></a>打开“搜索结果”页  
  
1.  打开报表管理器。  
  
2.  在页面顶部的 **“搜索”** 框中键入搜索条件。 然后按 Enter 或单击“搜索”箭头。  
  
## <a name="options"></a>选项  
 **删除**  
 单击此选项可从报表服务器数据库中删除项。  
  
> [!NOTE]  
>  此按钮仅在 **“详细信息视图”** 中可用。 然而，您可以将鼠标悬停在某个项之上，然后使用菜单来访问 **“详细信息视图”** 或 **“列表视图”** 中的删除功能。  
  
 **移动**  
 单击此选项可重定位项。 这将打开“移动项”页，在此页上可选择其他文件夹位置。  
  
> [!NOTE]  
>  此按钮仅在 **“详细信息视图”** 中可用。 然而，您可以将鼠标悬停在某个项之上，然后使用菜单来访问 **“详细信息视图”** 或 **“列表视图”** 中的移动功能。  
  
 搜索框  
 键入希望查找的项的全名或部分名称，再单击 **“转到”** 以启动搜索。 可以搜索的字符串最长为 128 个字符。  
  
 搜索结果将列出在文本值中任意位置包含整个搜索字符串的项名称或说明。  
  
 不支持布尔运算符，例如加号字符 (+)。  
  
 **详细信息视图**  
 单击以在一个列表中显示“搜索结果”页，其中包含有关各项的附加信息，如项类型、名称、说明、项所在的文件夹以及上次运行该项的时间。 在 **“详细信息视图”** 中，可以使用 **“删除”** 和 **“移动”** 按钮删除和重新定位文件夹中的项。  
  
 悬停在某个项之上，单击下拉箭头以打开下拉菜单，从中可以访问和配置所选项的属性。  
  
 **列表视图**  
 单击以显示“搜索结果”页，但没有 **“详细信息视图”** 中的详细信息。 当打开“搜索结果”页时，列表视图是默认视图。  
  
 悬停在某个项之上，单击下拉箭头以打开下拉菜单，从中可以访问和配置所选项的属性。  
  
## <a name="see-also"></a>另请参阅  
 [报表管理器（SSRS 本机模式）](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
