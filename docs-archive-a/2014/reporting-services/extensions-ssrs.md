---
title: 扩展
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 68e81b3554ed3a77e950d5da2a25cc0510322f77
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581145"
---
# <a name="extensions-for-sql-server-reporting-services-ssrs"></a><span data-ttu-id="cfa7c-102">用于 SQL Server Reporting Services 的扩展 (SSRS)</span><span class="sxs-lookup"><span data-stu-id="cfa7c-102">Extensions for SQL Server Reporting Services (SSRS)</span></span>

  <span data-ttu-id="cfa7c-103">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的报表服务器使用扩展插件来模块化其为身份验证、数据处理、报表呈现和报表传递接受的输入或输出的类型。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-103">The report server in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] uses extensions to modularize the types of input or output it accepts for authentication, data processing, report rendering, and report delivery.</span></span> <span data-ttu-id="cfa7c-104">这便于现有 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装利用行业中的新的软件标准，例如新的身份验证架构或自定义数据源类型。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-104">This makes it easy for existing [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] installations to utilize new software standards in the industry, such as a new authentication scheme, or a custom data source type.</span></span> <span data-ttu-id="cfa7c-105">报表服务器支持自定义的身份验证扩展插件、数据处理扩展插件、报表处理扩展插件、呈现扩展插件和传递扩展插件，并且支持在 RSReportServer.config 配置文件中向用户提供的可配置的扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-105">The report server supports custom authentication extensions, data processing extensions, report processing extensions, rendering extensions, and delivery extensions, and the extensions that are available to the users are configurable in the RSReportServer.config configuration file.</span></span> <span data-ttu-id="cfa7c-106">例如，您可以限制报表查看器允许使用的导出格式。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-106">For example, you can limit the export formats the report viewer is allowed to use.</span></span> <span data-ttu-id="cfa7c-107">报表服务器至少分别需要一个身份验证扩展插件、数据处理扩展插件和呈现扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-107">A report server requires at least one authentication extension, data processing extension, and rendering extension.</span></span> <span data-ttu-id="cfa7c-108">传递扩展插件和报表处理扩展插件是可选的，但如果希望支持报表分发或自定义控件，则是必需的。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-108">Delivery and report processing extensions are optional, but necessary if you want to support report distribution or custom controls.</span></span>  
  
 <span data-ttu-id="cfa7c-109">本主题介绍在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中可方便地使用的扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-109">This topic describes the extensions that are readily available in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].</span></span>  
  
## <a name="security-extensions"></a><span data-ttu-id="cfa7c-110">安全扩展插件</span><span class="sxs-lookup"><span data-stu-id="cfa7c-110">Security Extensions</span></span>

 <span data-ttu-id="cfa7c-111">安全扩展插件用于对用户和组进行身份验证和授权，以便其能够访问报表服务器。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-111">Security extensions are used to authenticate and authorize users and groups to a report server.</span></span> <span data-ttu-id="cfa7c-112">默认的安全扩展插件是基于 Windows 身份验证的。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-112">The default security extension is based on Windows Authentication.</span></span> <span data-ttu-id="cfa7c-113">如果您的部署模型需要其他身份验证方法（例如，如果您的 Internet 或 Extranet 部署需要基于窗体的身份验证），则您还可以创建自定义安全扩展插件来替换默认的安全扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-113">You can also create a custom security extension to replace default security if your deployment model requires a different authentication approach (for example, if you require forms-based authentication for Internet or extranet deployment).</span></span> <span data-ttu-id="cfa7c-114">单个 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安装中只能使用一个安全扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-114">Only one security extension can be used in a single [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] installation.</span></span> <span data-ttu-id="cfa7c-115">您可以替换默认的 Windows 身份验证安全扩展插件，但不能将它与自定义安全扩展插件一起使用。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-115">You can replace the default Windows Authentication security extension, but you cannot use it alongside a custom security extension.</span></span>  
  
