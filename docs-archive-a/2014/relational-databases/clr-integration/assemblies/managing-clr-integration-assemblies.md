---
title: 管理 CLR 集成程序集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: 191ccd73ca42ef4c26291e6de88f5f2b0cf565ef
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691236"
---
# <a name="managing-clr-integration-assemblies"></a>管理 CLR 集成程序集
  托管代码在被编译后部署在称作程序集的单元中。 程序集将打包为 DLL 或可执行 (.exe) 文件。 尽管可执行文件可以自动运行，但 DLL 必须在现有应用程序中承载。 托管的 DLL 程序集可以加载到中并由其承载 [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 CREATE ASSEMBLY 语句的数据库，然后才能将其加载到进程中并使用它。 还可以使用 ALTER ASSEMBLY 语句从更新的版本更新程序集，或者使用 DROP ASSEMBLY 语句从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中删除程序集。  
  
 程序集信息存储在安装了程序集的数据库的 `sys.assembly_files` 表中。 `sys.assembly_files` 表包含以下列。  
  
|列|说明|  
|------------|-----------------|  
|assembly_id|为程序集定义的标识符。 此编号分配到与同一程序集相关的所有对象。|  
|name|对象的名称。|  
|file_id|标识每个对象的编号，对于与给定的 `assembly_id` 关联的第一个对象，该值为 1。 如果有多个对象与同一个 `assembly_id` 关联，则后续的每个对象的 `file_id` 值依次递增 1。|  
|内容|程序集或文件的十六进制表示形式。|  
  
## <a name="in-this-section"></a>本节内容  
 [创建程序集](creating-an-assembly.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建 SAFE、EXTERNAL_ACCESS 和 UNSAFE CLR 程序集。  
  
 [改变程序集](altering-an-assembly.md)  
 介绍如何在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中更新 CLR 程序集。  
  
 [删除程序集](dropping-an-assembly.md)  
 介绍如何从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中删除 CLR 程序集。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../security/clr-integration-security.md)   
 [CLR 集成代码访问安全性](../security/clr-integration-code-access-security.md)  
  
  
