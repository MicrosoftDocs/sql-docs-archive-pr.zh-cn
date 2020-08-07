---
title: 报表生成器中的数据连接、数据源和连接字符串 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efe6cea439ed91cd5e6d306c15e34c6dd688a37a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87588341"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a><span data-ttu-id="43933-102">报表生成器中的数据连接、数据源和连接字符串</span><span class="sxs-lookup"><span data-stu-id="43933-102">Data Connections, Data Sources, and Connection Strings in Report Builder</span></span>
  <span data-ttu-id="43933-103">为了在报表中包含数据，您需要创建数据连接和数据集。</span><span class="sxs-lookup"><span data-stu-id="43933-103">To include data in a report, you create data connections and datasets.</span></span> <span data-ttu-id="43933-104">数据连接包括有关如何访问外部数据源的信息。</span><span class="sxs-lookup"><span data-stu-id="43933-104">A data connection includes information about how to access an external source of data.</span></span> <span data-ttu-id="43933-105">数据集包含一个查询命令，用于指定通过使用数据连接要包含哪些数据。</span><span class="sxs-lookup"><span data-stu-id="43933-105">A dataset includes a query command that specifies which data to include by using the data connection.</span></span>  
  
1.  <span data-ttu-id="43933-106">**“报表数据”窗格中的数据源** 在创建嵌入数据源或添加共享数据源后，会在“报表数据”窗格中显示一个数据源。</span><span class="sxs-lookup"><span data-stu-id="43933-106">**Data sources in the Report Data pane** A data source appears in the Report Data pane after you create an embedded data source or add a shared data source.</span></span>  
  
2.  <span data-ttu-id="43933-107">**“连接”对话框** 使用“连接”对话框可以生成连接字符串或粘贴连接字符串。</span><span class="sxs-lookup"><span data-stu-id="43933-107">**Connection Dialog Box** Use the Connection Dialog Box to build a connection string or to paste a connection string.</span></span>  
  
3.  <span data-ttu-id="43933-108">**数据连接信息** 将连接字符串传递给数据扩展插件。</span><span class="sxs-lookup"><span data-stu-id="43933-108">**Data connection information** The connection string is passed to the data extension.</span></span>  
  
4.  <span data-ttu-id="43933-109">**凭据** 凭据与连接字符串是分开管理的。</span><span class="sxs-lookup"><span data-stu-id="43933-109">**Credentials** Credentials are managed separately from the connection string.</span></span>  
  
5.  <span data-ttu-id="43933-110">**数据扩展插件/数据访问接口** 对数据的连接可通过多个数据访问层。</span><span class="sxs-lookup"><span data-stu-id="43933-110">**Data Extension/Data Provider** Connecting to the data can be through multiple data access layers.</span></span>  
  
