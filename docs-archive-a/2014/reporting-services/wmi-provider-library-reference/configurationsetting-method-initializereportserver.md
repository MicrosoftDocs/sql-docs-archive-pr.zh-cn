---
title: InitializeReportServer 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6a8e44a98320ca2c9add6a1b6eef9362eef7731
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87581110"
---
# <a name="initializereportserver-method-wmi-msreportserver_configurationsetting"></a>InitializeReportServer 方法 (WMI MSReportServer_ConfigurationSetting)
  初始化指定的报表服务实例。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>parameters  
 *InstallationID*  
 用于在加密密钥返回之前对其进行加密的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
 *ExtendedErrors[]*  
 [out] 一个字符串数组，包含此调用返回的其他错误。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 调用此方法时，将使用由 *InstallationID*标识的报表服务器的公钥，对访问该报表服务器数据库安全信息的加密密钥进行加密。  
  
 指定报表服务器的公钥必须在先前已写入报表服务器数据库。  
  
 必须对已能访问安全信息的报表服务器调用 *InitializeReportServer* 方法，以便此方法可以解密加密密钥。 然后，所产生的已加密的加密密钥将存储在报表服务器数据库中。  
  
 如果在调用 InitializeReportServer 方法时，Report Server 的[IsInitialized](configurationsetting-property-isinitialized.md)属性设置为 `true` ，则该方法将返回 success，而不会尝试对加密密钥进行加密。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
