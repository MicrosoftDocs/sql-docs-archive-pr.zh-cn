---
title: 为 (PowerPivot for SharePoint 配置使用情况数据收集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
author: minewiskan
ms.author: owend
ms.openlocfilehash: 90a071cf8380d1a951fcc413d659a22e7e420853
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589287"
---
# <a name="configure-usage-data-collection-for-powerpivot-for-sharepoint"></a>配置使用情况数据收集 (PowerPivot for SharePoint)
  使用情况数据收集是场级 SharePoint 功能。 PowerPivot for SharePoint 使用并扩展此系统以便在 PowerPivot 管理面板中提供显示 PowerPivot 数据和服务的使用情况的报告。 根据您安装 SharePoint 的方式，可能会为场禁用使用情况数据收集。 场管理员必须启用使用情况日志记录，才能创建显示在 PowerPivot 管理面板中的使用情况数据。  
  
 有关 PowerPivot 管理面板中使用情况数据的信息，请参阅 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)。  
  
 **本主题内容：**  
  
 [启用使用情况数据收集并选择触发数据收集的事件](#events)  
  
 [设置日志文件位置](#configdb)  
  
 [配置使用情况数据收集中使用的计时器作业](#jobs)  
  
 [限制存储使用情况数据历史记录的时间长度](#confighist)  
  
 [出于报告目的定义快速、中等和较慢的查询响应类别](#qrh)  
  
 [指定向使用情况数据收集系统报告查询统计信息的频率](#ttr)  
  
 [打开“PowerPivot 服务应用程序”页以访问配置设置](#openconfig)  
  
 [PowerPivot 使用情况数据收集的默认配置](#defaultconfig)  
  
> [!IMPORTANT]  
>  使用情况数据帮助您深入了解用户访问数据和资源的方式，但它不保证提供有关服务器操作和用户访问的可靠的永久数据。 例如，如果存在服务器重新启动，则事件使用情况数据将丢失，并且将无法恢复。 同样，如果临时日志文件达到最大大小，则在清除文件前将不会添加任何新数据。 如果您需要审核功能，请考虑使用 SharePoint 提供的工作流和内容类型功能来为您的场构建审核子系统。 有关详细信息，请查找网站上的产品和社区文档。  
  
##  <a name="enable-usage-data-collection-and-choose-events-that-trigger-data-collection"></a><a name="events"></a>启用使用情况数据收集并选择触发数据收集的事件  
 在 SharePoint 管理中心中配置使用情况数据收集。  
  
1.  在管理中心中，单击 **“监视”**。  
  
2.  在 **“报告”** 部分中，单击 **“配置 Usage and Health Data Collection”**。  
  
3.  选中 **“启用使用率数据集”**。  
  
4.  在 **“要记录的事件”** 部分中，选中或清除有关复选框以启用或禁用以下 Analysis Services 事件：  
  
    |事件|说明|  
    |-----------|-----------------|  
    |**PowerPivot 连接**|PowerPivot 连接事件用于监视代表用户进行的 PowerPivot 服务器连接。|  
    |**PowerPivot 加载数据使用情况**|PowerPivot 加载数据使用情况用于监视将 PowerPivot 数据加载到服务器内存中的请求。 将为从内容数据库或从缓存加载的 PowerPivot 数据文件生成加载事件。|  
    |**PowerPivot 卸载数据使用情况**|PowerPivot 卸载数据使用情况用于监视在一段非活动期后卸载 PowerPivot 数据源的请求。 将 PowerPivot 数据源缓存到磁盘将报告为卸载事件。|  
    |**PowerPivot 查询使用情况**|PowerPivot 查询使用情况用于监视在 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 实例中加载的数据的查询处理时间。|  
  
    > [!NOTE]  
    >  服务器运行状况和数据刷新操作也生成使用情况数据，但没有与这些进程相关联的事件。  
  
5.  您还可以更新日志文件的位置。 有关详细信息，请参阅下一节。  
  
6.  **** 单击“确定”以保存你的更改。  
  
7.  或者，您可以指定是记录所有消息还是只记录错误。 有关如何限制事件消息的详细信息，请参阅[配置和查看 SharePoint 日志文件和诊断日志记录 &#40;PowerPivot for SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)。  
  
##  <a name="set-log-file-location"></a><a name="configdb"></a>设置日志文件位置  
 PowerPivot 使用情况数据最初存储于本地服务器上的使用情况日志文件中，然后定期移到 PowerPivot 服务应用程序数据库。 在管理中心中设置日志文件的位置。 默认位置为：  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 若要查看或更改这些属性，请使用 **“Usage and Health Data Collection”** 页。  
  
1.  在管理中心的主页上，单击 **“监视”**。  
  
2.  在“监视”部分中，单击 **“配置 Usage and Health Data Collection”**。  
  
3.  在“使用率数据集设置”中，查看或修改文件位置、名称或最大文件大小。 如果您指定的最大文件大小过小，则该文件大小将很快达到最大值限制，并且在其内容移到中心使用情况数据收集数据库之前，不会有新条目添加到该文件。  
  
##  <a name="configure-the-timer-jobs-used-in-usage-data-collection"></a><a name="jobs"></a>配置使用情况数据收集中使用的计时器作业  
 PowerPivot 服务器运行状况和使用情况数据通过两个计时器作业移到使用情况数据收集系统中的不同位置。  
  
-   "Microsoft SharePoint Foundation 使用率数据导入" 计时器作业将 PowerPivot 使用情况移动到 PowerPivot 服务应用程序数据库。  
  
-   "PowerPivot 管理面板处理计时器作业" 将数据到 PowerPivot 工作簿，该工作簿是内置管理报表的数据源。  
  
 如果您需要更频繁地刷新出现在 PowerPivot 管理面板中的管理报告，则按照以下步骤执行。  
  
1.  在管理中心中，单击 **“监视”**。  
  
2.  单击 "**查看作业定义"。** 在“计时器作业”**** 部分中：  
  
3.  单击 **“Microsoft SharePoint Foundation 使用情况数据导入”**。  
  
4.  单击 "**立即运行**"。 如果禁用 **“立即运行”** 按钮，请依次单击 **“启用”** 和 **“立即运行”**。  
  
5.  在“作业定义”列表中，单击 **“PowerPivot 数据管理面板处理计时器作业”**。  
  
6.  单击 "**立即运行**"。  
  
7.  检查报告以查看刷新数据。 有关详细信息，请参阅 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)。  
  
##  <a name="limit-how-long-usage-data-history-is-stored"></a><a name="confighist"></a>限制存储使用情况数据历史记录的时间长度  
 为事件（连接、加载、卸载和按需查询处理）和数据刷新（计划的数据处理）存储使用情况数据历史记录。 尽管使用情况数据是通过 SharePoint 使用情况数据收集系统收集的，但报告的数据将移到 PowerPivot 应用程序数据库和报表数据库以便更长期地存储。 使用情况数据历史设置控制使用情况数据在 PowerPivot 应用程序数据库中应保留多长的时间。 相同的限制同样适用于同一 PowerPivot 服务应用程序数据库中存储的所有类型的使用情况数据。  
  
1.  [打开“PowerPivot 服务应用程序”页](#openconfig)。  
  
2.  在 **“使用情况数据收集”** 部分的 **“使用情况数据历史记录”** 中，输入您希望为每个工作簿保留数据刷新活动记录的天数。  
  
    -   默认值为 365 天。  
  
    -   0 指定不受限制的存储，使用情况数据将无限期地保留。  
  
    -   或者，也可以指定一个介于 1 和 5000 之间的范围。  
  
     将保留期减小到较少的天数将删除超过这个新限制的任何数据。 例如，将该值从 365 更改为 30 将导致删除超过 30 天前发生的所有历史记录信息的使用情况数据。 仅保留最近 30 天内的数据。  
  
     数据实际在发生下一个事件时被数据。 仅当系统处理某一事件时，才检查对使用情况数据历史记录的限制。  
  
3.  单击“确定”。  
  
 有关如何收集和存储使用情况数据的详细信息，请参阅[PowerPivot 使用情况数据收集](power-pivot-usage-data-collection.md)。  
  
##  <a name="define-fast-medium-and-slow-query-response-categories-for-reporting-purposes"></a><a name="qrh"></a>出于报告目的定义快速、中等和慢的查询响应类别  
 查询处理性能根据预定义的类别进行测量，这些预定义的类别按完成所用的时间长度定义请求-响应周期。 预定义的类别包括：一般、快速、预期、长时间运行和超出。 对 PowerPivot 服务器的每个请求都将基于完成时间属于上述类别之一。  
  
 查询响应信息用于活动报告中。 在这些报告内，为了更好地揭示 PowerPivot 系统的性能趋势，每种类别的用法各不相同。 例如，一般请求将被完全排除，因为这样做可以消除数据中的干扰并且使用其余类别显示更有意义的趋势。 相反，长时间运行或超出的请求统计信息是报告中的重点，以便管理员或工作簿所有者可以立即采取纠正措施。  
  
 虽然您不能添加或删除类别，但可以定义上限和下限，以确定一个类别从哪里结束、另一个类别从哪里开始。 如果您的组织使用服务级别协议 (SLA) 定义服务器可用性和性能的可接受级别，则您可以优化这些类别以反映您创建的 SLA。  
  
1.  [打开“PowerPivot 服务应用程序”页](#openconfig)。  
  
2.  在“使用情况数据收集”**** 部分的“一般响应上限”**** 中，输入设置完成一般响应的上限的值（毫秒）。 属于此类别的请求通常包括服务器 ping、会话初始化和元数据查询。 默认值为 500 毫秒（或半秒钟）。  
  
3.  在“快速请求上限”中，输入设置完成快速响应的上限的值（毫秒）。 属于此类别的请求包含对非常小的数据集或大型数据集的元数据服务器的查询。 默认值为 1000 毫秒（或 1 秒钟）。  
  
4.  在“预期响应上限”**** 中，输入设置在预期或平均时间范围内完成某一响应的上限的值（毫秒）。 属于此类别的请求包括将数据加载到查看器中。 默认值为 3000 毫秒（或 3 秒钟）。  
  
5.  在“长时间响应上限”**** 中，输入设置完成长时间运行响应的上限的值（毫秒）。 属于此类别的请求的运行时间比预期时间要长，但仍在可接受的范围内。 默认值为 10000 毫秒（或 10 秒钟）。  
  
     超出此限制的任何请求输入“超出” ** 类别。 对于“超出” ** 类别，没有可配置的阈值。 根据您在“长请求上限”中指定的上限推断出该值。 属于“超出”类别的请求的运行时间长于您定义的 SLA 所允许的时间。  
  
6.  单击“确定”。  
  
##  <a name="specify-how-often-query-statistics-are-reported-to-the-usage-data-collection-system"></a><a name="ttr"></a>指定向使用情况数据收集系统报告查询统计信息的频率  
 生成报告的时间间隔指定向使用情况数据收集系统报告查询统计信息的频率。 查询统计信息在进程中累积，并且定期作为单个事件报告。 您可以调整该时间间隔以便写入日志文件的间隔更长或更短。  
  
1.  [打开“PowerPivot 服务应用程序”页](#openconfig)。  
  
2.  在“使用情况数据收集”**** 部分的“查询报告间隔”**** 中，输入经过多少秒后服务器将所有类别（一般、快速、预期、长时间运行和超出）的查询统计信息作为单个事件报告给使用情况数据收集系统。  
  
    -   该范围是 1 到任意正整数。  
  
    -   默认值为 300 秒（或 5 分钟）。 对于运行多种应用程序和服务的动态场环境推荐此值。  
  
     如果您将该值提高得过多，则在报告之前可能会丢失统计信息。 例如，服务重新启动将导致查询统计信息丢失。 相反，如果内置活动报告中显示数据不足，请考虑减少该时间间隔以便更频繁地获取生成报告事件。  
  
3.  单击“确定”。  
  
##  <a name="open-the-powerpivot-service-application-page-to-access-configuration-settings"></a><a name="openconfig"></a>打开 "PowerPivot 服务应用程序" 页以访问配置设置  
 您必须是场管理员或服务管理员才能修改服务应用程序设置。 如果您在场中定义了多个 PowerPivot 服务应用程序，则必须单独修改每个应用程序。  
  
1.  在 SharePoint 管理中心内，在 **“应用程序管理”** 中单击 **“管理服务应用程序”**。  
  
2.  找到 PowerPivot 服务应用程序。 您可以通过类型来确定服务应用程序。 PowerPivot 服务应用程序的类型为 **“PowerPivot 服务应用程序”**。  
  
3.  单击 PowerPivot 服务应用程序名称。 将打开 PowerPivot 管理面板。  
  
4.  在 **“操作”** 中，单击 **“配置服务应用程序设置”**。 将打开“PowerPivot 服务应用程序设置”页。  
  
##  <a name="the-default-configuration-for-powerpivot-usage-data-collection"></a><a name="defaultconfig"></a>PowerPivot 使用情况数据收集的默认配置  
 可以使用默认设置启用针对 PowerPivot 服务操作的使用情况数据收集，以使其立即可用于支持 Analysis Services 集成功能的应用程序。 默认设置包括触发使用情况数据收集的事件、对存储多长时间的使用情况数据的限制以及用于对查询响应时间进行分类的阈值。  
  
 下表显示了使用情况数据收集配置的默认值。  
  
|设置|默认值|类型|有效范围|  
|-------------|-------------------|----------|-----------------|  
|**Analysis Services 使用事件** （连接、加载、卸载、请求）|\<enabled>|Boolean|这些值可以启用或禁用。|  
|**查询报告间隔**|300（以秒为单位）|Integer|1 到任意正整数。 默认为 5 分钟。|  
|**“使用情况数据历史记录”**|365（以天为单位）|Integer|0 指定无限制，但您也可以设置使历史数据过期并将自动删除它的上限。 有限保留期的有效值为 1 到 5000（单位为天）。|  
|一般响应上限|500（以毫秒为单位）|Integer|设置定义一般请求-响应交换的上限。 在 0 到 500 毫秒之间完成的任何请求都是一般请求，并且出于报告目的将被忽略。|  
|快速响应上限|1000（以毫秒为单位）|Integer|设置定义快速请求-响应交换的上限。|  
|“预期响应上限”|3000（以毫秒为单位）|Integer|设置定义预期请求-响应交换的上限。|  
|长时间运行响应上限|10000（以毫秒为单位）|Integer|设置定义长时间运行的请求-响应交换的上限。 超出此上限的任何请求都属于“超出”类别，因此没有上限。|  
  
## <a name="see-also"></a>另请参阅  
 [配置设置引用 &#40;PowerPivot for SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [PowerPivot 使用情况数据收集](power-pivot-usage-data-collection.md)  
  
  
