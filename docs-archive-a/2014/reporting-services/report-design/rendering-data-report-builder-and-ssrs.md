---
title: 呈现数据（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a458fdf9-fb2a-4fee-9fbd-b38f36e91753
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc2757d308529c8b5a03e206a827fce7028edbfb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691607"
---
# <a name="rendering-data-report-builder-and-ssrs"></a>呈现数据（报表生成器和 SSRS）
  使用 HTML、MHTML、Word、Excel、PDF 或 Image 之类的布局呈现器时，数据和其组织保持不变。 当使用逗号分隔值 (CSV) 或 XML 之类的数据呈现器格式导出时，不会呈现任何可视布局元素。 呈现报表时，CSV 和 XML 会将某些规则应用到表体及其内容。 这些规则用于确定数据在这些格式中的呈现方式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 可以使用数据呈现器执行以下操作：  
  
-   导入到数据库。 CSV 是一种可由包括 SQL Server 和 Microsoft Access 在内的许多数据库应用程序轻松导入的常用格式。  
  
-   导入到 Excel。 使用 CSV 呈现器可将数据导出为不带可视布局的 Excel 格式。 数据导出为 Excel 后，便可以使用标准的 Excel 工具，例如图表、公式和透视表。  
  
-   XSLT 转换。 可将 XSLT 应用到 XML 呈现器的输出。 这种服务器端转换是一种可将数据转换为几乎任何格式的有效方法。  
  
-   数据交换/EDI。 外部进程可以请求对报表进行 CSV 或 XML 呈现并使用这些数据。  
  
 控制数据呈现器格式的属性集不同于控制布局呈现器的属性集。 以下是 **“属性”** 窗格中仅适用于数据呈现器的属性集列表。  
  
-   DataElementOutput 属性用于控制在导出时数据中是否包含特定项。  
  
-   DataElementName 属性用于控制数据元素的名称。 在 CSV 中，这用于控制 CSV 列标题的名称。 在 XML 中，这将成为项的 XML 元素或属性的名称。  
  
-   DataElementStyle 属性用于控制在 XML 中是否将报表项呈现为元素或特性。  
  
 CSV 导出选项可将报表数据另存为不带任何格式的以逗号分隔的纯文本文件。 默认情况下，文件使用逗号 (,) 分隔各个字段和行，但可以使用设备信息设置配置此设置。 生成的文件可以用电子表格程序（如 Office SharePoint Server）打开，也可以用作其他程序的导入格式。 .csv 文件可在诸如记事本之类的文本编辑器中打开。 如果以 URL 形式进行访问，则 .csv 文件将返回 **text/csv**的 MIME 类型。 这种 .csv 文件为 MIME 1.0 版文件。 有关以 CSV 文件类型呈现报表的详细信息，请参阅[导出到 CSV 文件（报表生成器和 SSRS）](../report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)。  
  
 使用具有报表数据导出选项的 XML 文件可将报表另存为 XML 文件。 报表的 XML 架构特定于报表。 XML 导出选项不保存报表布局信息。 使用此选项生成的 XML 可以导入到数据库、用作 XML 数据消息或发送到自定义应用程序。 有关以 XML 文件类型呈现报表的详细信息，请参阅[导出到 XML（报表生成器和 SSRS）](../report-builder/exporting-to-xml-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 中的分页（报表生成器和 SSRS）](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [呈现行为（报表生成器和 SSRS）](rendering-behaviors-report-builder-and-ssrs.md)   
 [不同报表呈现扩展插件的交互功能（报表生成器和 SSRS）](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [呈现报表项（报表生成器和 SSRS）](rendering-report-items-report-builder-and-ssrs.md)   
 [列出 &#40;报表生成器和 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Reporting Services 设备信息设置](https://go.microsoft.com/fwlink/?LinkId=102515)  
  
  
