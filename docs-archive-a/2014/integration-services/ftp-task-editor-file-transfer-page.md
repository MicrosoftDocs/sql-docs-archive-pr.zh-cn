---
title: FTP 任务编辑器 (文件传输页面) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8094051e93c4165be6ae186bde394f9271d60669
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579640"
---
# <a name="ftp-task-editor-file-transfer-page"></a>FTP 任务编辑器（“文件传输”页）
  可以使用 **“FTP 任务编辑器”** 对话框的 **“文件传输”** 页配置任务执行的 FTP 操作。  
  
 若要了解此任务，请参阅 [FTP 任务](control-flow/ftp-task.md)。  
  
## <a name="options"></a>选项  
 **IsRemotePathVariable**  
 指示远程路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|值|说明|  
|-----------|-----------------|  
|**True**|目标路径存储在变量中。 选择该值将显示动态选项 **RemoteVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择该值将显示动态选项 **RemotePath**。|  
  
 **OverwriteFileAtDestination**  
 指定是否可以覆盖目标位置中的文件。  
  
 **IsLocalPathVariable**  
 指示本地路径是否存储在变量中。 此属性具有下表所列的选项。  
  
|值|说明|  
|-----------|-----------------|  
|**True**|目标路径存储在变量中。 选择该值将显示动态选项 **LocalVariable**。|  
|**False**|目标路径在文件连接管理器中指定。 选择该值将显示动态选项 **LocalPath**。|  
  
 **操作**  
 选择要执行的 FTP 操作。 此属性具有下表所列的选项。  
  
|值|说明|  
|-----------|-----------------|  
|**发送文件**|发送文件。 选择此值将显示动态选项 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**接收文件**|接收文件。 选择此值将显示动态选项 **LocalVariable**、 **LocalPathRemoteVariable** 和 **RemotePath**。|  
|**创建本地目录**|创建本地目录。 选择此值将显示动态选项 **LocalVariable** 和 **LocalPath**。|  
|**创建远程目录**|创建远程目录。 选择此值将显示动态选项 **RemoteVariable** 和 **RemotelPath**。|  
|**删除本地目录**|删除本地目录。 选择此值将显示动态选项 **LocalVariable** 和 **LocalPath**。|  
|**删除远程目录**|删除远程目录。 选择此值将显示动态选项 **RemoteVariable** 和 **RemotePath**。|  
|**删除本地文件**|删除本地文件。 选择此值将显示动态选项 **LocalVariable** 和 **LocalPath**。|  
|**删除远程文件**|删除远程文件。 选择此值将显示动态选项 **RemoteVariable** 和 **RemotePath**。|  
  
 **IsTransferASCII**  
 指示是否应以 ASCII 模式传输从远程 FTP 服务器传输来的文件和传输到远程 FTP 服务器上的文件。  
  
## <a name="isremotepathvariable-dynamic-options"></a>IsRemotePathVariable 动态选项  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 选择用户定义的现有变量，或单击“\<**New variable...**>”以创建用户定义变量。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、添加变量  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 选择现有 FTP 连接管理器，或单击“\<**New connection...**>”以创建连接管理器。  
  
 **相关主题：** [FTP 连接管理器](connection-manager/ftp-connection-manager.md)、[FTP 连接管理器编辑器](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>IsLocalPathVariable 动态选项  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 选择用户定义的现有变量，或单击“\<**New variable...**>”以创建变量。  
  
 **相关主题：** [Integration Services &#40;SSIS&#41; 变量](integration-services-ssis-variables.md)、添加变量  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 选择现有“文件连接管理器”，或单击“\<**New connection...**>创建一个连接管理器。  
  
 **相关主题**： [Flat File Connection Manager](connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [FTP 任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
