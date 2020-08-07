---
title: SQL Server Express LocalDB 参考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 25b71829-bdb1-46f4-ac36-80ddced52f3d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6996a37f5e36577743ae4286d36c16f74690890a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587750"
---
# <a name="sql-server-express-localdb-reference"></a><span data-ttu-id="69f99-102">SQL Server Express LocalDB 参考</span><span class="sxs-lookup"><span data-stu-id="69f99-102">SQL Server Express LocalDB Reference</span></span>
  <span data-ttu-id="69f99-103">本节包含有关 SQL Server Express LocalDB 的信息：</span><span class="sxs-lookup"><span data-stu-id="69f99-103">This section contains information about the SQL Server Express LocalDB:</span></span>  
  
-   [<span data-ttu-id="69f99-104">SQL Server Express LocalDB 错误消息参考</span><span class="sxs-lookup"><span data-stu-id="69f99-104">SQL Server Express LocalDB Error Message Reference</span></span>](express-localdb-error-messages/sql-server-express-localdb-reference-error-messages.md)  
  
-   [<span data-ttu-id="69f99-105">SQL Server Express LocalDB 实例 API 参考</span><span class="sxs-lookup"><span data-stu-id="69f99-105">SQL Server Express LocalDB Instance API Reference</span></span>](express-localdb-instance-apis/sql-server-express-localdb-reference-instance-apis.md)  
  
## <a name="code-sample"></a><span data-ttu-id="69f99-106">代码示例</span><span class="sxs-lookup"><span data-stu-id="69f99-106">Code Sample</span></span>  
 <span data-ttu-id="69f99-107">以下示例演示了 LocalDB API。</span><span class="sxs-lookup"><span data-stu-id="69f99-107">The following sample demonstrates the LocalDB API.</span></span>  <span data-ttu-id="69f99-108">在运行此示例之前，请确保 LocalDB 安装在计算机上。</span><span class="sxs-lookup"><span data-stu-id="69f99-108">Make sure that LocalDB is installed on the computer before running this sample.</span></span>  <span data-ttu-id="69f99-109">可以从 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express 的安装程序中安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="69f99-109">You can install LocalDB from setup in the [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express.</span></span>  
  
```  
// compile with: Advapi32.lib  
#include <SDKDDKVer.h>  
#include <stdio.h>  
  
// To use LocalDB API, you must define LOCALDB_DEFINE_PROXY_FUNCTIONS before you include sqlncli.h in one (and only one) of the   
// source files in your program. LOCALDB_DEFINE_PROXY_FUNCTIONS causes code to be generated that binds to the LocalDB API at runtime.  
  
#define LOCALDB_DEFINE_PROXY_FUNCTIONS  
#include "sqlncli.h"  
  
HRESULT CreateAndStartLocalDBInstance(PWCHAR wszVersion, PWCHAR wszInstanceName) {  
   HRESULT hr;  
  
   if (SUCCEEDED(hr = LocalDBCreateInstance(wszVersion, wszInstanceName, 0)))  
      hr = LocalDBStartInstance(wszInstanceName, 0, NULL, NULL);  
  
   return hr;  
}  
  
HRESULT StopAndDeleteLocalDBInstance(PWCHAR wszInstanceName) {  
   HRESULT hr;  
  
   if (SUCCEEDED(hr = LocalDBStopInstance(wszInstanceName, 0, 30)))   // 30 seconds timeout   
      hr = LocalDBDeleteInstance(wszInstanceName, 0);  
  
   return hr;  
}  
  
void PrintLocalDBError(HRESULT hr) {  
   HRESULT hrError;  
   WCHAR wszMessage[1024];  
   DWORD dwMessage = 1024;  
  
   if (hr == LOCALDB_ERROR_NOT_INSTALLED)  
      wprintf(L"Local DB is not installed.\n");  
  
   else if (hr == LOCALDB_ERROR_CANNOT_LOAD_RESOURCES)  
      wprintf(L"Cannot load resources for Local DB API DLL. Local DB installation is corrupted.\n");  
  
   else if (FAILED(hrError = LocalDBFormatMessage(hr, 0, 0, wszMessage, &dwMessage)))  
      wprintf(L"Cannot format an error message for a Local DB error code: %#x. LocalDBFormatMessage returned: %#x\n", hr, hrError);  
  
   else  
      wprintf(L"%s\n", wszMessage);  
}  
  
HRESULT PrintLocalDBInstances() {  
   HRESULT hr;  
   DWORD dwNumberOfInstances = 0;  
  
   if (FAILED(hr = LocalDBGetInstances(NULL, &dwNumberOfInstances)))  
      if (hr != LOCALDB_ERROR_INSUFFICIENT_BUFFER)  
         return hr;  
  
   PTLocalDBInstanceName localDBInstnces = (PTLocalDBInstanceName) malloc(dwNumberOfInstances * sizeof(TLocalDBInstanceName));  
   if (localDBInstnces == NULL) {  
      return HRESULT_FROM_WIN32(ERROR_OUTOFMEMORY);  
   }  
  
   if (FAILED(hr = LocalDBGetInstances(localDBInstnces, &dwNumberOfInstances))) {  
      free(localDBInstnces);  
      return hr;  
   }  
  
   for (DWORD i = 0; i < dwNumberOfInstances; i++) {  
      LocalDBInstanceInfo localDBInstanceInfo;  
  
      if (FAILED(hr = LocalDBGetInstanceInfo(localDBInstnces[i], &localDBInstanceInfo, sizeof(localDBInstanceInfo)))) {  
         free(localDBInstnces);  
         return hr;  
      }  
  
      wprintf(L"Name: %s State: %s Version: %u.%u.%u.%u\n",  
         localDBInstnces[i],   
         localDBInstanceInfo.bIsRunning ? L"running" : L"stopped",  
         localDBInstanceInfo.dwMajor,  
         localDBInstanceInfo.dwMinor,  
         localDBInstanceInfo.dwBuild,  
         localDBInstanceInfo.dwRevision);  
   }  
  
   free(localDBInstnces);  
   return S_OK;  
}  
  
int main() {  
   HRESULT hr;  
  
   WCHAR wszInstanceName[] = L"Contoso";  
   WCHAR wszVersion[] = L"11.0";  
  
   if (FAILED(hr = CreateAndStartLocalDBInstance(wszVersion, wszInstanceName)))  
      PrintLocalDBError(hr);  
  
   PrintLocalDBInstances();  
  
   if (FAILED(hr = StopAndDeleteLocalDBInstance(wszInstanceName)))  
      PrintLocalDBError(hr);  
  
   PrintLocalDBInstances();  
}  
```  
  
  