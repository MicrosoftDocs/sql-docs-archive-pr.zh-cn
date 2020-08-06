---
title: 调试存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4f5971fe611f06a413ca48b2bc91237a8c87ee8e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689655"
---
# <a name="debugging-stored-procedures"></a>调试存储过程
  实际上，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 存储过程是使用 C#（或任何其他 CLR 或 COM 语言）编写的 CLR 或 COM 库（通常为 DLL）。 因此，调试存储过程类似于在 Visual Studio 调试环境中调试任何其他应用程序。 您可以使用集成调试功能在 Visual Studio 开发环境中调试存储过程。 您可以使用这些功能执行下列操作：在过程位置停止、检查内存和注册值、更改变量、观察消息流量以及密切监视代码的运行状况。  
  
### <a name="to-debug-a-stored-procedure"></a>调试存储过程  
  
1.  在 Visual Studio 中打开用于创建 DLL 的项目。  
  
2.  使用要调试的过程相应的方法或函数创建断点。  
  
3.  使用 Visual Studio 创建存储过程 DLL 的调试版本。  
  
4.  将 DLL 部署到服务器中。 有关将 DLL 部署到服务器的详细信息，请参阅[创建存储过程](creating-stored-procedures.md)。  
  
5.  您需要一个调用要进行测试的存储过程的应用程序。 如果没有此类可用的应用程序，则可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 MDX 查询编辑器创建调用要进行测试的存储过程的 MDX 查询。  
  
6.  在 Visual Studio 中，附加到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 进程 (Msmdsrv.exe)。  
  
    1.  从 "**调试**" 菜单中，选择 "**附加 toProcess**"。  
  
    2.  在 "**附加 toProcess** " 对话框中，选择 "**显示所有用户的进程**"。  
  
    3.  在 "**可用进程**" 列表的 "**处理**" 列中，单击 " **Msmdsrv.exe**"。 如果服务器上运行多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，则需要通过要使用的实例的 ID 标识进程。  
  
    4.  在 "**附加到**" 文本框中，确保选择了适当的程序类型。 对于 CLR DLL，依次单击 "**选择**"、"**调试以下代码类型**" 和 "**托管**"，然后单击 **"确定"**。 对于 COM DLL，单击 "**选择**"，单击 "**调试以下代码类型**"，单击 "**本机**"，然后单击 **"确定"**。  
  
    5.  单击 **“附加”** 。  
  
7.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，调用程序或 MDX 脚本（用于调用存储过程）。 当调试程序到达包含断点的某行时，便会中断。 您可以在监视窗口中计算变量，查看局部变量并逐句检查代码。  
  
 如果在调试库时出现问题，则确保已将对应的程序数据库 (PDB) 文件复制到服务器中的部署位置。 如果在注册或部署过程中没有复制该文件，则必须手动将其复制到 DLL 所在的位置。 对于本机代码 (COM DLL)，PDB 文件驻留在 \debug 子目录中。 对于托管代码 (CLR DLL)，该文件驻留在 \WINDEBUG 子目录中。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型程序集管理](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [定义存储过程](defining-stored-procedures.md)  
  
  
