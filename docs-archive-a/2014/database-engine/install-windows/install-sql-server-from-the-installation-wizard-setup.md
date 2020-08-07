---
title: 从安装向导安装 SQL Server 2014 (安装) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04667831ab26423ed896ee3f9029d3189d741c7a
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87576972"
---
# <a name="install-sql-server-2014-from-the-installation-wizard-setup"></a>使用安装向导安装 SQL Server 2014（安装程序）
  本主题提供了使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序的安装向导来安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新实例的分步过程。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导提供了一个用于安装所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的功能树，这样您就不必分别安装这些组件了。 有关可安装的各种组件的详细信息，请参阅[安装 2014 SQL Server](installation-for-sql-server.md)。  有关如何分别安装组件的详细信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，请参阅[install SQL Server 2014](install-sql-server.md)。  
  
 以下附加主题介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他安装方法：  
  
-   [从命令提示符安装 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
-   [使用配置文件安装 SQL Server 2014](install-sql-server-using-a-configuration-file.md)  
  
-   [使用 SysPrep 安装 SQL Server 2014](install-sql-server-using-sysprep.md)  
  
-   [&#40;安装&#41;创建新的 SQL Server 故障转移群集](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)。  
  
-   [使用安装向导 &#40;安装&#41;升级到 SQL Server 2014 ](upgrade-sql-server-using-the-installation-wizard-setup.md)。  
  
## <a name="prerequisites"></a>必备条件  
 安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请查阅 [计划 SQL Server 安装](../../sql-server/install/planning-a-sql-server-installation.md)中的主题。  
  
> [!NOTE]  
>  对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
  
### <a name="to-install-sscurrent"></a>安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质， 然后双击根文件夹中的 Setup.exe。 若要从网络共享进行安装，请找到共享中的根文件夹，然后双击 Setup.exe。  
  
2.  安装向导将运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装中心。 若要创建新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，请单击左侧导航区域中的“安装”****，然后单击“全新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 独立安装或向现有安装添加功能”****。  
  
3.  在“产品密钥”页上，选择某个选项以指示您是安装免费版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，还是安装具有 PID 密钥的产品的生产版本。 有关详细信息，请参阅[SQL Server 2014 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
     若要继续，请单击 **“下一步”** 。  
  
4.  在“许可条款”页上查看许可协议，如果同意，请选中 **“我接受许可条款”** 复选框，然后单击 **“下一步”** 。 为了帮助改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您还可以启用功能使用情况选项并将报告发送给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在“全局规则”窗口中，如果没有规则错误，安装过程将自动前进到“产品更新”窗口。  
  
6.  如果未在“控制面板”\“所有控制面板项”\“Windows 更新”\“更改设置”中选中“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”复选框，则接下来将显示“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页。 在“ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新”页中选中选项会将计算机设置更改为在您浏览 Windows 更新时包括最新更新。  
  
7.  在“产品更新”页中，将显示最近提供的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品更新。 如果未发现任何产品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将不会显示该页并且自动前进到 **“安装安装程序文件”** 页。  
  
8.  在“安装安装程序文件”页上，安装程序将提供下载、提取和安装这些安装程序文件的进度。 如果找到了针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的更新，并且指定了包括该更新，则也将安装该更新。  
  
9. 在 “设置角色” 页上，选择 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能安装”** ，然后单击 **“下一步”** 以继续进入 “功能选择” 页。  
  
10. 在“功能选择”页上，选择要安装的组件。 选择功能名称后， **“功能说明”** 窗格中会显示每个组件组的说明。 您可以选中任意一些复选框。 有关详细信息，请参阅[SQL Server 2014 的版本和组件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[SQL Server 2014 各个版本支持的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
     **“所选功能的必备组件”** 窗格中将显示所选功能的必备组件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将在本过程后面所述的安装步骤中安装尚未安装的必备组件。  
  
     您还可以使用“功能选择”页底部的字段为共享组件指定自定义目录。 若要更改共享组件的安装路径，请更新该对话框底部字段中的路径，或单击 **“浏览”** 移动到另一个安装目录。 默认安装路径为 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]。  
  
     为共享组件指定的路径必须是绝对路径。 文件夹不能压缩或加密。 不支持映射的驱动器。  
  
     如果正在 64 位操作系统上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您将看到以下选项：  
  
    1.  共享功能目录  
  
    2.  共享功能目录 (x86)  
  
     为以上每个选项指定的路径必须不同。  
  
11. 如果所有规则均通过验证，则“功能规则”窗口将自动前进。  
  
12. 在“实例配置”页上指定是安装默认实例还是命名实例。 有关详细信息，请参阅 [Instance Configuration](../../sql-server/install/instance-configuration.md)。  
  
     **实例 ID** - 默认情况下，实例名称用作实例 ID。 这用于标识 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的安装目录和注册表项。 默认实例和命名实例都是如此。 对于默认实例，实例名称和实例 ID 为 MSSQLSERVER。 若要使用非默认的实例 ID，请为“实例 ID” **** 文本框指定一个不同值。  
  
    > [!NOTE]  
    >  典型的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]独立实例（无论是默认实例还是命名实例）不会对“实例 ID” **** 使用非默认值。  
  
     所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升级都将应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的每个组件。  
  
     **已安装的实例** - 该网格显示安装程序正在其中运行的计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 如果计算机上已经安装了一个默认实例，则必须安装 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的命名实例。  
  
     安装程序中的其余工作流取决于您指定要安装的功能。 您可能不会看到所有的页面，具体取决于您进行的选择。  
  
13. 使用“服务器配置 - 服务帐户”页指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的登录帐户。 此页上配置的实际服务取决于您选择安装的功能。  
  
     您可以为所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务分配相同的登录帐户，也可以单独配置各个服务帐户。 您还可以指定是自动启动、手动启动还是禁用服务。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议您逐个配置服务帐户，以便为每项服务提供最低权限，其中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务将被授予完成其任务所必须具备的最低权限。 有关详细信息，请参阅 [服务器配置 - 服务帐户](../../sql-server/install/server-configuration-service-accounts.md) 和 [配置 Windows 服务帐户和权限](../configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     若要为此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例中的所有服务帐户指定同一个登录帐户，请在该页底部的字段中提供凭据。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     使用“服务器配置 - 排序规则”页为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定非默认排序规则。 有关详细信息，请参阅[服务器配置 - 排序规则](../../sql-server/install/server-configuration-collation.md)。  
  
14. 使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - 服务器配置”页指定以下各项：  
  
    -   安全模式 - 为您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例选择 Windows 身份验证或混合模式身份验证。 如果选择“混合模式身份验证”，则必须为内置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员帐户提供一个强密码。  
  
         在设备与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成功建立连接之后，用于 Windows 身份验证和混合模式身份验证的安全机制是相同的。 有关详细信息，请参阅[数据库引擎配置-帐户设置](../../sql-server/install/database-engine-configuration-account-provisioning.md)。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理员 - 必须为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例至少指定一个系统管理员。 若要添加用以运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序的帐户，请单击 **“添加当前用户”** 。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”** ，然后编辑将拥有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的管理员特权的用户、组或计算机的列表。  
  
     使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - 数据目录”页指定非默认的安装目录。 若要安装到默认目录，请单击 **“下一步”** 。  
  
    > [!IMPORTANT]  
    >  如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 此外，将附带数据目录的 SQL Server 安装在驱动器的根文件夹或装入点上将失败。 有关详细信息，请查看[安装的卷 SQL Server 支持。](https://support.microsoft.com/kb/819546/en-us)  
  
     有关详细信息，请参阅 [数据库引擎配置 - 数据目录](../../sql-server/install/database-engine-configuration-data-directories.md)。  
  
     使用“ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置 - FILESTREAM”页对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例启用 FILESTREAM。 有关详细信息，请参阅 [数据库引擎配置 - 文件流](../../sql-server/install/database-engine-configuration-filestream.md)。  
  
15. 使用“[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置 - 帐户设置”页指定服务器模式以及将拥有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的管理员权限的用户或帐户。 服务器模式决定哪些内存和存储子系统用于服务器。 不同的解决方案类型在不同的服务器模式下运行。 如果您计划在服务器上运行多维数据集数据库，则选择默认选项“多维”和“数据挖掘”服务器模式。 对于管理员权限，您必须为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定至少一个系统管理员。 若要添加当前正在运行 SQL Server 安装程序的帐户，请单击 **“添加当前用户”** 按钮。 若要向系统管理员列表中添加帐户或从中删除帐户，请单击 **“添加”** 或 **“删除”** ，然后编辑将拥有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的管理员特权的用户、组或计算机的列表。 有关服务器模式和管理员权限的详细信息，请参阅 [Analysis Services 配置-帐户设置](../../sql-server/install/analysis-services-configuration-account-provisioning.md)。  
  
     完成对该列表的编辑后，请单击 **“确定”** 。 验证配置对话框中的管理员列表。 完成此列表后，请单击 **“下一步”** 。  
  
     使用“ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 配置 - 数据目录”页指定非默认的安装目录。 若要安装到默认目录，请单击 **“下一步”** 。  
  
    > [!IMPORTANT]  
    >  如果指定非默认的安装目录，请确保安装文件夹对于此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例是唯一的。 此对话框中的任何目录都不应与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的目录共享。 此外，将附带数据目录的 SQL Server 安装在驱动器的根文件夹或装入点上将失败。 有关详细信息，请查看[安装的卷 SQL Server 支持。](https://support.microsoft.com/kb/819546/en-us)  
  
     有关详细信息，请参阅 [Analysis Services 配置 - 数据目录](../../sql-server/install/analysis-services-configuration-data-directories.md)。  
  
16. 使用“ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置”页指定要创建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装类型。 有关 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置模式和选项的详细信息，请参阅 [Reporting Services 配置选项 (SSRS)](../../sql-server/install/reporting-services-configuration-options-ssrs.md)。  
  
     选择了选项后，单击 **“下一步”** 继续。  
  
17. 使用“Distributed Replay 控制器配置”页可以指定您希望向其授予针对 Distributed Replay 控制器服务的管理权限的用户。 具有管理权限的用户将可以不受限制地访问 Distributed Replay 控制器服务。  
  
     单击 **“添加当前用户”** 按钮可以添加要向其授予针对 Distributed Replay 控制器服务的访问权限的用户。 单击 **“添加”** 按钮可以添加针对 Distributed Replay 控制器服务的访问权限。 单击 **“删除”** 按钮可以从 Distributed Replay 控制器服务中删除访问权限。  
  
     若要继续，请单击 **“下一步”** 。  
  
18. 使用“ Distributed Replay 客户端配置”页可以指定您希望向其授予针对 Distributed Replay 客户端服务的管理权限的用户。 具有管理权限的用户将可以不受限制地访问 Distributed Replay 客户端服务。  
  
     “控制器名称”是一个可选参数，并且默认值为 \<*blank*>。 输入客户端计算机将与 Distributed Replay 客户端服务进行通信的控制器的名称。 注意以下事项：  
  
    -   如果您已经设置了一个控制器，则在配置每个客户端时输入该控制器的名称。  
  
    -   如果您尚未设置控制器，则可以将控制器名称保留为空白。 但是，您必须在 **“客户端配置”** 文件中手动输入控制器名称。  
  
     为 Distributed Replay 客户端服务指定 **“工作目录”** 。 默认工作目录为 \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\。  
  
     为 Distributed Replay 客户端服务指定 **“结果目录”** 。 默认结果目录为 \<*drive letter*>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\。  
  
     若要继续，请单击 **“下一步”** 。  
  
19. “准备安装”页将显示安装期间指定的安装选项的树状视图。 在此页上，安装程序指示是启用还是禁用产品更新功能以及最终的更新版本。  
  
     若要继续，请单击 **“安装”** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将首先安装所选功能的必备组件，然后安装所选功能。  
  
20. 在安装过程中，“安装进度”页会提供相应的状态，因此您可以在安装过程中监视安装进度。  
  
21. 安装完成后，“完成”页会提供指向安装摘要日志文件以及其他重要说明的链接。 若要完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程，请单击 **“关闭”** 。  
  
22. 如果安装程序指示您重新启动计算机，请立即重新启动。 安装完成后，请务必阅读来自安装向导的消息。 有关详细信息，请参阅 [查看和读取 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="next-steps"></a>后续步骤  
 配置新安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 为了减少系统的可攻击外围应用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有选择地安装和启用了一些关键服务和功能。 有关详细信息，请参阅 [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [验证 SQL Server 安装](validate-a-sql-server-installation.md)   
 [删除 SQL Server 2014 安装](repair-a-failed-sql-server-installation.md)   
 [查看和读取 SQL Server 安装程序日志文件](view-and-read-sql-server-setup-log-files.md)   
 [使用安装向导 &#40;安装程序升级到 SQL Server 2014&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](install-sql-server-from-the-command-prompt.md)  
  
  