## <a name="data-processing-extensions"></a><span data-ttu-id="cfa7c-116">数据处理扩展插件</span><span class="sxs-lookup"><span data-stu-id="cfa7c-116">Data Processing Extensions</span></span>

 <span data-ttu-id="cfa7c-117">数据处理扩展插件用于查询数据源和返回平展行集。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-117">Data Processing extensions are used to query a data source and return a flattened row set.</span></span> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] <span data-ttu-id="cfa7c-118">使用不同的扩展插件与不同类型的数据源交互。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-118">uses different extensions to interact with different types of data sources.</span></span> <span data-ttu-id="cfa7c-119">您可以使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]随附的扩展插件，也可以开发自己的扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-119">You can use the extensions that are included in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], or you can develop your own extensions.</span></span> <span data-ttu-id="cfa7c-120">提供用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)]、Hyperion Essbase、Teradata、OLE DB 和 ODBC 数据源的数据处理扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-120">Data processing extensions for [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)], Hyperion Essbase, Teradata, OLE DB, and ODBC data sources are provided.</span></span> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] <span data-ttu-id="cfa7c-121">还可以使用任何 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 数据访问接口。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-121">can also use any [!INCLUDE[vstecado](../includes/vstecado-md.md)] data provider.</span></span> <span data-ttu-id="cfa7c-122">数据处理扩展插件通过执行以下任务来处理来自报表处理器组件的查询请求：</span><span class="sxs-lookup"><span data-stu-id="cfa7c-122">Data processing extensions process query requests from the Report Processor component by performing the following tasks:</span></span>  
  
- <span data-ttu-id="cfa7c-123">打开与数据源之间的连接。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-123">Open a connection to a data source.</span></span>  
  
- <span data-ttu-id="cfa7c-124">分析查询，并返回字段名称列表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-124">Analyze a query and return a list of field names.</span></span>  
  
- <span data-ttu-id="cfa7c-125">对数据源运行查询，并返回行集。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-125">Run a query against the data source and return a rowset.</span></span>  
  
- <span data-ttu-id="cfa7c-126">如果需要，还会向查询传递参数。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-126">Pass parameters to a query, if required.</span></span>  
  
- <span data-ttu-id="cfa7c-127">遍历返回的行集，并检索数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-127">Iterate through the rowset and retrieve data.</span></span>  
  
<span data-ttu-id="cfa7c-128">某些扩展插件还可以执行以下任务：</span><span class="sxs-lookup"><span data-stu-id="cfa7c-128">Some extensions can also perform the following tasks:</span></span>  
  
- <span data-ttu-id="cfa7c-129">分析某一查询，并返回该查询中所使用的参数名称的列表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-129">Analyze a query and return a list of parameter names used in the query.</span></span>  
  
- <span data-ttu-id="cfa7c-130">分析查询，并返回分组所使用的字段的列表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-130">Analyze a query and return the list of fields used for grouping.</span></span>  
  
- <span data-ttu-id="cfa7c-131">分析查询，并返回排序所使用的字段的列表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-131">Analyze a query and return the list of fields used for sorting.</span></span>  
  
- <span data-ttu-id="cfa7c-132">提供用户名和密码以连接到数据源。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-132">Provide a user name and password to connect to the data source.</span></span>  
  
- <span data-ttu-id="cfa7c-133">向查询传递具有多个值的参数。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-133">Pass parameters with multiple values to a query.</span></span>  
  
- <span data-ttu-id="cfa7c-134">循环访问行并检索辅助元数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-134">Iterate through rows and retrieve auxiliary metadata.</span></span>  
  
