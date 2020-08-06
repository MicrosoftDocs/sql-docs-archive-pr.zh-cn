---
title: 预加载缓存（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b60b74f7ab5c0c843b848c09ee574fd59a99c682
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689777"
---
# <a name="preload-the-cache-report-manager"></a>预加载缓存（报表管理器）
  您可以通过为共享数据集创建缓存刷新计划，为共享数据集预加载缓存。  
  
 您可以通过以下两种方式为报表预加载缓存：  
  
1.  为报表创建缓存刷新计划。 这是首选方法。  
  
2.  使用数据驱动订阅可以用参数化报表的实例预加载缓存。 这也是在早于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]版本中预加载缓存的唯一方法。 有关详细信息，请参阅 [缓存报表 (SSRS)](caching-reports-ssrs.md)版本中预加载缓存的唯一方法。  
  
 必须首先满足以下条件才能缓存报表或共享数据集：  
  
-   共享数据集或报表必须已启用缓存。  
  
-   共享数据集或报表的共享数据源必须配置为使用存储凭据或没有凭据。  
  
-   必须运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。  
  
### <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>通过创建缓存刷新计划预加载缓存  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，导航到 **“内容”** 页，然后导航到要缓存的项。  
  
3.  将光标悬停在项之上，单击下拉列表，然后单击“管理”****。  
  
4.  单击 **“缓存刷新选项”** 选项卡。  
  
5.  在工具栏上，单击 **“新建缓存刷新计划”**。  
  
    > [!NOTE]  
    >  如果该项未启用缓存，系统将会提示您启用缓存。 若要启用缓存，请单击 **“确定”**。  
  
     “缓存刷新计划”页将打开。  
  
6.  可以根据需要键入刷新计划的说明。  
  
7.  对于共享计划，单击 **“共享计划”**，然后选择要使用的计划的名称。  
  
     对于自定义计划，单击“项特定的计划”****，然后单击“配置”****。  
  
8.  配置计划  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>通过使用数据驱动订阅将用户特定报表预加载到缓存中  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  在报表管理器中，导航到 **“内容”** 页，然后导航到要为其创建订阅的报表。  
  
3.  单击该报表，单击“订阅”**** 选项卡，再单击“新建数据驱动订阅”****。  
  
4.  可以根据需要键入订阅的说明。  
  
5.  从 **“指定通知收件人的方式”** 列表中，选择 **Null 传递提供程序**。  
  
6.  指定数据源类型，再单击 **“下一步”** 以配置数据源。  
  
7.  指定用于访问包含订阅服务器数据的数据源的连接类型、连接字符串和凭据。 以下示例演示用于连接到名为 Subscribers 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的连接字符串：  
  
    ```  
    data source=<servername>; initial catalog=Subscribers  
    ```  
  
8.  单击“下一步”。  
  
9. 指定检索订阅服务器数据的查询或命令。 对于处理时间很长的查询，可以根据需要延长超时期限。 例如：  
  
    ```  
    Select * from UserInfo  
    ```  
  
10. 单击 **“验证”** 。 在继续之前，必须验证查询。 在出现 **“查询验证成功”** 消息时，单击 **“下一步”**。  
  
11. 由于不能为 Null 传递提供程序配置传递扩展插件设置，请单击 **“下一步”**。  
  
12. 为订阅指定报表参数值，再单击 **“下一步”**。  
  
13. 指定处理订阅的时间。 不要选择 **“在报表服务器上更新报表数据时”**。 该设置仅适用于快照。 如果要使用预先存在的计划，请选择“根据共享计划”****。  
  
     若要创建自定义计划，请单击 **“根据为此订阅创建的计划”** ，再单击 **“下一步”**。 配置计划，再单击 **“完成”**。  
  
    > [!NOTE]  
    >  为确保订阅服务器能接收到最新的报表，所配置的计划应与为订阅服务器定义的报表传递计划相一致。 有关详细信息，请参阅[报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
14. 按照下面的步骤为报表配置执行选项。 在报表页上，单击 **“属性”** 选项卡。  
  
15. 在左框架中，单击 **“执行”** 选项卡。  
  
16. 在该页上，选择 **“用最新数据呈现此报表”**。  
  
17. 选择如下两个缓存选项之一并配置过期时间：  
  
    -   若要使缓存的副本在特定的时间段后过期，请单击 **“缓存报表的临时副本。在数分钟之后使报表副本过期”。** 键入报表过期所需的分钟数。  
  
    -   若要按计划使缓存的副本过期，请单击“缓存报表的临时副本” **。按下列计划使报表副本过期。** 单击“配置”****，或选择一个共享计划以设置报表过期计划。  
  
18. 单击“应用”。  
  
## <a name="see-also"></a>另请参阅  
 [Data-Driven Subscriptions](../subscriptions/data-driven-subscriptions.md)   
 [创建数据驱动订阅（SSRS 教程）](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [性能、快照、缓存 &#40;Reporting Services&#41;](performance-snapshots-caching-reporting-services.md)   
 [设置报表处理属性](set-report-processing-properties.md)   
 [缓存报表 (SSRS)](caching-reports-ssrs.md)  
  
  
