---
title: SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b5c62777edd1fab2b0cb3babc13ab09f7bcf32a9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692192"
---
# <a name="setdatabaseconnection-method-wmi-msreportserver_configurationsetting"></a>SetDatabaseConnection 方法 (WMI MSReportServer_ConfigurationSetting)
  设置与特定报表服务器数据库的报表服务器数据库连接。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>parameters  
 *Server*  
 用于托管报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称。  
  
 *DatabaseName*  
 报表服务器数据库的名称。  
  
 *CredentialsType*  
 用于连接的凭据类型。 值可以是：  
  
-   0 - Windows  
  
-   1 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Windows 服务  
  
 *UserName*  
 连接报表服务器数据库时所用的帐户名。  
  
 *密码*  
 连接报表服务器数据库时所用的密码。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 当 CredentialsType 参数设置为 0 (Windows) 时，必须设置 UserName 和 Password 参数    。 UserName 参数的格式必须为“domain\username”，相应的值必须代表有效的 Windows 登录名  。  
  
 如果将 CredentialsType 参数设置为 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])，则 UserName 参数传递的值必须符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的要求****。  
  
 如果将 CredentialsType 参数设置为 2（Windows 服务），则报表服务器将使用集成安全性连接到报表服务器数据库，并且忽略 UserName 和 Password 参数    。 报告服务器 Web 服务将使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 帐户或应用程序池的帐户及 Windows 服务帐户访问报表服务器数据库。  
  
 调用后，SetDatabaseConnection 方法将加密凭据和数据库信息并将它们存储在指定报表服务器的配置文件中。  
  
 SetDatabaseConnection 方法不会检查报表服务器是否可以使用指定的数据连接到报表服务器数据库。  
  
 在第一次设置时，将根据以下处理器来设置 ConnectionPoolSize 属性：ConnectionPoolSize = #Processors * 75。  
  
 SetDatabaseConnection 方法不会向指定的帐户授予权限。 您必须为需要访问报表服务器数据库的每一帐户调用 [GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md) 方法，然后运行所生成的脚本。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
