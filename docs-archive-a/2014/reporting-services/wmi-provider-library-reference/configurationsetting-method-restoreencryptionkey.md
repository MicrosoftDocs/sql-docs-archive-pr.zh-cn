---
title: RestoreEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- RestoreEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- RestoreEncryptionKey method
ms.assetid: 37e949f5-15af-4858-848a-f482ee94fcd9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e67478541bab615a6d441ae273ed3385a8654203
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692194"
---
# <a name="restoreencryptionkey-method-wmi-msreportserver_configurationsetting"></a>RestoreEncryptionKey 方法 (WMI MSReportServer_ConfigurationSetting)
  将指定的加密密钥重新应用于报表服务器数据库。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub RestoreEncryptionKey(ByRef KeyFile() As Integer, _  
    ByRef Length As Int32, ByVal Password As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void RestoreEncryptionKey(out Byte[] KeyFile, out Int32 Length,   
            string Password, out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>parameters  
 *KeyFile[]*  
 [out] 包含已加密的加密密钥的数组。  
  
 *长度*  
 [out] 该方法返回的数组长度。  
  
 *密码*  
 用于对加密密钥进行加密的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
 *ExtendedErrors[]*  
 [out] 一个字符串数组，包含此调用返回的其他错误。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 如果报表服务器数据库中已经存在报表服务器的条目，则删除它。 然后，使用指定的加密密钥和报表服务器的公钥创建新条目。  
  
 在调用清除加密密钥列表的 [DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md) 方法之后调用该方法最有效。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
