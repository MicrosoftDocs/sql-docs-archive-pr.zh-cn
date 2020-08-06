---
title: 配置报表的执行属性（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 51cd7b5db225b39f5a061ed750b2ef5cdd265b9a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591753"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>配置报表的执行属性（报表管理器）
  可以设置报表处理选项以指定何时为报表检索数据。 如果外部数据源按照特定的时间刷新（例如，每天或每周刷新数据仓库），并且您想要避免每当请求报表时对同一数据进行检索的开销，则为报表计划数据处理非常有用。 如果您想要控制外部数据库服务器上的处理负载，或者如果想要为必须使用相同数据集的多个用户提供一致的结果，则计划数据处理也很有用。 使用可变数据的按需运行报表每分钟都会生成不同的结果。 相反，报表快照则可用来针对包含同一时间点数据的其他报表或分析工具进行有效比较。  
  
 报表快照是一个报表，其中包含在特定时间点检索到的布局说明以及查询结果。 与按需运行报表（在选择该报表时可获得最新的查询结果）不同，报表快照按计划进行处理，再保存到报表服务器中。 当您选择报表快照进行查看时，报表服务器将在报表服务器数据库中检索存储的报表，然后显示快照创建时报表的数据和布局。  
  
 报表快照不以特定的呈现格式进行保存。 相反，将以用户或应用程序发出请求时的最终查看格式（如 HTML）来呈现报表快照。 延迟呈现会使快照具有可移植性。 报表可以采用适用于请求设备或 Web 浏览器的正确格式呈现。  
  
### <a name="to-configure-report-processing-options"></a>配置报表处理选项  
  
1.  启动 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)。  
  
2.  导航到并打开要设置处理选项的报表。  
  
 悬停在该报表之上，然后单击下拉箭头。  
  
1.  在下拉菜单中，单击“管理”，然后选择“处理选项”选项卡********。  
  
2.  单击 **“通过执行快照呈现此报表”**，然后选择以下选项之一：  
  
    -   如果要创建快照，则选择“使用下列计划创建报表执行快照”，再定义特定于报表的计划，或从“共享计划”列表中进行选择********。  
  
    -   如果希望立即创建快照，请选择 **“在此页上单击‘应用’按钮后创建报表快照”**。  
  
3.  单击“应用”。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表处理属性](../report-server/set-report-processing-properties.md)   
 [打开并关闭报表 &#40;报表管理器&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [“内容”页（报表管理器）](../contents-page-report-manager.md)   
 [报表服务器内容管理（SSRS 本机模式）](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [“处理选项”属性页（报表管理器）](../processing-options-properties-page-report-manager.md)  
  
  