## <a name="rendering-extensions"></a><span data-ttu-id="cfa7c-135">呈现扩展插件</span><span class="sxs-lookup"><span data-stu-id="cfa7c-135">Rendering Extensions</span></span>

 <span data-ttu-id="cfa7c-136">呈现扩展插件将来自报表处理器的数据和布局信息转换为设备特定的格式。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-136">Rendering extensions transform data and layout information from the Report Processor into a device-specific format.</span></span> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] <span data-ttu-id="cfa7c-137">包括七种呈现扩展插件：HTML、Excel、CSV、XML、Image、PDF 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-137">includes seven rendering extensions: HTML, Excel, CSV, XML, Image, PDF, and [!INCLUDE[msCoName](../includes/msconame-md.md)] Word.</span></span>  
  
- <span data-ttu-id="cfa7c-138">**HTML 呈现扩展插件** 通过 Web 浏览器向报表服务器请求报表时，报表服务器将使用 HTML 呈现扩展插件来呈现报表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-138">**HTML Rendering Extension** When you request a report from a report server through a Web browser, the report server uses the HTML rendering extension to render the report.</span></span> <span data-ttu-id="cfa7c-139">HTML 呈现扩展插件使用 UTF-8 编码生成所有的 HTML。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-139">The HTML rendering extension generates all HTML using UTF-8 encoding.</span></span> <span data-ttu-id="cfa7c-140">有关详细信息，请参阅 &#40;[报表生成器和 SSRS 的呈现&#41;](report-builder/rendering-to-html-report-builder-and-ssrs.md)和[规划 Reporting Services 和 Power View &#40;Reporting Services&#41;的浏览器2014支持](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-140">For more information, see [Rendering to HTML &#40;Report Builder and SSRS&#41;](report-builder/rendering-to-html-report-builder-and-ssrs.md) and [Planning for Reporting Services and Power View Browser Support &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).</span></span>  
  
