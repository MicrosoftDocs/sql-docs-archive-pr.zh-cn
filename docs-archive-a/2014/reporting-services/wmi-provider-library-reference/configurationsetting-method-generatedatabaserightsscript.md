---
title: GenerateDatabaseRightsScript 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 768e73d13d3b06f7913c3c816fded1b28c56199f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87692201"
---
# <a name="generatedatabaserightsscript-method-wmi-msreportserver_configurationsetting"></a>GenerateDatabaseRightsScript 方法 (WMI MSReportServer_ConfigurationSetting)
  生成一个 SQL 脚本，用来向用户授予运行报表服务器所需的报表服务器数据库和其他数据库的权限。 调用者需要能够连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库服务器并能够执行该脚本。  
  
## <a name="syntax"></a>语法  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>parameters  
 *UserName*  
 通过此脚本授予权限时作为授予对象的用户的用户名或 Windows 安全标识符 (SID)。  
  
 *DatabaseName*  
 脚本要向用户授予访问权限的数据库名称。  
  
 *IsRemote*  
 一个布尔值，指示对于报表服务器而言数据库是否为远程数据库。  
  
 *IsWindowsUser*  
 一个布尔值，指示指定用户名是 Windows 用户还是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 *脚本*  
 [out] 包含所生成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 脚本的字符串。  
  
 *HRESULT*  
 [out] 指示调用是成功还是失败的值。  
  
## <a name="return-value"></a>返回值  
 返回 *HRESULT* ，指示方法调用是成功还是失败。 值 0 指示方法调用已成功。 非零值指示已发生错误。  
  
## <a name="remarks"></a>备注  
 如果 *DatabaseName* 为空，则忽略 *IsRemote* ，并且数据库名称使用报表服务器配置文件中的值。  
  
 如果将*如果 iswindowsuser*设置为 `true` ，*用户名*的格式应为 \<domain> \\<用户名 \> 。  
  
 如果将*如果 iswindowsuser*设置为 `true` ，则生成的脚本将向用户授予登录权限 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，将 Report Server 数据库设置为默认数据库，并授予对 Report Server 数据库、Report Server 临时数据库、master 数据库和 MSDB 系统数据库的**RSExec**角色。  
  
 当*如果 iswindowsuser*设置为时 `true` ，该方法接受标准 Windows sid 作为输入。 在提供标准的 Windows SID 或服务帐户名后，它们会转换为用户名字符串。 如果数据库是本地数据库，相应帐户会正确转换为帐户的本地化表示形式。 如果数据库是远程数据库，则相应帐户会表示为该计算机的帐户。  
  
 下表显示了转换后的帐户及其远程表示形式。  
  
|被转换的帐户/SID|公用名|远程名称|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|Local System|\<Domain>\\<ComputerName\>$|  
|.\LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|ComputerName\LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|LocalSystem|Local System|\<Domain>\\<ComputerName\>$|  
|(S-1-5-20)|Network Service|\<Domain>\\<ComputerName\>$|  
|NT AUTHORITY\NetworkService|Network Service|\<Domain>\\<ComputerName\>$|  
|(S-1-5-19)|Local Service|错误 - 参见下方内容。|  
|NT AUTHORITY\LocalService|Local Service|错误 - 参见下方内容。|  
  
 在 [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)]上，如果使用的是内置帐户，且报表服务器数据库是远程数据库，将返回错误。  
  
 如果指定了 `LocalService` 内置帐户，且报表服务器数据库是远程数据库，将返回错误。  
  
 如果 *IsWindowsUser* 为 true，且 *UserName* 中提供的值需要转换，则 WMI 提供程序会确定报表服务器数据库是位于同一计算机上还是远程计算机上。 为了确定该数据库是否安装在本地，WMI 提供程序会将 DatabaseServerName 属性与下面的值列表进行对比评估。 如果发现结果匹配，则数据库为本地数据库。 否则，为远程数据库。 比较不区分大小写。  
  
|DatabaseServerName 的值|示例|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 如果将*如果 iswindowsuser*设置为 `true` ，则 WMI 提供程序会调用 LookupAccountName 来获取该帐户的 SID，然后调用 LookupAccountSID 来获取要放入脚本中的名称 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 这样便可确保所使用的帐户名可通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 验证。  
  
 当*如果 iswindowsuser*设置为时 `false` ，生成的脚本将授予对 Report Server 数据库的**RSExec**角色、Report Server 临时数据库和 MSDB 数据库。  
  
 当*如果 iswindowsuser*设置为时 `false` ，中的 SQL Server 用户必须已经存在于上才能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 成功运行该脚本。  
  
 如果报表服务器没有指定的报表服务器数据库，调用 GrantRightsToDatabaseUser 将返回错误。  
  
 生成的脚本支持 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 和 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。  
  
## <a name="requirements"></a>要求  
 **命名空间：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [MSReportServer_ConfigurationSetting 成员](msreportserver-configurationsetting-members.md)  
  
  
