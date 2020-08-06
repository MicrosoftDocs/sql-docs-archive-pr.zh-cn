---
title: 使用浏览器中的“打印”控件打印报表（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8dbd4243320dd8d36dafc27ea910755fd3e70a83
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579528"
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>使用打印控件从浏览器中打印报表（报表生成器和 SSRS）
  虽然浏览器是用于查看报表的最常见的客户端应用程序，但是浏览器的打印功能并不是打印报表的理想选择。 浏览器的打印功能是针对打印网页而设计的。 通常，从浏览器打印的页面包括网页上的所有可见元素，以及标识网页或网站的页眉和页脚信息。 从浏览器打印将会打印当前窗口的内容。 对于多页报表，浏览器最多打印第一页，而且如果报表页超出了打印页的尺寸，打印的内容可能还会减少。  
  
 若要改善您在浏览器中查看的报表打印质量，以及打印多页报表，您可以使用中提供的客户端打印功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。 客户端打印功能提供了一个标准 **“打印”** 对话框，可用来选择打印机，指定页面范围和边距，以及在打印前预览报表。 客户端打印功能旨在替代浏览器 **“文件”** 菜单上的 **“打印”** 命令。 使用客户端打印功能时，报表的打印效果与其设计样式相同，只是不包含在网页打印输出中看到的额外元素。  
  
 要使用客户端打印，需安装 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 控件。 有关详细信息，请参阅 [启用和禁用 Reporting Services 的客户端打印](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>打印选项  
 若要配置报表的打印属性，请在 **“打印”** 对话框中，单击 **“属性”** 按钮。 **“纸张大小”** 取决于在报表定义中定义的报表页大小的默认高度和宽度。 根据打印机类型及其功能的不同，可用的值会有所不同。 宽度和高度显示的默认值取决于计算机上配置的打印驱动程序。 更改这些值后，报表将使用新的尺寸进行打印。 页宽和页高都由 **“方向”**（设置为 **“纵向”** 或 **“横向”**）确定。 默认的显示方向取决于报表的页宽和页高。  
  
> [!NOTE]  
>  **“打印”** 对话框和宽度、高度及页面方向的默认打印机设置都由报表定义确定。  
  
### <a name="print-preview"></a>打印预览  
 若要预览报表，请在 **“打印”** 对话框中，单击 **“预览”** 按钮。 单击“预览”将在单独的预览窗口中打开报表的首页。 如果报表已呈现在报表服务器上，则可以预览其他页。 预览的报表以 EMF 格式呈现。 在到达最后一页（此时会禁用 **“下一页”** 按钮）之前，您可以导航到上一页或下一页。  
  
### <a name="adjusting-print-margins"></a>调整打印边距  
 您可以在打印报表之前，修改所呈现的 EMF 报表的打印边距。 为此，请在 **“打印”** 对话框中，单击 **“预览”** 按钮。 在预览页的顶部，单击 **“边距”** 按钮。 此时，将显示“边距”对话框。 根据需要，配置上、下、左、右边距。 [!INCLUDE[clickOK](../../includes/clickok-md.md)] 此时，该对话框将关闭，并且修改后的设置会存储下来，以用于呈现预览和打印。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;报表生成器和 SSRS 打印报表&#41;](print-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](print-a-report-report-builder-and-ssrs.md)  
  
  