- <span data-ttu-id="cfa7c-141">**Excel 呈现扩展插件** Excel 呈现扩展插件呈现可在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 或更高版本中查看和修改的报表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-141">**Excel Rendering Extension** The Excel rendering extension renders reports that can be viewed and modified in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 or later.</span></span> <span data-ttu-id="cfa7c-142">此呈现扩展插件会创建二进制交换文件格式 (BIFF) 的文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-142">This rendering extension creates files in Binary Interchange File Format (BIFF).</span></span> <span data-ttu-id="cfa7c-143">BIFF 是 Excel 数据的本机文件格式。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-143">BIFF is the native file format for Excel data.</span></span> <span data-ttu-id="cfa7c-144">在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 中呈现的报表支持适用于任何电子表格的所有功能。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-144">Reports that are rendered in [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] support all of the features available for any spreadsheet.</span></span> <span data-ttu-id="cfa7c-145">有关详细信息，请参阅 [导出到 Microsoft Excel（报表生成器和 SSRS）](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-145">For more information, see [Exporting to Microsoft Excel &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).</span></span>  
  
- <span data-ttu-id="cfa7c-146">**CSV 呈现扩展插件** 逗号分隔值 (CSV) 呈现扩展插件通过不带任何格式的以逗号分隔的纯文本文件形式呈现报表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-146">**CSV Rendering Extension** The Comma-Separated Value (CSV) rendering extension renders reports in comma-delimited plain text files, without any formatting.</span></span> <span data-ttu-id="cfa7c-147">用户随后可使用电子表格应用程序（如 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]）或任何其他可读取文本文件的程序打开这些文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-147">Users can then open these files with a spreadsheet application, such as [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)], or any other program that reads text files.</span></span> <span data-ttu-id="cfa7c-148">有关详细信息，请参阅 [导出到 CSV 文件（报表生成器和 SSRS）](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-148">For more information, see [Exporting to a CSV File &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).</span></span>  
  
- <span data-ttu-id="cfa7c-149">**XML 呈现扩展插件** XML 呈现扩展插件以 XML 文件形式呈现报表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-149">**XML Rendering Extension** The XML rendering extension renders reports in XML files.</span></span> <span data-ttu-id="cfa7c-150">随后可通过其他程序存储或读取这些 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-150">These XML files can then be stored or read by other programs.</span></span> <span data-ttu-id="cfa7c-151">您还可以使用 XSLT 转换将报表转换为另一种 XML 架构，供其他应用程序使用。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-151">You can also use an XSLT transformation to turn the report into another XML schema for use by another application.</span></span> <span data-ttu-id="cfa7c-152">XML 呈现扩展插件生成的 XML 文件是 UTF-8 编码文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-152">The XML generated by the XML rendering extension is UTF-8 encoded.</span></span> <span data-ttu-id="cfa7c-153">有关详细信息，请参阅 [导出到 XML（报表生成器和 SSRS）](report-builder/exporting-to-xml-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-153">For more information, see [Exporting to XML &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-xml-report-builder-and-ssrs.md).</span></span>  
  
-   <span data-ttu-id="cfa7c-154">**图像呈现扩展插件** 图像呈现扩展插件会将报表呈现为位图或图元文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-154">**Image Rendering Extension** The Image rendering extension renders reports to bitmaps or metafiles.</span></span> <span data-ttu-id="cfa7c-155">该扩展插件可使用以下格式呈现报表：BMP、EMF、GIF、JPEG、PNG、TIFF 和 WMF。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-155">The extension can render reports in the following formats: BMP, EMF, GIF, JPEG, PNG, TIFF, and WMF.</span></span> <span data-ttu-id="cfa7c-156">默认情况下，将使用 TIFF 格式呈现图像，这种格式的图像可以通过您的操作系统的默认图像查看器（例如，Windows 图片和传真查看器）进行显示。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-156">By default, the image is rendered in TIFF format, which can be displayed with the default image viewer of your operating system (for example, Windows Picture and Fax Viewer).</span></span> <span data-ttu-id="cfa7c-157">您可以从查看器中将图像发送到打印机。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-157">You can send the image to a printer from the viewer.</span></span> <span data-ttu-id="cfa7c-158">使用图像呈现扩展插件呈现报表可确保报表在每个客户端上的显示都相同。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-158">Using the Image rendering extension to render reports ensures that the report looks the same on every client.</span></span> <span data-ttu-id="cfa7c-159">（用户查看 HTML 格式的报表时，该报表的外观会因用户浏览器的版本、用户浏览器设置以及可用字体而异。）图像呈现扩展插件在服务器上呈现报表，因此所有用户看到的都是相同的图像。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-159">(When a user views a report in HTML, the appearance of that report can vary depending on the version of the user's browser, the user's browser settings, and the fonts that are available.) The Image rendering extension renders the report on the server, so all users see the same image.</span></span> <span data-ttu-id="cfa7c-160">由于是在服务器上呈现报表，因此服务器上必须安装了报表中使用的所有字体。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-160">Because the report is rendered on the server, all fonts that are used in the report must be installed on the server.</span></span> <span data-ttu-id="cfa7c-161">有关详细信息，请参阅 [导出到图像文件（报表生成器和 SSRS）](report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-161">For more information, see [Exporting to an Image File &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md).</span></span>  
  
- <span data-ttu-id="cfa7c-162">**PDF 呈现扩展插件** PDF 呈现扩展插件以 PDF 文件形式呈现报表，可以使用 Adobe Acrobat 6.0 或更高版本打开和查看这些文件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-162">**PDF Rendering Extension** The PDF rendering extension renders reports in PDF files that can be opened and viewed with Adobe Acrobat 6.0 or later.</span></span> <span data-ttu-id="cfa7c-163">有关详细信息，请参阅 [导出到 PDF 文件（报表生成器和 SSRS）](report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-163">For more information, see [Exporting to a PDF File &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md).</span></span>  
  
- <span data-ttu-id="cfa7c-164">**Word 呈现扩展插件**[!INCLUDE[msCoName](../includes/msconame-md.md)] Word 呈现扩展插件可将报表呈现为与 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 或更高版本兼容的 Word 文档。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-164">**Word Rendering Extension** The [!INCLUDE[msCoName](../includes/msconame-md.md)] Word rendering extension renders a report as a Word document that is compatible with [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 or later.</span></span> <span data-ttu-id="cfa7c-165">有关详细信息，请参阅 [导出到 Microsoft Word（报表生成器和 SSRS）](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)中处理数据。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-165">For more information, see [Exporting to Microsoft Word &#40;Report Builder and SSRS&#41;](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).</span></span>  
  
## <a name="report-processing-extensions"></a><span data-ttu-id="cfa7c-166">报表处理扩展插件</span><span class="sxs-lookup"><span data-stu-id="cfa7c-166">Report Processing Extensions</span></span>

 <span data-ttu-id="cfa7c-167">可以添加报表处理扩展插件，以便为 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]未随附的报表项提供自定义报表处理。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-167">Report processing extensions can be added to provide custom report processing for report items that are not included with [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].</span></span> <span data-ttu-id="cfa7c-168">默认情况下，报表服务器可以处理表、图表、矩阵、列表、文本框、图像以及所有其他报表项。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-168">By default, a report server can process tables, charts, matrices, lists, text boxes, images, and all other report items.</span></span> <span data-ttu-id="cfa7c-169">如果希望向在报表执行期间需要自定义处理的报表添加特殊功能（例如，如果希望嵌入 [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint 地图），则可以创建相应的报表处理扩展插件来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-169">If you want to add special features to a report that require custom processing during report execution (for example, if you want to embed a [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint map), you can create a report processing extension to do so.</span></span>  
  
## <a name="delivery-extensions"></a><span data-ttu-id="cfa7c-170">传递扩展插件</span><span class="sxs-lookup"><span data-stu-id="cfa7c-170">Delivery Extensions</span></span>

 <span data-ttu-id="cfa7c-171">后台处理应用程序使用传递扩展插件将报表传递到各个位置。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-171">The background processing application uses delivery extensions to deliver reports to various locations.</span></span> [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] <span data-ttu-id="cfa7c-172">包括电子邮件传递扩展插件和文件共享传递扩展插件。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-172">includes an e-mail delivery extension and a file share delivery extension.</span></span> <span data-ttu-id="cfa7c-173">电子邮件传递扩展插件可以通过简单邮件传输协议 (SMTP) 发送电子邮件，并在其中包含报表本身或指向报表的 URL 链接。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-173">The e-mail delivery extension sends an e-mail message through Simple Mail Transport Protocol (SMTP) that includes either the report itself or a URL link to the report.</span></span> <span data-ttu-id="cfa7c-174">还可以向寻呼程序、电话或其他设备发送没有 URL 链接或报表的简短通知。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-174">Short notices without the URL link or report can also be sent to pagers, phones, or other devices.</span></span> <span data-ttu-id="cfa7c-175">文件共享传递扩展插件可以将报表保存到网络上的共享文件夹中。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-175">The file share delivery extension saves reports to a shared folder on your network.</span></span> <span data-ttu-id="cfa7c-176">您可以指定位置、呈现格式和文件名，并覆盖所创建的文件的选项。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-176">You can specify a location, rendering format, and file name, and overwrite options for the file you create.</span></span> <span data-ttu-id="cfa7c-177">可以使用文件共享传递插件来存档所呈现的报表，并将其作为处理特大型报表的策略的一部分。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-177">You can use file share delivery for archiving rendered reports and as part of a strategy for working with very large reports.</span></span> <span data-ttu-id="cfa7c-178">传递扩展插件可以与订阅协同工作。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-178">Delivery extensions work in conjunction with subscriptions.</span></span> <span data-ttu-id="cfa7c-179">用户创建订阅时，可以选择一个可用的传递扩展插件，以确定如何传递报表。</span><span class="sxs-lookup"><span data-stu-id="cfa7c-179">When a user creates a subscription, the user chooses one of the available delivery extensions to determine how the report is delivered.</span></span>