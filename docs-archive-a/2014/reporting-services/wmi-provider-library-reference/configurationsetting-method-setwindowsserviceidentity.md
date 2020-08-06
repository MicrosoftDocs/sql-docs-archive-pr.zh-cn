---
title: SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 15d1b7fa5fc6d69a963785cdaf976c80623c47f3
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692174"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserver_configurationsetting"></a>SetWindowsServiceIdentity 方法 (WMI MSReportServer_ConfigurationSetting)
  将报表服务器 Windows 服务作为指定的 Windows 用户运行，并授予此帐户足够的文件系统权限以允许操作报表服务器。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>parameters  
 *UseBuiltInAccount*  
 指示指定的帐户是否是内置 Windows 帐户。  
  
 *帐户*  
 要用于运行 Windows 服务的 Windows 帐户，格式为“DOMAIN\alias”。  
  
 *密码*  
 帐户的密码。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 当*UseBuiltInAccount*参数设置为 `true` 并且 Report Server 在 MICROSOFT [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] 或 Windows XP 上运行时，将忽略*Name*、 *Domain*和*Password*参数的值，并使用本地系统帐户。  
  
 如果将*UseBuiltInAccount*参数设置为 `true` 并且 Report Server 在 Windows server 2003 上运行，则将忽略*Domain*和*Password*属性，并且名称字段必须包含 "builtin\system" 或 "Builtin\System" 或 "Builtin\LocalService"。  
  
 SetWindowsServiceIdentity 方法可对报表服务器安装目录中的文件和文件夹设置文件权限。  
  
 *帐户*参数中指定的帐户需要 `LogonAsService` Windows 中的权限。 该方法可将此权限授予指定的帐户。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
