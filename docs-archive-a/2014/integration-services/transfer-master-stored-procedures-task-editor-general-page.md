---
title: 传输主存储过程任务编辑器 (常规页) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.general.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: fa1abd4c-e2be-427f-be53-860e49c97227
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a25a5c9c6ed3802e21ac522e94163ce5fb9e8c0
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690716"
---
# <a name="transfer-master-stored-procedures-task-editor-general-page"></a>传输主存储过程任务编辑器（“常规”页）
  可以使用 **“传输主存储过程任务编辑器”** 对话框的 **“常规”** 页，对传输主存储过程任务进行命名和说明。 有关此任务的详细信息，请参阅 [Transfer Master Stored Procedures Task](control-flow/transfer-master-stored-procedures-task.md)。  
  
> [!NOTE]  
>  此任务只将 **dbo** 拥有的用户定义存储过程从源服务器上的 **master** 数据库传递到目标服务器上的 **master** 数据库。 若要在目标服务器上创建存储过程，必须在目标服务器上的 **master** 数据库中授予用户 CREATE PROCEDURE 权限，或者用户必须为目标服务器上 **sysadmin** 固定服务器角色的成员。  
  
## <a name="options"></a>选项  
 **名称**  
 为传输主存储过程任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入传输主存储过程任务的说明。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [传输主存储过程任务编辑器 &#40;"存储过程" 页&#41;](../../2014/integration-services/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)   
 [“表达式”页](expressions/expressions-page.md)  
  
  
