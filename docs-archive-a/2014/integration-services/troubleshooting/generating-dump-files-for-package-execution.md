---
title: 生成包执行的转储文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 61e511aaff6c3c77338211537a685f8a1dc82981
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576877"
---
# <a name="generating-dump-files-for-package-execution"></a>生成包执行的转储文件
  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，可以创建提供包执行信息的调试转储文件。 这些文件中的信息有助于解决包执行问题。  
  
> [!NOTE]  
>  调试转储文件可能包含敏感信息。 为了帮助保护敏感信息，可以使用访问控制列表 (ACL) 来限制对这些文件的访问，或将这些文件复制到具有受限访问权限的文件夹中。 例如，在将调试文件发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支持服务部门之前，建议您删除所有敏感信息或机密信息。  
  
 将项目部署到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器时，可以创建转储文件，该文件提供有关此项目中所含包的执行情况的信息。 ISServerExec.exe 进程结束时，创建这些转储文件。 您可以通过在 **“执行包”** 对话框中选择 **“出错时转储”** 选项，指定在执行包期间出错时创建转储文件。 还可以使用以下存储过程：  
  
-   [catalog.set_execution_parameter_value（SSISDB 数据库）](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
     调用此存储过程以配置在执行包期间出现任意错误或事件时创建转储文件，以及出现特定事件时创建转储文件。  
  
-   [catalog.create_execution_dump](/sql/integration-services/system-stored-procedures/catalog-create-execution-dump)  
  
     调用此存储过程以暂停正在运行的包并创建转储文件。  
  
 如果你正在使用包部署模型部署包，则可以使用 **dtexec** 实用工具或 **dtutil** 实用工具在命令行下指定调试转储选项，来创建调试转储文件。 有关详细信息，请参阅 [dtexec Utility](../packages/dtexec-utility.md) 和 [dtutil Utility](../dtutil-utility.md)。 有关包部署模型的详细信息，请参阅[部署项目和包](../packages/deploy-integration-services-ssis-projects-and-packages.md)以及[包部署 &#40;SSIS&#41;](../packages/legacy-package-deployment-ssis.md)。  
  
## <a name="debug-dump-file-format"></a>调试转储文件格式  
 指定调试转储选项时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建下列调试转储文件：  
  
-   .mdmp 调试转储文件。 这是一个二进制文件。  
  
-   .tmp 调试转储文件。 这是一个文本格式文件。  
  
 默认情况下，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 将这些文件存储在 \<drive>:\Program Files\Microsoft SQL Server\110\Shared\ErrorDumps 文件夹中。  
  
 下表仅介绍 .tmp 文件中的某些部分。 .tmp 文件还包含该表中未列出的其他数据。  
  
|信息类型|说明|示例|  
|-------------------------|-----------------|-------------|  
|环境|操作系统版本、内存使用情况数据、进程 ID 和进程映像名称。 环境信息位于 .tmp 文件的开头。|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory:58% in use. Physical:845M/2044M  Paging:2404M/4095M (avail/total)|  
|动态链接库 (DLL) 路径和版本|系统在处理包的过程中加载的各 DLL 的路径和版本号。|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module:C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module:C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|最近的消息|系统最近发出的消息。 包括每条消息的时间、类型、说明和线程 ID。|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp:2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID:2368           (ThreadID)<br /><br /> [E:3]         Event Name:OnError                        (EventName)<br /><br /> [E:3]         Source Name:              (SourceName)<br /><br /> [E:3]         Source ID:                      (SourceID)<br /><br /> [E:3]         Execution ID:               (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description:该组件不存在、未注册、不可升级或缺少所需接口。 此组件的联系人信息为“”。|  
  
## <a name="related-content"></a>相关内容  
 [“执行包”对话框](../execute-package-dialog-box.md)  
  
  
