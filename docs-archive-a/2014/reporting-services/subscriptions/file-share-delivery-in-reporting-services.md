---
title: Reporting Services 中的文件共享传递 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
ms.assetid: 9f338dd3-f68a-4355-b9d7-9b25dacf3b5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9bba83a89612f8601adedd827edad0e587d096d8
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590558"
---
# <a name="file-share-delivery-in-reporting-services"></a>Reporting Services 中的文件共享传递
  SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含文件共享传递扩展插件，以便你可以将报表传递到文件夹。 默认情况下会提供文件共享传递扩展插件，并且不需要进行其他配置。 为了成功传递文件，必须设置对共享文件夹的写访问权限。 此外，需要访问报表的用户还必须对共享文件夹具有读取权限。  
  
 若要将报表分发到文件共享位置，需要定义标准订阅或数据驱动订阅。 一次只能订阅并请求传递一个报表。 若要了解如何在数据驱动订阅中使用文件共享传递，请参阅[创建数据驱动订阅（SSRS 教程）](../create-a-data-driven-subscription-ssrs-tutorial.md)。 此外，运行远程文件共享订阅的帐户需要本地登录 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 计算机的权限。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 本主题内容：  
  
-   [传递到共享文件夹的报表的特征](#bkmk_Characteristics)  
  
-   [目标文件夹](#bkmk_target_folders)  
  
-   [文件格式](#bkmk_file_formats)  
  
-   [文件选项](#bkmk_file_options)  
  
##  <a name="characteristics-of-a-report-that-is-delivered-to-a-shared-folder"></a><a name="bkmk_Characteristics"></a>传递到共享文件夹的报表的特征  
 与报表服务器承载和管理的报表不同，传递到共享文件夹的报表是静态的文件。 为报表定义的交互功能在作为文件存储到文件系统中的报表上不起作用。 交互功能将表示为静态元素。 例如，如果传递矩阵报表，结果文件只能显示报表的顶级视图；您不能通过展开行和列来查看支持数据。 如果报表中包含图表，则图表将使用默认的显示方式。 如果报表链接到其他报表，则链接呈现为静态文本。 若要在传递的报表中保留交互功能，请改用电子邮件传递。 有关详细信息，请参阅 [Reporting Services 中的电子邮件传递](e-mail-delivery-in-reporting-services.md)。  
  
##  <a name="target-folders"></a><a name="bkmk_target_folders"></a>目标文件夹  
 如果所定义的订阅使用文件共享传递，则必须指定现有文件夹作为目标文件夹。 报表服务器不会在文件系统上创建文件夹。 您指定的文件夹必须可通过网络连接进行访问。  
  
 验证将查看共享文件夹中报表的用户是否具有读取权限。  
  
 在订阅中指定目标文件夹时，请使用包含计算机网络名称的通用命名约定 (UNC) 格式。 不能在文件夹路径中包含尾随反斜杠。 下面是一个 UNC 路径的示例：  
  
```  
\\<servername>\reportarchive\operations\2003  
```  
  
 当您创建该文件夹时，请考虑所需的连接限制。 报表服务器需要两种连接，但是您必须包括足够的连接才能容纳其他要打开共享文件夹中的报表的用户。  
  
##  <a name="file-formats"></a><a name="bkmk_file_formats"></a> 文件格式  
 在呈现报表时可以使用多种文件格式，如 HTML 或 Excel。 若要按特定文件格式保存报表，请在创建订阅时选择相应的呈现格式。 例如，如果选择 **Excel** ，则会将报表保存为 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 格式。 虽然您可以选择任意支持的呈现格式，但对于不同的格式，呈现文件的优劣效果会有所不同。  
  
 对于文件共享传递，请选择以单一文件传递报表的格式，其中，所有图像和相关内容都包含在报表内。 适用的格式包括 Web 存档、PDF、TIFF 和 Excel。 请避免使用 HTML4.0。 如果报表中包括图像，则 HTML 4.0 格式不会将图像包括在文件中。  
  
##  <a name="file-options"></a><a name="bkmk_file_options"></a> 文件选项  
 创建订阅时，可以通过选择有关选项来确定文件名的创建方式，以及是否在以后用更新的版本替代它。 完全限定的文件名有三部分：名称、扩展名和文本/数字，将文本/数字追加到文件末尾可以创建唯一的文件名。 覆盖选项确定了是否在文件名末尾添加文本或数字。  
  
 文件名基于报表名称，但您可以在订阅中提供自定义名称。 扩展名是可选的，但如果指定它的话，报表服务器将创建对应于呈现格式的扩展名。  
  
 您可以指定覆盖选项对每个报表传递重复使用相同的文件名或者创建新文件。 若要覆盖文件，必须使用相同的文件名和扩展名。  
  
 为每个传递创建唯一的文件的另一种方法是在文件名中包含时间戳。 若要执行此操作，请将“”`@timestamp`变量添加到文件名中（例如，CompanySales@timestamp**）。 采用这种方法，文件名的定义是唯一的，因此永远不会被覆盖。  
  
## <a name="see-also"></a>另请参阅  
 [在纯模式下创建、修改和删除标准订阅 &#40;Reporting Services&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
