---
title: SoapException 错误表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SoapException class
ms.assetid: 3dbf1b5a-bd2a-4385-925d-5d095d72014c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b17ecc3049ce1afe07f3aa2e0b06f417d4f8dcee
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590040"
---
# <a name="soapexception-errors-table"></a>SoapException 错误表
  报表服务器基于在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中发生的错误在 SOAP 异常中生成错误和错误消息。 下表显示可通过报表服务器 Web 服务中的“SoapException”**** 从方法访问的错误。 该表按引发异常的方法组织。  
  
|方法|错误代码|  
|-----------------|----------------|  
|**ALL**|rsEvaluationCopyExpired****|  
|**ALL**|rsFailedToDecryptConfigInformation****|  
|**ALL**|rsInvalidRSEditionConfiguration****|  
|**ALL**|rsReportServerNotActivated****|  
|**ALL**|rsServerBusy****|  
|**ALL**|rsReportServerServiceUnavailable****|  
|**ALL**|rsReportServerDisabled****|  
|ALL****，但 GetPermissions****、GetRenderResource****、GetSystemPermissions****、ListEvents**** 和 ListSecureMethods**** 除外|rsAccessDenied****|  
|ALL****，但 CreateBatch****、ExecuteBatch****、GetSystemPolicies****、GetSystemPermissions****、GetSystemProperties****、ListEvents****、ListJobs****、ListRoles****、ListSchedules****、ListSecureMethods****、ListSubscriptions****、ListSystemRoles****、ListSystemTasks****、ListTasks**** 除外|rsMissingParameter****|  
|CreateDataDrivenSubscription****、CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateReportHistorySnapshot****、CreateResource****、CreateSubscription****、DeleteItem****、DeleteReportHistorySnapshot****、DisableDataSource****、EnableDataSource****、FindItems****、FlushCache****、GetCacheOptions****、GetDataSourceContents****、GetExecutionOptions****、GetPermissions****、GetPolicies****、GetProperties****、GetReportDataSourcePrompts****、GetReportDataSources****、GetReportDefinition****、GetReportHistoryLimit****、GetReportHistoryOptions****、GetReportLink****、GetReportParameters****、GetResourceContents****、GetRoleProperties****、GetServerDateTime****、IheritParentSecurity****、ListChildren****、ListLinkedReports****、ListReportHistory****、ListReportsUsingDataSource****、ListSchedules****、ListSubscriptions****、ListSubscriptionsUsingDataSource****、MoveItem****、Render****、RenderStream****、SetCacheOptions****、SetDataSourceContents****、SetExecutionOptions****、SetPolicies****、SetProperties****、SetReportDataSources****、SetReportDefinition****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetReportLink****、SetReportParameters****、SetResourceContents****、UpdateReportExecutionSnapshot****、ValidateExtensionSettings****|**rsItemNotFound**|  
|CancelBatch****、CreateDataDrivenSubscription****、CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateReportHistorySnapshot****、CreateResource****、CreateRole****、CreateSchedule****、CreateSubscription****、DeleteItem****、DeleteReportHistorySnapshot****、DeleteRole****、DeleteSchedule****、DeleteSubscription****、DisableDataSource****、EnableDataSource****、ExecuteBatch****、FindItems****、FlushCache****、GetResourceContents****、GetServerDateTime****、MoveItem****、PauseSchedule****、ResumeSchedule****、SetCacheOptions****、SetDataDrivenSubscriptionProperties****、SetDataSourceContents****、SetExecutionOptions****、SetPolicies****、SetProperties****、SetReportDataSources****、SetReportDefinition****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetReportLink****、SetReportParameters****、SetResourceContents****、SetRoleProperties****、SetScheduleProperties****、SetSubscriptionProperties****、SetSystemPolicies****、SetSystemProperties****、UpdateReportExecutionSnapshot****、ValidateExtensionSettings****|rsBatchNotFound****|  
|CreateDataDrivenSubscription****、CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateReportHistorySnapshot****、CreateResource****、CreateSubscription****、DeleteItem****、DeleteReportHistorySnapshot****、DisableDataSource****、EnableDataSource****、FindItems****、FlushCache****、GetCacheOptions****、GetDataSourceContents****、GetExecutionOptions****、GetItemType****、GetPermissions****、GetPolicies****、GetProperties****、GetReportDataSourcePrompts****、GetReportDataSources****、GetReportDefinition****、GetReportHistoryLimit****、GetReportHistoryOptions****、GetReportLink****、GetResourceContents****、GetServerDateTime****、IheritParentSecurity****、ListChildren****、ListLinkedReports****、ListReportHistory****、ListSchedules****、ListSubscriptionsUsingDataSource****、MoveItem****、Render****、RenderStream****、SetCacheOptions****、SetDataSourceContents****、SetExecutionOptions****、SetPolicies****、SetProperties****、SetReportDataSources****、SetReportDefinition****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetReportLink****、SetReportParameters****、SetResourceContents****、SetSubscriptionProperties****、UpdateReportExecutionSnapshot****、ValidateExtensionSettings****|rsInvalidItemPath****|  
|CreateDataDrivenSubscription****、CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateReportHistorySnapshot****、CreateResource****、CreateSubscription****、DeleteReportHistorySnapshot****、DisableDataSource****、EnableDataSource****、FindItems****、FlushCache****、GetCacheOptions****、GetDataSourceContents****、GetExecutionOptions****、GetReportDataSourcePrompts****、GetReportDataSources****、GetReportDefinition****、GetReportHistoryLimit****、GetReportHistoryOptions****、GetReportLink****、GetReportParameters****、GetResourceContents****、GetServerDateTime****、GetSystemProperties****、ListChildren****、ListLinkedReports****、ListReportHistory****、ListReportsUsingDataSource****、ListSchedules****、ListSubscriptions****、ListSubscriptionsUsingDataSource****、MoveItem****、Render****、RenderStream****、SetCacheOptions****、SetDataSourceContents****、SetExecutionOptions****、SetReportDataSources****、SetReportDefinition****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetReportLink****、SetReportParameters****、SetResourceContents****、UpdateReportExecutionSnapshot****、ValidateExtensionSettings****|rsWrongItemType****|  
|CreateReport****、CreateResource****、DeleteReportHistorySnapshot****、DeleteSchedule****、DeleteSubscription****、GetDataDrivenSubscriptionProperties****、GetSubscriptionProperties****、ListChildren****、ListScheduledReports****、PauseSchedule****、Render****、RenderStream****、ResumeSchedule****、SetCacheOptions****、SetDataDrivenSubscriptionProperties****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetScheduleProperties****、SetSubscriptionProperties****|rsParameterTypeMismatch****|  
|CreateDataDrivenSubscription****、CreateDataSource****、CreateSchedule****、CreateSubscription****、FindItems****、GetReportParameters****、PrepareQuery****、Render****、SetCacheOptions****、SetDataDrivenSubscriptionProperties****、SetDataSourceContents****、SetPolicies****、SetReportDataSources****、SetReportParameters****、SetScheduleProperties****、SetSubscriptionProperties****、SetSystemPolicies****|rsMissingElement****|  
|CreateDataDrivenSubscription****、CreateDataSource****、CreateSchedule****、CreateSubscription****、PrepareQuery****、Render****、SetCacheOptions****、SetDataDrivenSubscriptionProperties****、SetDataSourceContents****、SetProperties****、SetReportDataSources****、SetReportParameters****、SetScheduleProperties****、SetSubscriptionProperties****、SetSystemProperties****|rsInvalidElement****|  
|CreateDataDrivenSubscription****、CreateSchedule****、CreateSubscription****、FindItems****、GetRenderResource****、PrepareQuery****、Render****、RenderStream****、SetCacheOptions****、SetDataDrivenSubscriptionProperties****、SetExecutionOptions****、SetProperties****、SetReportHistoryOptions****、SetReportParameters****、SetScheduleProperties****、SetSubscriptionProperties****、SetSystemProperties****|rsElementTypeMismatch****|  
|CreateDataSource****、CreateRole****、GetDataDrivenSubscriptionProperties****、GetRenderResource****、ListExtensions****、Render****、SetDataDrivenSubscriptionProperties****、SetDataSourceContents****、SetExecutionOptions****、SetReportHistoryLimit****、SetReportHistoryOptions****、SetScheduleProperties****|rsInvalidParameter****|  
|CreateDataDrivenSubscription****、CreateReportHistorySnapshot****、CreateSubscription****、PrepareQuery****、SetDataDrivenSubscriptionProperties****、SetExecutionOptions****、SetReportHistoryOptions****、SetSubscriptionProperties****|**rsInvalidDataSourceCredentialSetting**|  
|CreateDataDrivenSubscriptionProperties****、CreateReportHistorySnapshot****、CreateSchedule****、CreateSubscription****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****、UpdateReportExecutionSnapshot****|rsReportParameterValueNotSet****|  
|CreateDataDrivenSubscription****、CreateSubscription****、GetExtensionSettings****、GetRenderResource****、Render****、RenderStream****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsMultipleExtensionsFoundInAssembly****|  
|CreateDataDrivenSubscriptionProperties****、CreateSubscription****、Render****、SetCacheOptions****、SetExecutionOptions****、SetReportParameters****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsReportParameterTypeMismatch****|  
|CreateSchedule****、CreateSubscription****、DeleteSchedule****、PauseSchedule****、ResumeSchedule****、SetCacheOptions****、SetExecutionOptions****、SetScheduleProperties****、SetSubscriptionProperties****|rsSchedulerNotResponding****|  
|DeleteSchedule****、GetScheduleProperties****、ListScheduledReports****、PauseSchedule****、ResumeSchedule****、SetCacheOptions****、SetExecutionOptions****、SetScheduleProperties****|rsScheduleNotFound****|  
|CreateDataDrivenSubscriptionProperties****、CreateSubscription****、Render****、SetReportParameters****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsReadOnlyReportParameter****|  
|CreateDataDrivenSubscriptionProperties****、CreateSubscription****、GetReportParameters****、Render****、SetReportParameters****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsUnknownReportParameter****|  
|DeleteSubscription****、GetDataDrivenSubscriptionProperties****、GetSubscriptionProperties****、SetDataDrivenSubscriptionProperties****、SetExecutionOptions****、SetSubscriptionProperties****|rsSubscriptionNotFound****|  
|CreateDataDrivenSubscription****、CreateSubscription****、GetExtensionSettings****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsDeliveryExtensionNotFound****|  
|CreateDataDrivenSubscription****、CreateSubscription****、GetExtensionSettings****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsDeliveryError****|  
|CreateDataDrivenSubscription****、GetDataDrivenSubscriptionProperties****、PrepareQuery****、SetDataDrivenSubscriptionProperties****|rsSecureConnectionRequired****|  
|CreateDataDrivenSubscription****、CreateSubscription****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsCannotSubscribeToEvent****|  
|CreateDataDrivenSubscription****、CreateSubscription****、FireEvent****、SetDataDrivenSubscriptionProperties****、SetSubscriptionProperties****|rsUnknownEventType****|  
|CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateResource****、MoveItem****|rsItemPathLengthExceeded****|  
|CopyItem****、CreateFolder****、CreateReport****、CreateResource****、DeleteItem****|rsReservedItem****|  
|CreateDataSource****、SetDataSourceContents****、SetReportDataSources****|rsInvalidElementCombination****|  
|SetCacheOptions****、SetExecutionOptions****、SetReportHistoryOptions****|rsInvalidParameterCombination****|  
|CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateResource****、MoveItem****|rsInvalidItemName****|  
|CreateDataSource****、CreateFolder****、CreateLinkedReport****、CreateReport****、CreateResource****、MoveItem****|rsItemAlreadyExists****|  
|CreateFolder****、CreateLinkedReport****、CreateReport****、CreateResource****、SetProperties****|rsReadOnlyProperty****|  
|GetPolicies****、GetSystemPolicies****、SetPolicies****、SetSystemPolicies****|rsInvalidPolicyDefinition****|  
|SetCacheOptions****、SetDataSourceContents****、SetReportDataSources****、SetReportParameters****|rsOperationPreventsUnattendedExecution****|  
|CreateReportHistorySnapshot****、Render****、PrepareQuery****、UpdateReportExecutionSnapshot****|rsInvalidDataSourceReference****|  
|CreateReportHistorySnapshot****、PrepareQuery****、Render****、UpdateReportExecutionSnapshot****|rsDataSourceDisabled****|  
|CreateReport****、PrepareQuery****、SetReportDefinition****|**rsProcessingError**|  
|GetRenderResource****、Render****、RenderStream****|rsInvalidReportLink****|  
|DeleteReportHistorySnapshot****、Render****、RenderStream****|rsReportHistoryNotFound****|  
|SetCacheOptions****、SetExecutionOptions****、SetReportHistoryOptions****|rsReportMayNotBeScheduled****|  
|CreateDataDrivenSubscription****、GetDataDrivenSubscriptionProperties****、SetDataDrivenSubscriptionProperties****|rsOperationNotSupported****|  
|CreateDataSource****、SetDataSourceContents****、SetReportDataSources****|rsDataExtensionNotFound****|  
|DeleteRole****、SetPolicies****、SetRoleProperties****|rsRoleNotFound****|  
|DeleteReportHistorySnapshot****、Render****、RenderStream****|rsParametersNotSpecified****|  
|GetReportParameters****、SetReportParameters****|rsNotSupported****|  
|SetReportParameters****、UpdateReportExecutionSnapshot****|rsReportSnapshotNotEnabled****|  
|CreateSchedule****、SetScheduleProperties****|rsScheduleAlreadyExists****|  
|CreateRole****、SetRoleProperties****|rsTaskNotFound****|  
|CreateRole****、SetRoleProperties****|rsMixedTasks****|  
|ListSubscriptions****、SetPolicies****|rsUnknownUserName****|  
|**MoveItem**|rsInvalidMove****|  
|RenderStream****|rsStreamNotFound****|  
|RenderStream****|rsMissingSessionId****|  
|**呈现**|rsReportNotReady****|  
|**呈现**|rsAssemblyNotPermissioned****|  
|SetExecutionOptions****|rsReportSnapshotEnabled****|  
|FindItems****|rsInvalidSearchOperator****|  
|SetReportDataSources****|rsDataSourceNotFound****|  
|PrepareQuery****、Render****|rsDataSourceNoPrompt****|  
|PrepareQuery****|rsCannotPrepareQuery****|  
|DeleteRole****|rsReservedRole****|  
|CreateRole****|rsEmptyRole****|  
|InheritParentSecurity****|rsInheritedPolicy****|  
|CreateRole****|rsRoleAlreadyExists****|  
|InheritParentSecurity****|rsCannotDeleteRootPolicy****|  
|CancelJob****|rsJobWasCanceled****|  
|ListSecureMethods****|rsServerConfigurationError****|  
  
## <a name="see-also"></a>另请参阅  
 [介绍 Reporting Services 中的异常处理](../introducing-exception-handling-in-reporting-services.md)   
 [错误和事件参考 &#40;Reporting Services&#41;](../../troubleshooting/errors-and-events-reference-reporting-services.md)   
 [Reporting Services SoapException 类](reporting-services-soapexception-class.md)   
 [使用 Detail 属性处理特定错误](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
