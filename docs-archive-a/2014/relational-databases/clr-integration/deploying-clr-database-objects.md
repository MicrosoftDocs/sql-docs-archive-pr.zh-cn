---
title: 部署 CLR 数据库对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
author: rothja
ms.author: jroth
ms.openlocfilehash: daf069bc37a58a879224b2217f4dcb700c1d6e99
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576819"
---
# <a name="deploying-clr-database-objects"></a>部署 CLR 数据库对象
  部署是分发要在其他计算机上安装并运行的已完成应用程序或模块的过程。 可以使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 开发公共语言运行时 (CLR) 数据库对象，并将这些对象部署到测试服务器。 或者，也可以使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 再分发文件替代 Visual Studio 对托管数据库对象进行编译。 编译完之后，可以使用 Visual Studio 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，将包含 CLR 数据库对象的程序集部署到测试服务器。 请注意，Visual Studio .NET 2003 无法用于 CLR 集成编程或部署。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含预先安装的 .NET Framework，而 Visual Studio .NET 2003 无法使用 .NET Framework 2.0 程序集。  
  
 在测试服务器上测试并验证了 CLR 方法后，便可以使用部署脚本将这些方法分发到生产服务器。 可以手动生成部署脚本，或使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 生成（请参阅本主题后面的过程）。  
  
 默认情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中关闭了 CLR 集成功能，必须启用该功能才能使用 CLR 程序集。 有关详细信息，请参阅 [Enabling CLR Integration](clr-integration-enabling.md)。  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>将程序集部署到测试服务器  
 可以使用 Visual Studio 开发 CLR 函数、过程、触发器、用户定义类型 (UDT) 或用户定义聚合 (UDA)，并将其部署到测试服务器。 也可以使用 .NET Framework 再分发文件附带的命令行编译器（如 csc.exe 和 vbc.exe）编译这些托管数据库对象。 开发 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 托管数据库对象不一定需要 Visual Studio 集成开发环境。  
  
 请务必确保解决所有编译器错误和警告。 随后，可以使用 Visual Studio 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语句，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 数据库中注册包含 CLR 例程的程序集。  
  
> [!NOTE]  
>  必须对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例启用 TCP/IP 网络协议，才能使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 进行远程开发、调试和开发。 有关在服务器上启用 TCP/IP 协议的详细信息，请参阅[配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)。  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>使用 Visual Studio 部署程序集  
  
1.  通过**Build** \<project name> 从 "**生成**" 菜单中选择 "生成" 来生成项目。  
  
2.  解决所有生成错误和警告，然后将程序集部署到测试服务器。  
  
3.  从 "**生成**" 菜单中选择 "**部署**"。 随后，将在 Visual Studio 中首次创建 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 项目时指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例和数据库中注册程序集。  
  
#### <a name="to-deploy-the-assembly-using-transact-sql"></a>使用 Transact-SQL 部署程序集  
  
1.  使用 .NET Framework 附带的命令行编译器编译源文件中的程序集。  
  
2.  对于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 源文件：  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  对于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 源文件：  
  
 `vbc /target:library C:\helloworld.vb`  
  
 以上命令使用 `/target` 选项启动 Visual C# 或 Visual Basic 编译器，以指定生成库 DLL。  
  
1.  解决所有生成错误和警告，然后将程序集部署到测试服务器。  
  
2.  在测试服务器上打开 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。 创建一个新查询，连接到合适的测试数据库（如 AdventureWorks）。  
  
3.  将如下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 添加到查询中，在服务器上创建程序集。  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  随后，必须在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例中创建过程、函数、聚合、用户定义类型或触发器。 如果 `HelloWorld` 程序集在 `HelloWorld` 类中包含名为 `Procedures` 的方法，则可以将如下 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 添加到查询中，以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中创建名为 `hello` 的过程。  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 有关在中创建不同类型的托管数据库对象的详细信息 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请参阅[Clr 用户定义函数](../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)、 [Clr 用户](../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)定义的聚合、 [Clr 用户定义类型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)、 [clr 存储过程](../../database-engine/dev-guide/clr-stored-procedures.md)和[clr 触发器](../../database-engine/dev-guide/clr-triggers.md)。  
  
## <a name="deploying-the-assembly-to-production-servers"></a>将程序集部署到生产服务器  
 在测试服务器上测试并验证了 CLR 数据库对象后，便可以将这些数据库对象分发到生产服务器。 有关调试托管数据库对象的详细信息，请参阅[调试 CLR 数据库对象](debugging-clr-database-objects.md)。  
  
 托管数据库对象的部署类似于常规数据库对象（如表、[!INCLUDE[tsql](../../../includes/tsql-md.md)] 例程等）。 可以使用部署脚本将包含 CLR 数据库对象的程序集部署到其他服务器。 部署脚本可以使用 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 的“生成脚本”功能生成。 部署脚本也可以手动生成，或使用“生成脚本”功能生成然后手动更改。 部署脚本生成之后，可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的其他实例上运行，以部署托管数据库对象。  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>使用“生成脚本”生成部署脚本  
  
1.  打开 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]，然后连接到注册要部署的托管程序集或数据库对象的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。  
  
2.  在**对象资源管理器**中，展开 **\<server name>** 和**数据库**树。 右键单击托管数据库对象所注册到的数据库，选择 "**任务**"，然后选择 "**生成脚本**"。 将打开脚本向导。  
  
3.  从列表框中选择数据库，然后单击 "**下一步**"。  
  
4.  在 "**选择脚本选项**" 窗格中，单击 "**下一步**"，或更改选项，然后单击 "**下一步**"。  
  
5.  在 "**选择对象类型**" 窗格中，选择要部署的数据库对象的类型。 单击“下一步”。  
  
6.  对于在 "**选择对象类型**" 窗格中选择的每个对象类型，将显示 " ** \<type> 选择**" 窗格。 在此窗格中，可以从在指定数据库中注册的该数据库对象类型的所有实例中进行选择。 选择一个或多个对象，然后单击 "**下一步**"。  
  
7.  选择了所有所需的数据库对象类型后，将出现 "**输出选项**" 窗格。 选择 "**将脚本保存到文件**" 并指定脚本的文件路径。 选择“下一步”。 查看您的选择，然后单击 "**完成**"。 部署脚本将保存到指定的文件路径。  
  
## <a name="post-deployment-scripts"></a>后期部署脚本  
 您可以运行后期部署脚本。  
  
 若要添加后期部署脚本，请在 Visual Studio 项目目录中添加一个名为 postdeployscript.sql 的文件。 例如，在**解决方案资源管理器**中右键单击项目，然后选择 "**添加现有项**"。 将文件添加到项目的根目录，而不是 TestScripts 文件夹中。  
  
 单击“部署”时，Visual Studio 将在项目部署完成之后运行此脚本。  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时 (CLR) 集成编程概念](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
