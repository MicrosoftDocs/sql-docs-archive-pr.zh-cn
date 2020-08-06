---
title: 在控制流中添加或删除任务或容器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8338a4143358d732a974287e587f482dc5c36a22
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87587557"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>在控制流中添加或删除任务或容器
  在控制流设计器中工作时， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中的工具箱会列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 为在包中生成控制流而提供的任务。 有关这些工具箱的详细信息，请参阅 [SSIS Toolbox](../ssis-toolbox.md)。  
  
 包可以包含同一任务的多个实例。 任务的每个实例在包中都唯一标识，因此可以分别配置每个实例。  
  
 如果删除任务，则将该任务连接到控制流中其他任务和容器的优先约束也将被删除。  
  
 下面的过程介绍如何在包的控制流中添加或删除任务或容器。  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>将任务或容器添加到控制流  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“控制流”** 选项卡。  
  
4.  若要打开 **“工具箱”** ，请单击 **“查看”** 菜单上的 **“工具箱”** 。  
  
5.  展开 **“控制流项”** 和 **“维护任务”** 。  
  
6.  将任务和容器从 **“工具箱”** 拖动到 **“控制流”** 选项卡的设计图面。  
  
7.  将任务或容器的连接线拖动到控制流中的另一组件，从而连接包控制流内的任务或容器。  
  
8.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>从控制流删除任务或容器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。 执行下列操作之一：  
  
    -   单击“控制流”  选项卡，右键单击要删除的任务或容器，然后单击“删除”  。  
  
    -   打开 **包资源管理器**。 在“可执行文件”  文件夹上，右键单击要删除的任务或容器，然后单击“删除”  。  
  
3.  若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 任务](integration-services-tasks.md)   
 [Integration Services 容器](integration-services-containers.md)   
 [控制流](control-flow.md)  
  
  
