---
title: 为报表和共享数据集处理设置超时值 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c891b4911994ba2814a612439f141d16e4ad12a6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586329"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>为报表和共享数据集处理设置超时值 (SSRS)
  可以通过指定超时值来限制使用系统资源的方式。 报表服务器支持两种类型的超时值：  
  
-   嵌入数据集查询超时值，即报表服务器等待数据库响应的秒数。 此值在报表中定义。  
  
-   共享数据集查询超时值，即报表服务器等待数据库响应的秒数。 该值是共享数据集定义的一部分，并且可在您在报表服务器上管理共享数据集时进行管理。  
  
-   报表执行超时值，即在停止前报表可持续处理的最大秒数。 此值在系统级定义。 可以针对不同的报表采用不同的设置。  
  
 大多数超时错误出现在查询处理期间。 如果遇到超时错误，请尝试增大查询超时值。 请确保将报表执行超时值调整为大于查询超时值。时间段应该足以完成查询和报表处理。  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>为报表中的嵌入数据集设置查询超时值  
 查询超时值是在创作报表过程中在定义嵌入数据集时指定的。 该超时值随报表一起存储，它存储在报表定义的 `Timeout` 元素中。 默认情况下，此值设置为 30 秒。 有关详细信息，请参阅 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 对已发布报表的属性具有修改权限的用户可以通过编辑报表定义文件来重置此值。  
  
 还可以为数据驱动订阅指定查询超时值。 查询超时值是在“数据驱动订阅”页中指定的。 指定的值决定了报表服务器在从订阅服务器数据源检索数据时等待查询处理完成的时间。  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>为共享数据集设置查询超时值  
 当您创建或管理共享数据集时在报表服务器上以秒为单位指定查询超时值。 默认情况下，该值设置为 0 秒，这相当于无超时值。 有关详细信息，请参阅 [管理共享数据集](../report-data/manage-shared-datasets.md)。  
  
## <a name="setting-a-report-execution-time-out"></a>设置报表执行超时值  
 可以通过设置报表执行超时值来限制报表服务器用于处理报表的时间量。 报表执行超时值可以在报表管理器中指定。 可以为“站点设置”页中的所有报表设置默认值，然后覆盖特定报表的“执行”属性页中的值。 默认情况下，该值设置为 1800 秒。 有关详细信息，请参阅 [设置报表处理属性](set-report-processing-properties.md)。  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>报表执行超时值的计算方法  
 报表服务器每隔 60 秒对正在运行的作业进行一次计算。 每隔 60 秒，报表服务器就会将实际处理时间与报表执行超时值进行比较。 如果报表的执行时间超过了报表执行超时值，则将停止报表处理。  
  
 请注意，如果指定的超时值小于 60 秒，且报表处理的开始时间和完成时间均发生在报表服务器未对正在运行的作业进行计算的空闲时间段，则报表可以完全执行。 例如，如果将报表的超时值设置为 10 秒，而运行报表需要 20 秒，并且报表处理开始于 60 秒周期的前期，则报表可以完全处理。  
  
> [!NOTE]  
>  可以在 RSReportServer.config 文件中设置 `RunningRequestsDbCycle` 设置，以更改计算正在运行的作业的频率。  
  
## <a name="see-also"></a>另请参阅  
 [在 SharePoint 集成模式下 &#40;Reporting Services 设置处理选项&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Reporting Services 报表服务器（本机模式）](reporting-services-report-server-native-mode.md)   
 [管理正在运行的进程](../subscriptions/manage-a-running-process.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)  
  
  