6.  <span data-ttu-id="43933-111">**外部数据源** 检索来自关系数据库、多维数据库、SharePoint 列表、Web 服务或报表模型的数据。</span><span class="sxs-lookup"><span data-stu-id="43933-111">**External data sources** Retrieve data from relational databases, multidimensional data bases, SharePoint lists, Web services, or report models.</span></span>  
  
 <span data-ttu-id="43933-112">有关详细信息，请参阅 Reporting Services 中的[嵌入和共享数据连接或数据源 &#40;报表生成器和 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)和[数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)。</span><span class="sxs-lookup"><span data-stu-id="43933-112">For more information, see [Embedded and Shared Data Connections or Data Sources &#40;Report Builder and SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) and [Data Connections, Data Sources, and Connection Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).</span></span>  
  
 <span data-ttu-id="43933-113">通过使用预定义的共享数据源、共享数据集和报表部件，也可以将数据包含在报表中。</span><span class="sxs-lookup"><span data-stu-id="43933-113">Data can also be included in a report by using predefined shared data sources, shared datasets, and report parts.</span></span> <span data-ttu-id="43933-114">这些项已具有您所需的数据连接信息。</span><span class="sxs-lookup"><span data-stu-id="43933-114">These items already have the data connection information that you need.</span></span> <span data-ttu-id="43933-115">有关详细信息，请参阅[将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="43933-115">For more information, see [Add Data to a Report &#40;Report Builder and SSRS&#41;](report-data/report-datasets-ssrs.md).</span></span>  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 <span data-ttu-id="43933-116">![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")</span><span class="sxs-lookup"><span data-stu-id="43933-116">![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")</span></span>  
  
##  <a name="connection-string-examples"></a><a name="ConnectionString"></a><span data-ttu-id="43933-117">连接字符串示例</span><span class="sxs-lookup"><span data-stu-id="43933-117">Connection String Examples</span></span>  
 <span data-ttu-id="43933-118">数据连接包括一个连接字符串，它通常由外部数据源的所有者提供。</span><span class="sxs-lookup"><span data-stu-id="43933-118">A data connection includes a connection string that is typically provided by the owner of the external data source.</span></span> <span data-ttu-id="43933-119">下表列出了不同外部数据源类型的连接字符串示例：</span><span class="sxs-lookup"><span data-stu-id="43933-119">The following table lists examples of connections strings for different types of external data sources.</span></span>  
  
|<span data-ttu-id="43933-120">**数据源**</span><span class="sxs-lookup"><span data-stu-id="43933-120">**Data source**</span></span>|<span data-ttu-id="43933-121">**示例**</span><span class="sxs-lookup"><span data-stu-id="43933-121">**Example**</span></span>|<span data-ttu-id="43933-122">**描述**</span><span class="sxs-lookup"><span data-stu-id="43933-122">**Description**</span></span>|  
|---------------------|-----------------|---------------------|  
|<span data-ttu-id="43933-123">本地服务器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库</span><span class="sxs-lookup"><span data-stu-id="43933-123">[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] database on the local server</span></span>|`data source="(local)";initial catalog=AdventureWorks2012`|<span data-ttu-id="43933-124">将数据源类型设置为 `SQL Server`。</span><span class="sxs-lookup"><span data-stu-id="43933-124">Set data source type to `SQL Server`.</span></span>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="43933-125">实例数据库</span><span class="sxs-lookup"><span data-stu-id="43933-125">instance database</span></span>|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|<span data-ttu-id="43933-126">将数据源类型设置为 `SQL Server`。</span><span class="sxs-lookup"><span data-stu-id="43933-126">Set data source type to `SQL Server`.</span></span>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] <span data-ttu-id="43933-127">Express 数据库</span><span class="sxs-lookup"><span data-stu-id="43933-127">Express database</span></span>|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|<span data-ttu-id="43933-128">将数据源类型设置为 `SQL Server`。</span><span class="sxs-lookup"><span data-stu-id="43933-128">Set data source type to `SQL Server`.</span></span>|  
|<span data-ttu-id="43933-129">本地服务器上的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库</span><span class="sxs-lookup"><span data-stu-id="43933-129">[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database on the local server</span></span>|`data source=localhost;initial catalog=Adventure Works DW 2012`|<span data-ttu-id="43933-130">将数据源类型设置为 `SQL Server Analysis Services`。</span><span class="sxs-lookup"><span data-stu-id="43933-130">Set data source type to `SQL Server Analysis Services`.</span></span>|  
|<span data-ttu-id="43933-131">SharePoint 列表</span><span class="sxs-lookup"><span data-stu-id="43933-131">SharePoint List</span></span>|`data source=http://MySharePointWeb/MySharePointSite/`|<span data-ttu-id="43933-132">将数据源类型设置为 `SharePoint List`。</span><span class="sxs-lookup"><span data-stu-id="43933-132">Set data source type to `SharePoint List`.</span></span>|  
||||  
|<span data-ttu-id="43933-133">报表模型</span><span class="sxs-lookup"><span data-stu-id="43933-133">Report Models</span></span>|<span data-ttu-id="43933-134">不适用。</span><span class="sxs-lookup"><span data-stu-id="43933-134">Not applicable.</span></span>|<span data-ttu-id="43933-135">报表模型不需要连接字符串。</span><span class="sxs-lookup"><span data-stu-id="43933-135">You do not need a connection string for a report model.</span></span> <span data-ttu-id="43933-136">在报表生成器中，找到报表服务器并选择表示报表模型的 .smdl 文件。</span><span class="sxs-lookup"><span data-stu-id="43933-136">In Report Builder, browse to the report server and select the .smdl file that is the report model.</span></span>|  
|<span data-ttu-id="43933-137">Oracle 服务器</span><span class="sxs-lookup"><span data-stu-id="43933-137">Oracle server</span></span>|`data source=myserver`|<span data-ttu-id="43933-138">将数据源类型设置为 `Oracle`。</span><span class="sxs-lookup"><span data-stu-id="43933-138">Set the data source type to `Oracle`.</span></span> <span data-ttu-id="43933-139">必须在报表生成器计算机上和报表服务器上安装 Oracle 客户端工具。</span><span class="sxs-lookup"><span data-stu-id="43933-139">The Oracle client tools must be installed on the Report Builder computer and on the report server.</span></span>|  
|<span data-ttu-id="43933-140">SAP NetWeaver BI 数据源</span><span class="sxs-lookup"><span data-stu-id="43933-140">SAP NetWeaver BI data source</span></span>|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|<span data-ttu-id="43933-141">将数据源类型设置为 `SAP NetWeaver BI`。</span><span class="sxs-lookup"><span data-stu-id="43933-141">Set the data source type to `SAP NetWeaver BI`.</span></span>|  
|<span data-ttu-id="43933-142">Hyperion Essbase 数据源</span><span class="sxs-lookup"><span data-stu-id="43933-142">Hyperion Essbase data source</span></span>|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|<span data-ttu-id="43933-143">将数据源类型设置为 `Hyperion Essbase`。</span><span class="sxs-lookup"><span data-stu-id="43933-143">Set the data source type to `Hyperion Essbase`.</span></span>|  
|<span data-ttu-id="43933-144">Teradata 数据源</span><span class="sxs-lookup"><span data-stu-id="43933-144">Teradata data source</span></span>|<span data-ttu-id="43933-145">`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`</span><span class="sxs-lookup"><span data-stu-id="43933-145">`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`</span></span>|<span data-ttu-id="43933-146">将数据源类型设置为 `Teradata`。</span><span class="sxs-lookup"><span data-stu-id="43933-146">Set the data source type to `Teradata`.</span></span> <span data-ttu-id="43933-147">连接字符串是包含四个字段的 Internet 协议 (IP) 地址，其中每个字段可以包含一至三位数。</span><span class="sxs-lookup"><span data-stu-id="43933-147">The connection string is an Internet Protocol (IP) address in the form of four fields, where each field can be from one to three digits.</span></span>|  
|<span data-ttu-id="43933-148">Teradata 数据源</span><span class="sxs-lookup"><span data-stu-id="43933-148">Teradata data source</span></span>|<span data-ttu-id="43933-149">`Database=` *\<database name>* `; data source=` *\<NN*N*>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`</span><span class="sxs-lookup"><span data-stu-id="43933-149">`Database=` *\<database name>* `; data source=` *\<NN*N*>.\<NNN>.\<NNN>.\<N*NN*>*`;Use X Views=False;Restrict to Default Database=True`</span></span>|<span data-ttu-id="43933-150">与前一示例类似，将数据源类型设置为 `Teradata`。</span><span class="sxs-lookup"><span data-stu-id="43933-150">Set the data source type to `Teradata`, similar to the previous example.</span></span> <span data-ttu-id="43933-151">请仅使用在 Database 标记中指定的默认数据库，不要自动发现数据关系。</span><span class="sxs-lookup"><span data-stu-id="43933-151">Only use the default database that is specified in the Database tag, and do not automatically discover data relationships.</span></span>|  
|<span data-ttu-id="43933-152">XML 数据源、Web 服务</span><span class="sxs-lookup"><span data-stu-id="43933-152">XML data source, Web service</span></span>|`data source=http://adventure-works.com/results.aspx`|<span data-ttu-id="43933-153">将数据源类型设置为 `XML`。</span><span class="sxs-lookup"><span data-stu-id="43933-153">Set the data source type to `XML`.</span></span> <span data-ttu-id="43933-154">连接字符串是支持 Web 服务定义语言 (WSDL) 的 Web 服务的 URL。</span><span class="sxs-lookup"><span data-stu-id="43933-154">The connection string is a URL for a web service that supports Web Services Definition Language (WSDL).</span></span>|  
|<span data-ttu-id="43933-155">XML 数据源、XML 文档</span><span class="sxs-lookup"><span data-stu-id="43933-155">XML data source, XML document</span></span>|`http://localhost/XML/Customers.xml`|<span data-ttu-id="43933-156">将数据源类型设置为 `XML`。</span><span class="sxs-lookup"><span data-stu-id="43933-156">Set the data source type to `XML`.</span></span> <span data-ttu-id="43933-157">其连接字符串是一个指向 XML 文档的 URL。</span><span class="sxs-lookup"><span data-stu-id="43933-157">The connection string is a URL to the XML document.</span></span>|  
|<span data-ttu-id="43933-158">XML 数据源、嵌入的 XML 文档</span><span class="sxs-lookup"><span data-stu-id="43933-158">XML data source, embedded XML document</span></span>|<span data-ttu-id="43933-159">*空*</span><span class="sxs-lookup"><span data-stu-id="43933-159">*Empty*</span></span>|<span data-ttu-id="43933-160">将数据源类型设置为 `XML`。</span><span class="sxs-lookup"><span data-stu-id="43933-160">Set the data source type to `XML`.</span></span> <span data-ttu-id="43933-161">XML 数据嵌入在报表定义中。</span><span class="sxs-lookup"><span data-stu-id="43933-161">The XML data is embedded in the report definition.</span></span>|  
  
 <span data-ttu-id="43933-162">有关每种连接类型的详细信息，请参阅[从外部数据源 &#40;ssrs&#41;](report-data/add-data-from-external-data-sources-ssrs.md)和[支持的数据源 Reporting Services &#40;Ssrs&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)中添加数据。</span><span class="sxs-lookup"><span data-stu-id="43933-162">For more information about each connection type, see [Add Data from External Data Sources &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) and [Data Sources Supported by Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).</span></span>  
  

  
##  <a name="creating-data-sources"></a><a name="Creating"></a><span data-ttu-id="43933-163">创建数据源</span><span class="sxs-lookup"><span data-stu-id="43933-163">Creating Data Sources</span></span>  
 <span data-ttu-id="43933-164">若要创建嵌入数据源，您必须具有一个连接字符串和访问数据所需的凭据。</span><span class="sxs-lookup"><span data-stu-id="43933-164">To create an embedded data source, you must have a connection string and the credentials that you need to access the data.</span></span> <span data-ttu-id="43933-165">此信息通常来自数据源的所有者。</span><span class="sxs-lookup"><span data-stu-id="43933-165">This information usually comes from the owner of the data source.</span></span> <span data-ttu-id="43933-166">数据连接作为数据源的一部分保存在报表定义中。</span><span class="sxs-lookup"><span data-stu-id="43933-166">The data connection is saved in the report definition as part of the data source.</span></span> <span data-ttu-id="43933-167">凭据和连接是分开管理的。</span><span class="sxs-lookup"><span data-stu-id="43933-167">Credentials are managed independently from the connection.</span></span> <span data-ttu-id="43933-168">有关分步说明，请参阅[添加和验证数据连接或数据源 &#40;报表生成器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="43933-168">For step-by-step instructions, see [Add and Verify a Data Connection or Data Source &#40;Report Builder and SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="43933-169">某些类型的凭据可能只支持报表生成器使用的一部分情形，而全部情形包括：在查询设计器中运行查询、未连接到报表服务器时从您的计算机预览报表以及从报表服务器运行报表。</span><span class="sxs-lookup"><span data-stu-id="43933-169">Some types of credentials might not support all the scenarios that Report Builder uses: to run a query in the query designer, preview a report from your computer when you are not connected to a report server, and run the report from the report server.</span></span> <span data-ttu-id="43933-170">建议您尽量使用共享数据源。</span><span class="sxs-lookup"><span data-stu-id="43933-170">We recommend that you use shared data sources whenever possible.</span></span> <span data-ttu-id="43933-171">可以在报表服务器上存储共享数据源的凭据。</span><span class="sxs-lookup"><span data-stu-id="43933-171">You can store credentials for a shared data source on the report server.</span></span> <span data-ttu-id="43933-172">有关详细信息，请参阅 [在报表生成器中指定凭据](../../2014/reporting-services/specify-credentials-in-report-builder.md)。</span><span class="sxs-lookup"><span data-stu-id="43933-172">For more information, see [Specify Credentials in Report Builder](../../2014/reporting-services/specify-credentials-in-report-builder.md).</span></span>  
  
 <span data-ttu-id="43933-173">若要创建共享数据源，必须使用报表管理器直接在 Report Server 上创建数据源，或在中使用创作环境（如报表设计器） [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="43933-173">To create a shared data source, you must use Report Manager to create the data source directly on the report server, or use an authoring environment such as Report Designer in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].</span></span> <span data-ttu-id="43933-174">有关详细信息，请参阅[&#40;SSRS&#41;创建嵌入数据源或共享数据源](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)。</span><span class="sxs-lookup"><span data-stu-id="43933-174">For more information, see [Create an Embedded or Shared Data Source &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md).</span></span>  
  

  
## <a name="see-also"></a><span data-ttu-id="43933-175">另请参阅</span><span class="sxs-lookup"><span data-stu-id="43933-175">See Also</span></span>  
 <span data-ttu-id="43933-176">[将数据添加到报表 &#40;报表生成器和 SSRS&#41;](report-data/report-datasets-ssrs.md) </span><span class="sxs-lookup"><span data-stu-id="43933-176">[Add Data to a Report &#40;Report Builder and SSRS&#41;](report-data/report-datasets-ssrs.md) </span></span>  
 [<span data-ttu-id="43933-177">报表部件（报表生成器和 SSRS）</span><span class="sxs-lookup"><span data-stu-id="43933-177">Report Parts &#40;Report Builder and SSRS&#41;</span></span>](report-parts-report-builder-and-ssrs.md)  
  
  