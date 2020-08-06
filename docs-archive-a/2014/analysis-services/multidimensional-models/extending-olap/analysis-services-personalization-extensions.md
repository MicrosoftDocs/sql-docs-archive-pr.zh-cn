---
title: Analysis Services 个性化设置扩展 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0cd36cb2882659bff902d9830af0c5acefd98444
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591607"
---
# <a name="analysis-services-personalization-extensions"></a>Analysis Services 个性化设置扩展
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化设置扩展是实现插件体系结构的理念的基础。 在插件体系结构中，您可以动态地开发新的多维数据集对象和功能，并可以与其他开发人员方便地共享。 因此， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展提供了可实现以下目的的功能：  
  
-   **动态设计和部署**设计和部署 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展后，用户可以在下一个用户会话开始时访问对象和功能。  
  
-   **接口独立性**无论你用来创建 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展的接口如何，用户都可以使用任何接口访问对象和功能。  
  
-   **会话上下文** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化设置扩展不是现有基础结构中的永久对象，不需要重新处理多维数据集。 在用户连接到数据库时，它们将公开并为该用户创建，并在整个用户会话期间保持可用。  
  
-   **快速分发**[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]与其他软件开发人员共享个性化设置扩展，无需深入了解如何查找此扩展功能的详细规范。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展具有多种用途。 例如，您的公司的销售涉及到多种货币。 您可创建一个计算成员，以本地货币返回访问此多维数据集的人员的总销售额。 首先要此成员创建为个性化设置扩展。 然后，将此计算成员与一组用户共享。 共享后，这些用户一连接到服务器就可以立即访问该计算成员。 即使用户使用的接口不是用于创建该计算成员的接口，也可以访问该计算成员。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]个性化设置扩展是对现有托管程序集体系结构的简单、精致的修改，并在整个 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] [microsoft.analysisservices.sharepoint.integration.dll AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120))对象模型、多维表达式 (MDX) 语法和架构行集中公开。  
  
## <a name="logical-architecture"></a>逻辑体系结构  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展的体系结构以托管程序集体系结构以及以下四个基本元素为基础：  
  
 [PlugInAttribute] 自定义属性  
 启动服务时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将加载所需的程序集，并确定哪些类具有[Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120))自定义属性。  
  
> [!NOTE]  
>  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 将定义自定义属性作为描述代码及影响运行时行为的方式。 有关详细信息，请参阅 MSDN 上的开发人员指南中的 "[属性概述](https://go.microsoft.com/fwlink/?LinkId=82929)" 主题 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 。  
  
 对于包含[microsoft.analysisservices.sharepoint.integration.dll. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120))自定义属性的所有类，将 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 调用其默认构造函数。 在启动时调用所有构造函数会提供一个共用位置，从该位置可不受任何用户活动干扰地生成新对象。  
  
 除了生成有关创作和管理个性化设置扩展的小型信息缓存外，类构造函数通常还会订阅 SessionOpened 和[microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))事件。 [microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . AdomdServer 事件。 未能订阅这些事件可能会导致将类错误地标记为由公共语言运行时 (CLR) 垃圾收集器进行清理。  
  
 会话上下文  
 对于基于个性化设置扩展的那些对象，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 会在客户端会话期间创建执行环境，并在此环境中动态地生成大多数对象。 与其他任何 CLR 程序集一样，此执行环境还可以访问其他函数和存储过程。 用户会话结束时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将删除动态创建的对象并关闭执行环境。  
  
 事件  
 对象创建是由会话事件 `On-Cube-OpenedCubeOpened` 和 `On-Cube-ClosingCubeClosing` 触发的。  
  
 客户端与服务器之间的通信是通过特定事件发生的。 这些事件使客户端了解会导致生成客户端对象的情况。 客户端环境是使用两种事件动态创建的：会话事件和多维数据集事件。  
  
 会话事件与服务器对象关联。 当客户端登录到服务器时，将 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 创建一个会话并触发[Microsoft.analysisservices.sharepoint.integration.dll. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))事件。 当客户端在服务器上结束会话时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将触发[Microsoft.analysisservices.sharepoint.integration.dll. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))事件。  
  
 多维数据集事件与连接对象关联。 连接到多维数据集会触发[microsoft.analysisservices.sharepoint.integration.dll. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120))事件。 关闭多维数据集的连接或通过更改为不同的多维数据集，就会触发[microsoft.analysisservices.sharepoint.integration.dll. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120))事件。  
  
 可跟踪性和错误处理  
 使用 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] 可跟踪所有活动。 未处理的错误会报告给 Windows 事件日志。  
  
 所有对象的创作和管理都是独立于此体系结构，是对象的开发人员的唯一责任。  
  
