---
title: GetReportServerUrls 方法 (WMI MSReportServer_Instance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f36a5ba10c05276cffabc155e5289d675db8dae7
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690335"
---
# <a name="getreportserverurls-method-wmi-msreportserver_instance"></a>GetReportServerUrls 方法 (WMI MSReportServer_Instance)
  返回可用于访问报表服务器和报表管理器的 URL 列表。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>parameters  
 *ApplicationName[]*  
 一个包含安装的应用程序的数组。 值为 `ReportServerWebService` 或 `ReportManager`。  
  
 *URLs[]*  
 一个包含已成功注册的 URL 的数组。  
  
 *长度*  
 一个包含返回数组的长度的整数值。  
  
 *HRESULT*  
 一个指示成功或错误代码的值。  
  
## <a name="return-values"></a>返回值  
  
## <a name="remarks"></a>备注  
 可通过 InvokeMethod 函数调用由 WMI 管理对象公开的方法。 有关详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework WMI 文档中的“Executing Methods on Management Objects”（对管理对象执行方法）。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
