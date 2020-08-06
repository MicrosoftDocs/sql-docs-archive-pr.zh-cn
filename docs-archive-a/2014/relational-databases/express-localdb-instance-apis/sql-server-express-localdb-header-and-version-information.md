---
title: SQL Server Express LocalDB 标头和版本信息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_location:
- sqluserinstance.dll
ms.assetid: 506b5161-b902-4894-b87b-9192d7b1664a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 138081852cf505b03265fd9c5f39eae6ed2af39b
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590822"
---
# <a name="sql-server-express-localdb-header-and-version-information"></a>SQL Server Express LocalDB 标头信息和版本信息
  没有用于 SQL Server Express LocalDB 实例 API 的单独头文件；LocalDB 函数签名和错误代码在 SQL Server Native Client 头文件 (sqlncli.h) 中定义。 若要使用 LocalDB 实例 API，必须在项目中包含 sqlncli.h 头文件。  
  
## <a name="localdb-versioning"></a>LocalDB 版本  
 对于每个主要 SQL Server 版本，LocalDB 安装将使用单组二进制代码。 这些 LocalDB 版本独立进行维护和修补。 这意味着，用户必须指定他或她将使用的 LocalDB 基准版本（也即主 SQL Server 版本）。 版本是使用 .NET Framework **system.web**类定义的标准版本格式指定的：  
  
 *主要. 次要 [. 生成 [. 修订]]*  
  
 版本字符串中的前两个数字 (*主要*和*次要*) 是必需的。 版本字符串中的最后两个数字 (*生成*和*修订*) 是可选的，如果用户将其省略，则默认为零。这意味着，如果用户仅指定 "12.2" 作为 LocalDB 版本号，则会将其视为用户指定了 "12.2.0.0"。  
  
 LocalDB 安装的版本在 SQL Server 实例注册表项下的 MSSQLServer\CurrentVersion 注册表项中定义，例如：  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12E.LOCALDB\ MSSQLServer\CurrentVersion: "CurrentVersion"="12.0.2531.0"  
```  
  
 并行支持同一工作站上的多个 LocalDB 版本。 但是，用户代码始终使用本地计算机上的最新可用的**Sqluserinstance.dll** DLL 连接到 LocalDB 实例。  
  
## <a name="locating-the-sqluserinstance-dll"></a>查找 SQLUserInstance DLL  
 若要查找**Sqluserinstance.dll** DLL，客户端提供程序使用以下注册表项：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions]  
```  
  
 在此注册表项之下有一个项列表，每个项对应于计算机上安装的每个 LocalDB。 其中每个键都命名为带有格式的 LocalDB 版本号 *\<major-version>* 。*\<minor-version>* 例如， (的密钥名为 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 12.0) 。 在每个版本项之下都有一个 `InstanceAPIPath` 名称-值对，用于定义指向随该版本一起安装的 SQLUserInstance.dll 文件的完全路径。 下面的示例显示一个安装了 LocalDB 版本 11.0 和 12.0 的计算机的注册表项：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
```  
  
 客户端提供程序必须在所有已安装的版本中找到最新版本，并从关联的值加载**Sqluserinstance.dll** DLL 文件 `InstanceAPIPath` 。  
  
### <a name="wow64-mode-on-64-bit-windows"></a>64 位 Windows 上的 WOW64 模式  
 64 位 LocalDB 安装将有一组附加注册表项，以允许在 Windows 64 位上的 Windows 32 位 (WOW64) 模式下运行的 32 位应用程序使用 LocalDB。 具体而言，在 64 位 Windows 上，LocalDB MSI 将创建以下注册表项：  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Wow6432Node\Microsoft SQL Server Local DB\Installed Versions\12.0]  
"InstanceAPIPath"="C:\\Program Files (x86)\\Microsoft SQL Server\\120\\LocalDB\\Binn\\SqlUserInstance.dll"]  
  
```  
  
 64位程序读取 `Installed Versions` 密钥将显示指向**sqluserinstance.dll** DLL 的64位版本的值，而32位程序 (在 WOW64 模式下的64位 Windows 上运行) 将自动重定向到 `Installed Versions` hive 下的某个注册表项 `Wow6432Node` 。 此项包含指向**Sqluserinstance.dll** DLL 32 位版本的值。  
  
## <a name="using-localdb_define_proxy_functions"></a>使用 LOCALDB_DEFINE_PROXY_FUNCTIONS  
 LocalDB 实例 API 定义了一个名为 LOCALDB_DEFINE_PROXY_FUNCTIONS 的常量，该常量可自动发现和加载**Sqluserinstance.dll** DLL。  
  
 该常量启用的代码部分为每个 LocalDB API 提供代理的实现。 代理实现使用公用函数绑定到最新安装的**Sqluserinstance.dll** DLL 中的入口点，然后转发请求。  
  
 只有在包含 sqlncli.h 之前，在用户代码中定义常量 LOCALDB_DEFINE_PROXY_FUNCTION 时，才启用代理函数。 只应在一个源模块（.cpp 文件）中定义常量，因为该常量为所有 API 入口点定义外部函数名称。 它为每个 LocalDB API 提供代理的实现。  
  
 下面的代码示例演示如何使用本机 C++ 代码中的宏：  
  
```  
// Define the LOCALDB_DEFINE_PROXY_FUNCTIONS constant to enable the LocalDB proxy functions   
// The #define has to take place BEFORE the API header file (sqlncli.h) is included  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include <sqlncli.h>  
...  
HRESULT hr = S_OK;  
  
// Create LocalDB instance by calling the create API proxy function included by macro  
if (FAILED(hr = LocalDBCreateInstance( L"12.0", L"name", 0)))  
{  
...  
}  
...  
  
```  
  
  