## <a name="infrastructure-foundations"></a>基础结构基础  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展基于现有组件。 下面简要列出了提供个性化设置扩展功能的增强功能和改进功能。  
  
### <a name="assemblies"></a>程序集  
 自定义特性[microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120))可添加到自定义程序集以标识 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 个性化设置扩展类。  
  
### <a name="changes-to-the-adomdserver-object-model"></a>对 AdomdServer 对象模型的更改  
 [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120))对象模型中的以下对象已增强或已添加到模型中。  
  
#### <a name="new-adomdconnection-class"></a>新增 AdomdConnection 类  
 [AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120))类是新增的，并通过属性和事件公开了多个个性化设置扩展。  
  
 **属性**  
  
-   [AdomdConnection *](/previous-versions/sql/sql-server-2014/bb678099(v=sql.120))，表示当前连接的会话 Id 的只读字符串值。 microsoft.analysisservices.sharepoint.integration.dll *。  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdConnection. ClientCulture *](/previous-versions/sql/sql-server-2014/bb677433(v=sql.120))，对与当前会话关联的客户端区域性的只读引用。  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdConnection *](/previous-versions/sql/sql-server-2014/bb630315(v=sql.120))，表示当前用户的标识接口的只读引用。  
  
 **事件**  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120))  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120))  
  
#### <a name="new-properties-in-the-context-class"></a>上下文类中的新增属性  
 [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120))类有两个新属性：  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll *](/previous-versions/sql/sql-server-2014/bb678098(v=sql.120))，它是对新服务器对象的只读引用。  
  
-   CurrentConnection *，它是对新[microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) AdomdServer 对象的只读引用。 [microsoft.analysisservices.sharepoint.integration.dll. AdomdServer](/previous-versions/sql/sql-server-2014/bb630975(v=sql.120))。  
  
#### <a name="new-server-class"></a>新增服务器类  
 [Microsoft.analysisservices.sharepoint.integration.dll](/previous-versions/sql/sql-server-2014/bb677955(v=sql.120))类是新类，并通过类属性和事件公开多个个性化设置扩展。  
  
 **属性**  
  
-   [Microsoft.AnalysisServices.AdomdServer.Server.Name *](/previous-versions/sql/sql-server-2014/bb677694(v=sql.120))，表示服务器名称的只读字符串值。  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll *](/previous-versions/sql/sql-server-2014/bb677437(v=sql.120))，它是对与服务器关联的全局区域性的只读引用。  
  
 **事件**  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
-   [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
#### <a name="adomdcommand-class"></a>AdomdCommand 类  
 [Microsoft.analysisservices.sharepoint.integration.dll. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120))类现在支持以下 MDX 命令：  
  
-   [CREATE MEMBER 语句 (MDX)](/sql/mdx/mdx-data-definition-create-member)  
  
-   [&#40;MDX&#41;更新成员语句](/sql/mdx/mdx-data-definition-update-member)  
  
-   [DROP MEMBER 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [CREATE SET 语句 (MDX)](/sql/mdx/mdx-data-definition-create-set)  
  
-   [DROP SET 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [&#40;MDX 创建 KPI 语句&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [DROP KPI 语句 &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>MDX 扩展和增强功能  
 通过 `caption` 属性、`display_folder` 属性和 `associated_measure_group` 属性对 CREATE MEMBER 命令进行了增强。  
  
 添加 UPDATE MEMBER 命令是为了在求解计算丢失优先顺序时需要更新的情况下避免重新创建成员。 更新无法更改计算成员的作用域，无法将计算成员移动到其他父级，也无法定义其他 `solveorder`。  
  
 通过 `caption` 属性、`display_folder` 属性和新 `STATIC | DYNAMIC` 关键字对 CREATE SET 命令进行了增强。 *静态*意味着仅在创建时计算设置。 *动态*意味着每次在查询中使用该集时都会计算该集。 如果省略关键字，默认值则为 `STATIC`。  
  
 在 MDX 语法中增加了 CREATE KPI 和 DROP KPI 命令。 可以从任意 MDX 脚本动态创建 KPI。  
  
### <a name="schema-rowsets-extensions"></a>架构行集扩展  
 在 MDSCHEMA_MEMBERS*作用域*添加。 作用域值如下：MDMEMBER_SCOPE_GLOBAL=1、MDMEMBER_SCOPE_SESSION=2。  
  
 在 MDSCHEMA_SETS 添加*set_evaluation_context*列。 将计算上下文值设置为：MDSET_RESOLUTION_STATIC = 1、MDSET_RESOLUTION_DYNAMIC = 2。  
  
 在 MDSCHEMA_KPIS 上，增加了作用域列。 作用域值如下：MDKPI_SCOPE_GLOBAL=1、MDKPI_SCOPE_SESSION=2。  
  
  
