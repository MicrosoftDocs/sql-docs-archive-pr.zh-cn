---
title: LocalDBCreateInstance 函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBCreateInstance
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 3eebb485-8a53-4a79-82a9-57b8de9f8e84
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ff822c552176ad8c083a1c8ea6c0f2430f72972f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589108"
---
# <a name="localdbcreateinstance-function"></a>LocalDBCreateInstance 函数
  创建新的 SQL Server Express LocalDB 实例。  
  
 **头文件：** sqlncli.msi  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT LocalDBCreateInstance(  
           PCWSTR wszVersion,  
           PCWSTR pInstanceName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>参数  
 *wszVersion*  
 [输入] LocalDB 版本，例如 11.0 或 11.0.1094.2。  
  
 *pInstanceName*  
 [输入] 要创建的 LocalDB 实例的名称。  
  
 dwFlags**  
 [输入] 保留供将来使用。 当前应设置为 0。  
  
## <a name="returns"></a>返回  
 S_OK  
 函数成功。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 计算机上没有安装 SQL Server Express LocalDB。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 一个或多个指定的输入参数无效。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定的实例名称无效。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 应在其中存储该实例的路径的长度超过 MAX_PATH。  
  
 [LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION](../express-localdb-error-messages/localdb-error-instance-exists-with-lower-version.md)  
 指定的实例已存在，但其版本低于请求的版本。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定的版本不可用。  
  
 [LOCALDB_ERROR_VERSION_REQUESTED_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-version-requested-not-installed.md)  
 没有安装指定的修补程序级别。  
  
 [LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-create-instance-folder.md)  
 不能在 %userprofile% 下创建文件夹。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 无法检索用户配置文件的文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 无法访问实例文件夹。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 无法访问实例注册表。  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 无法修改实例注册表。  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 SQL Server 进程已启动，但 SQL Server 启动失败。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 实例配置已损坏。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 发生了意外错误。 有关详细信息，请参阅事件日志。  
  
## <a name="remarks"></a>备注  
 如果 LocalDB 实例完全正常运行，指定的名称已存在并且其版本等于或高于所请求的版本，则结果为 S_OK。  
  
 在现有实例损坏的情况下，对 `LocalDBCreateInstance` API 方法的后续调用将失败。 必须手动修复损坏的实例或显式删除它们，然后才能再次使用。  
  
 有关使用 LocalDB API 的代码示例，请参阅[SQL Server Express LocalDB 引用](../sql-server-express-localdb-reference.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Express LocalDB 标头信息和版本信息](sql-server-express-localdb-header-and-version-information.md)  
  
  
