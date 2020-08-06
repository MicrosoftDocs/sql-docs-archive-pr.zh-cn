---
title: “生成和发布脚本向导”
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.generatescriptswizard.setscriptingoptions.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql12.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql12.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql12.swb.generatescriptswizard.summarypage.f1
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql12.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
- sql12.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql12.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql12.swb.generatescriptswizard.introduction.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql12.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.choosetables.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b3957db316648fd37da071ac155aad01b93c7cb
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590719"
---
# <a name="generate-and-publish-scripts-wizard"></a>“生成和发布脚本向导”
  你可以使用“生成和发布脚本向导”  创建脚本，以在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 的实例之间传输数据库。 您可以在本地网络中或从 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]为数据库引擎实例上的数据库生成脚本。 生成的脚本可以在数据库引擎或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的另一个实例上运行。 您还可以使用该向导将数据库的内容直接发布到使用 Database Publishing Services 创建的 Web 服务。 您可以为整个数据库创建脚本，或将其限制为特定的对象。  
  
1.  **开始之前：**  [发布到宿主服务](#PubHostSvc)， [权限](#Permissions)  
  
2.  **要生成或发布脚本，请使用：**  [生成和发布脚本向导](#GenPubScriptWiz)  
  
## <a name="before-you-begin"></a>开始之前  
 源和目标数据库可以位于 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或者运行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 或更新版本的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 实例上。  
  
###  <a name="publishing-to-a-hosted-service"></a><a name="PubHostSvc"></a> 发布到宿主服务  
 除了创建脚本之外， **“生成和发布脚本向导”** 还可用于将数据库发布到特定类型的宿主 SQL Server Web 服务。 SQL Server Hosting Toolkit 将 Database Publishing Services 作为 CodePlex 上的共享源项目提供。 Database Publishing Services 项目可由 Web 宿主提供程序用来生成一组 Web 服务，使其客户可以轻松地将数据库部署到 Web 服务。 有关下载 SQL Server Hosting Toolkit 的详细信息，请参阅 [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)（SQL Server 数据库发布服务）。  
  
 若要将一个数据库发布到 Web 宿主服务，请在该向导的 **“设置脚本编写选项”** 页上选择 **“发布到 Web 服务”** 。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 权限  
 发布数据库的最小权限是原始数据库上 db_ddladmin 固定数据库角色中的成员身份。 将数据库脚本发布到位于宿主提供程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的最小权限是目标数据库上 db_ddladmin 固定数据库角色中的成员身份。  
  
 用户还必须提供用户名和密码来访问他们的宿主提供程序帐户，才能使用该向导进行发布。 必须先在宿主提供程序中创建目标数据库，然后才能发布源数据库。 发布将覆盖该现有数据库中的对象。  
  
##  <a name="using-the-generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> 使用“生成和发布脚本向导”  
 **生成和发布脚本**  
  
1.  在 **对象资源管理器**中，展开包含要为其编写脚本的数据库的实例的节点。  
  
2.  指向 **“任务”**，然后单击 **“生成脚本”**。  
  
3.  完成向导对话框：  
  
    -   [“简介”页](#Introduction)  
  
    -   [“选择对象”页](#ChooseObjects)  
  
    -   [“设置脚本编写选项”页](#SetScriptOpt)  
  
    -   [“高级脚本编写选项”页](#AdvScriptOpt)  
  
    -   [“管理提供程序”页](#MgProviders)  
  
    -   [“高级发布选项”页](#AdvPubOpts)  
  
    -   [“提供程序配置”页](#ProvConfig)  
  
    -   [摘要页](#Summary)  
  
    -   [“保存或发布脚本”页](#SavePubScripts)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> “简介”页  
 本页介绍用于生成或发布脚本的步骤。  
  
 **不再显示此页** - 下次启动“生成和发布脚本向导”  时跳过此页。  
  
 “下一步 >”**** - 进入“选择方法”**** 页。  
  
 “取消”**** - 结束向导，而不从数据库中生成或发布脚本。  
  
###  <a name="choose-objects-page"></a><a name="ChooseObjects"></a> “选择对象”页  
 使用此页可选择要包含在该向导生成的脚本中的对象。 在以下向导页中，您可以选择将这些脚本保存到您选择的位置，或者使用它们将数据库对象和数据发布到安装了 [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)的远程 Web 宿主提供程序。  
  
 **编写整个数据库的脚本选项** - 单击此项可为数据库中的所有对象生成脚本并且为数据库本身包括一个脚本。  
  
 **选择特定数据库对象** - 单击此项可以将向导限制为仅对数据库中的所选特定对象生成脚本：  
  
-   **数据库对象** - 选择要在脚本中包含的至少一个对象。  
  
-   **全选** - 选中所有可用的复选框。  
  
-   **取消全选** - 清除所有复选框。 然后，您必须至少选择一个数据库对象才能继续。  
  
###  <a name="set-scripting-options-page"></a><a name="SetScriptOpt"></a> “设置脚本编写选项”页  
 使用此页可以指定您是否希望向导将脚本保存到您选择的位置或者是否要使用它们将数据库对象发布到远程 Web 宿主提供程序。 若要发布，您必须有权访问通过使用 Database Publishing Services Web 服务安装的 Web 服务。  
  
 **选项** - 如果您希望向导将脚本保存到您选择的位置，则选择 **“将脚本保存到特定位置”** 。 您以后可以对数据库引擎的实例或者对 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]运行这些脚本。 如果您希望向导将数据库对象发布到远程 Web 宿主提供程序，请选择 **“发布到 Web 服务”** 。  
  
 **将脚本保存到特定位置**-保存一个或多个。将 transact-sql 脚本文件保存到指定的位置。  
  
-   **高级** - 显示出 **“高级脚本编写选项”** 对话框，您可在其中选择用于生成脚本的高级选项。  
  
-   **保存到文件** - 将脚本保存到一个或多个 .sql 文件。 单击浏览 (…) 按钮可以指定文件的名称和位置****。 如果已存在同名的文件，请选中 **“覆盖现有文件”** 复选框以替换该文件。 单击 **“单个文件”** 或 **“每个对象一个文件”** 可以指定生成脚本的方式。 单击 **“Unicode 文本”** 或 **“ANSI 文本”** 可以指定应在脚本中使用的文本的类型。  
  
-   **保存到剪贴板** - 将 Transact-SQL 脚本保存到剪贴板。  
  
-   **保存到新建查询窗口** - 在“数据库引擎查询编辑器”窗口中生成脚本。 如果没有打开编辑器窗口，则将打开一个新的编辑器窗口作为脚本的目标。  
  
 **发布到 Web 服务** - 将您选择的对象发布到为其配置了提供程序的远程 Web 宿主服务。  
  
-   **管理提供程序** - 显示出 **“管理提供程序”** 对话框。 使用 **“管理提供程序”** 对话框可添加、编辑和删除宿主提供程序。 每个提供程序都指定与 Web 宿主服务的连接信息以及该服务上的目标数据库。  
  
-   **高级** - 显示出 **“高级发布选项”** 对话框，您可在其中选择用于发布脚本的高级选项。  
  
-   **提供程序** - 选择为托管要发布您所选对象的数据库的 Web 宿主服务指定连接信息的提供程序。 在 **“管理提供程序”** 对话框中必须具有至少一个提供程序，以便选择某一提供程序。  
  
-   **目标数据库** - 选择要发布您选择的对象的目标数据库。 您必须在选择目标数据库之前选择一个提供程序。  
  
###  <a name="advanced-scripting-options-page"></a><a name="AdvScriptOpt"></a> “高级脚本编写选项”页  
 使用此页可以指定希望此向导生成脚本的方式。 此页中提供有许多不同的选项。 如果在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] “数据库引擎类型” **中指定的 SQL Server 或**版本不支持这些选项，则这些选项将灰显。  
  
 **选项** - 通过从每个选项右侧的可用设置列表中选择一个值来指定高级选项。  
  
 **常规** - 以下选项将应用于整个脚本。  
  
-   **ANSI 填充**- `ANSI PADDING ON` 在脚本中包括。 默认值为 **True**。  
  
-   **追加到文件** - 值为 **True**时，此脚本将被添加到在 **“设置脚本编写选项”** 页上指定的现有脚本的底部。 值为 **False**时，新脚本将覆盖以前的脚本。 默认值为 **False**。  
  
-   **出错时继续编写脚本** - 值为 **True**时，将在出现错误时停止编写脚本。 值为 **False**时，将继续编写脚本。 默认值为 **False**。  
  
-   **将 UDDT 转换为基类型** - 值为 **True**时，用户定义数据类型 (UDDT) 被转换为用于创建它们的基本数据类型。 将运行脚本的数据库中不存在 UDDT 时，请使用 **True** 。 值为 **False**时，使用 UDDT。 默认值为 **False**。  
  
-   **生成依赖对象的脚本** - 为执行选定对象的脚本时必须存在的任何对象生成脚本。 默认值为 **True**。  
  
-   **包含说明性标头** - 值为 **True**时，说明性注释将被添加到脚本中，将脚本分成若干个部分，每个对象为一个部分。 默认值为 **False**。  
  
-   **包含 if NOT EXISTS** - 值为 **True**时，脚本包含一个用于检查对象在数据库中是否已经存在的语句，并在对象已经存在的情况下不尝试创建新对象。 默认值为 **False**。  
  
-   **包含系统约束名称**-当**为 False**时，在源数据库上自动命名的约束的默认值将在目标数据库上自动重新命名。 值为 **True**时，约束将在源数据库和目标数据库上具有相同名称。  
  
-   **包含不支持的语句** - 值为 **False**时，脚本不包含选定服务器版本或引擎类型上不支持的对象的语句。 值为 **True**时，脚本包含不支持的对象。 不支持的对象的每个语句都将具有一个注释，指出必须首先编辑语句，然后才能对所选 SQL Server 版本或引擎类型运行脚本。 默认值为 **False**。  
  
-   **架构限定对象名称** - 在创建的对象的名称中包括架构名称。 默认值为 **True**。  
  
-   **脚本绑定** - 为绑定默认值和规则对象生成脚本。 默认值为 **False**。 有关详细信息，请参阅 [CREATE DEFAULT (Transact SQL)](/sql/t-sql/statements/create-default-transact-sql) 和 [CREATE RULE (Transact-SQL)](/sql/t-sql/statements/create-rule-transact-sql)。  
  
-   “编写排序规则脚本”  - 在脚本中包括排序规则信息。 默认值为 **False**。 有关详细信息，请参阅 [排序规则和 Unicode 支持](../collations/collation-and-unicode-support.md)。  
  
-   **编写默认值脚本** - 在表列中包括用于设置默认值的默认对象。 默认值为 **True**。 有关详细信息，请参阅 [CREATE DEFAULT (Transact-SQL)](/sql/t-sql/statements/create-default-transact-sql)。  
  
-   “编写 DROP 和 CREATE 脚本”  - 值为“编写脚本”  时，将包括[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句以创建对象。 值为 **“编写 DROP 脚本”** 时，将包括 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句以删除对象。 值为 **“编写 DROP 和 CREATE 脚本”** 时，对于为其编写脚本的每个对象，脚本中将包括 [!INCLUDE[tsql](../../../includes/tsql-md.md)] DROP 语句，随后是 CREATE 语句。 默认值为 **“编写 CREATE 脚本”** 。  
  
-   **编写扩展属性脚本** - 如果对象具有扩展属性，则在脚本中包括扩展属性。 默认值为 **True**。  
  
-   **为引擎类型编写脚本** - 创建可在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 或 SQL Server 数据库引擎实例的选定类型上运行的脚本。 在脚本中不包括在指定类型上不支持的对象。 默认类型为源服务器的类型。  
  
-   **为服务器版本编写脚本** - 创建可在选定版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上运行的脚本。 无法为某一版本的早期版本编写该版本新增功能的脚本。 默认版本为源服务器的版本。  
  
-   **编写登录脚本** - 当要为其编写脚本的对象是数据库用户时，使用此选项可创建用户依赖的登录帐户。 默认值为 **False**。  
  
-   **编写对象级权限脚本** - 包括在数据库中的对象上设置权限的脚本。 默认值为 **False**。  
  
-   **脚本统计信息**-设置为 "**编写统计信息脚本**" 时，此选项包含 `CREATE STATISTICS` 用于对对象重新创建统计信息的语句。 **“编写统计信息和直方图脚本”** 选项还会创建直方图信息。 默认值为 **“不编写统计信息脚本”** 。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
-   **编写 USE DATABASE 脚本**-将 `USE DATABASE` 语句添加到脚本。 若要确保在正确的数据库中创建数据库对象，请包含 `USE DATABASE` 语句。 如果脚本应在其他数据库中使用，请选择**False**以忽略该 `USE DATABASE` 语句。 默认值为 **True**。 有关详细信息，请参阅 [USE (Transact-SQL)](/sql/t-sql/language-elements/use-transact-sql)。  
  
-   **要编写脚本的数据的类型** - 选择应编写脚本的内容：“仅限数据”  和/或“仅限架构”  。 默认值为 **“仅限架构”** 。  
  
 **表/视图选项** - 下列选项仅应用于表或视图的脚本。  
  
-   **编写更改跟踪的脚本** - 如果在源数据库或源数据库中的表上启用了“编写更改跟踪的脚本”选项，则编写更改跟踪的脚本。 默认值为 **False**。 有关详细信息，请参阅[关于更改跟踪 (SQL Server)](../track-changes/about-change-tracking-sql-server.md)。  
  
-   **编写 check 约束脚本**-将 `CHECK` 约束添加到脚本中。 默认值为 **True**。 `CHECK` 约束要求输入表中的数据满足某些指定的条件。 有关详细信息，请参阅 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)。  
  
-   “编写数据压缩选项的脚本”  - 如果在源数据库或源数据库中的表上配置了编写数据压缩选项的脚本选项，则编写数据压缩选项的脚本。 有关详细信息，请参阅 [Data Compression](../data-compression/data-compression.md)。 默认值为 **False**。  
  
-   **编写外键脚本** - 将外键添加到脚本中。 默认值为 **True**。 外键可指示和强制保持表间的关系。  
  
-   **编写全文检索脚本** - 编写创建全文检索的脚本。 默认值为 **False**。  
  
-   **编写索引脚本** - 编写创建索引的脚本。 默认值为 **True**。 索引有助于快速查找数据。  
  
-   **编写主键脚本** - 编写对表创建主键的脚本。 默认值为 **True**。 主键可唯一标识表的每一行。  
  
-   **编写触发器脚本** - 编写对表创建 DML 触发器的脚本。 默认值为 **False**。 DML 触发器是当数据库服务器中发生数据操作语言 (DML) 事件时要执行的操作。 有关详细信息，请参阅 [DML Triggers](../triggers/dml-triggers.md)。  
  
-   **编写唯一键脚本** - 编写对表创建唯一键的脚本。 唯一键可防止输入重复的数据。 默认值为 **True**。 有关详细信息，请参阅 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)。  
  
###  <a name="manage-providers-page"></a><a name="MgProviders"></a>管理提供程序页  
 使用此对话框可查看、添加、编辑、删除或测试宿主提供程序连接。 宿主提供程序为使用 CodePlex 上 SQL Server Hosting Toolkit 中的 Database Publishing Service 项目创建的 Web 服务指定连接信息。  
  
 **已配置的提供程序** - 列出已保存的每个宿主提供程序的名称和 **Web** 服务地址。  
  
 **新建** - 打开 **“新提供程序的提供程序配置”** 对话框以添加新的宿主提供程序。  
  
 **编辑** - 打开相应的 **“提供程序配置”** 对话框以编辑现有的宿主提供程序。  
  
 **删除** - 删除选定的宿主提供程序。  
  
 **测试** - 使用选定提供程序中的信息测试与宿主服务的连接。  
  
 **确定** - 保存您在 **“宿主提供程序”** 对话框中做的所有更改。  
  
 **取消** - 撤消您在 **“宿主提供程序”** 对话框中做的所有更改。  
  
###  <a name="advanced-publishing-options-page"></a><a name="AdvPubOpts"></a>"高级发布选项" 页  
 使用此页可指定您希望该向导发布数据库的方式。 此页中提供有许多不同的选项。 如果在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] “数据库引擎类型” **中指定的 SQL Server 或**版本不支持这些选项，则这些选项将灰显。  
  
 **选项** - 通过从每个选项右侧的可用设置列表中选择一个值来指定高级选项。  
  
 **常规** - 以下选项将应用于整个发布。  
  
1.  **将 UDDT 转换为基类型** - 值为 **True**时，用户定义数据类型 (UDDT) 被转换为用于创建它们的基本数据类型。 将运行脚本的数据库中不存在 UDDT 时，请使用 **True** 。 值为 **False**时，使用 UDDT。 默认值为 **False**。  
  
2.  **发布排序规则** - 包括表列的排序规则信息。 默认值为 **False**。 有关详细信息，请参阅 [排序规则和 Unicode 支持](../collations/collation-and-unicode-support.md)。  
  
3.  **发布默认值** - 在表列中包括用于设置默认值的默认对象。 默认值为 **True**。 有关详细信息，请参阅 [CREATE DEFAULT (Transact-SQL)](/sql/t-sql/statements/create-default-transact-sql)。  
  
4.  “发布依赖对象”**** - 发布在执行所选对象的脚本时必须存在的任何对象。 默认值为 **True**。  
  
5.  **发布扩展属性** - 如果对象具有扩展属性，则在发送到提供程序以供发布的脚本中包含扩展属性。 默认值为 **True**。  
  
6.  **为服务器版本发布** - 创建发送到远程提供程序的脚本，以便采用可在所选版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上运行的方式进行发布。 无法为某一版本的早期版本编写该版本新增功能的脚本。 默认版本为源服务器的版本。  
  
7.  **发布对象级权限** - 包括数据库中的选定对象上的权限。 默认值为 **False**。  
  
8.  **发布统计信息**-设置为 "**发布统计信息**" 时，将包含 `CREATE STATISTICS` 语句以重新创建有关对象的统计信息。 **“发布统计信息和直方图”** 选项还会创建直方图信息。 默认值为 **“不发布统计信息脚本”**。 有关详细信息，请参阅 [CREATE STATISTICS (Transact-SQL)](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
9. **发布 vardecimal 选项**-在 `vardecimal` 源数据库表上启用目标数据库表时对其启用表格式。 默认值为 **True**。  
  
10. **架构限定对象名称** - 在创建的对象的名称中包括架构名称。 默认值为 **True**。  
  
11. **脚本绑定** - 在发送到提供程序以供发布的脚本中包括默认值和规则对象。 默认值为 **True**。 有关详细信息，请参阅 [CREATE DEFAULT (Transact SQL)](/sql/t-sql/statements/create-default-transact-sql) 和 [CREATE RULE (Transact-SQL)](/sql/t-sql/statements/create-rule-transact-sql)。  
  
12. “要发布的数据的类型”**** - 选择应对其编写脚本的目标：“仅限数据”****、“仅限架构”**** 或同时针对这两者。 默认值为 **“架构和数据”**。  
  
 **发布选项** - 指定是否在发布到 Web 主机提供商时使用事务。  
  
1.  **使用事务进行发布** - 在发布到远程 Web 宿主提供程序时使用事务。 如果目标数据库无法完成发布，则这些事务将被回滚。 默认值为 **True**。  
  
 **表/视图选项** - 以下选项仅应用于表或视图。  
  
1.  **发布 check 约束**-在 `CHECK` 发布过程中包括创建约束。 默认值为 **True**。 `CHECK` 约束要求输入表中的数据满足某些指定的条件。 有关详细信息，请参阅 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)。  
  
2.  **发布外键** - 在发布过程中包括创建外键。 默认值为 **True**。 外键可指示和强制保持表间的关系。 有关详细信息，请参阅 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md)。  
  
3.  **发布全文检索** - 编写创建全文检索的脚本。 默认值为 **False**。  
  
4.  **发布索引** - 在发布过程中包括表上的索引。 默认值为 **True**。 索引有助于快速查找数据。  
  
5.  **发布主键** - 在发布过程中包括创建主键。 默认值为 **True**。 主键可唯一标识表的每一行。 有关详细信息，请参阅 [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md)。  
  
6.  **发布触发器** - 在发布过程中包括创建 DML 触发器。 默认值为 **True**。 DML 触发器是当数据库服务器中发生数据操作语言 (DML) 事件时要执行的操作。 有关详细信息，请参阅 [DML Triggers](../triggers/dml-triggers.md)。  
  
7.  **发布唯一键** - 在发布过程中包括创建表的唯一键。 唯一键可防止输入重复的数据。 默认值为 **True**。 有关详细信息，请参阅 [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md)。  
  
8.  **发布更改跟踪** - 如果在源数据库或源数据库中的表上启用了“发布更改跟踪”选项，则在发布过程中包括更改跟踪。 默认值为 **False**。 有关详细信息，请参阅[关于更改跟踪 (SQL Server)](../track-changes/about-change-tracking-sql-server.md)。  
  
9. “发布数据压缩选项”**** - 如果在源数据库或源数据库中的表上配置了发布数据压缩选项，则在发布过程中包括数据压缩选项。 默认值为 **True**。 有关详细信息，请参阅 [Data Compression](../data-compression/data-compression.md)。  
  
###  <a name="provider-configuration-page"></a><a name="ProvConfig"></a>"提供程序配置" 页  
 使用此对话框可以查看或修改宿主提供程序设置。 可以使用此对话框执行以下操作：  
  
-   查看、添加或编辑宿主提供程序的连接信息。  
  
-   查看、添加、编辑或删除用于提供程序连接的数据库。  
  
-   自动配置宿主提供程序的数据库。  
  
 宿主提供程序为使用 CodePlex 上 SQL Server Hosting Toolkit 中的 Database Publishing Service 项目创建的 Web 服务指定连接信息。  
  
 **名称** - 宿主提供程序的名称。  
  
 **Web 服务地址** - 宿主服务的 HTTPS 地址。  
  
 **Web 服务身份验证** - 登录宿主服务所需的用户名和密码。  
  
 **保存密码** - 进行加密，并将密码保存在本地计算机上。  
  
 “可用数据库”**** - 为宿主提供程序配置的数据库以升序列出，格式为： *server_name*。*database_name*.  
  
 **新建** - 打开 **“数据库”** 配置对话框，然后添加一个新的数据库。  
  
 **编辑** - 打开所选数据库的 **“数据库”** 配置对话框。  
  
 **删除** - 删除选定的数据库。  
  
 **设置为默认值** - 选择数据库作为默认值。  
  
 **确定** - 保存在此对话框中做的所有更改并返回到向导。  
  
 **取消** - 撤消在此对话框中做的所有更改并返回到向导。  
  
###  <a name="summary-page"></a><a name="Summary"></a> 摘要页  
 此页汇总了您在此向导中所选的选项。 若要更改某个选项，请单击 **“上一步”**。 若要开始生成将保存或发布的脚本，请单击 **“下一步”**。  
  
 **检查所做选择** - 显示您在向导的每一页中所做的选择。 展开某个节点可看到在相应页中选择的选项。  
  
###  <a name="save-or-publish-scripts-page"></a><a name="SavePubScripts"></a> “保存或发布脚本”页  
 使用此页可以在向导出现时监视其进度。  
  
 **详细信息** - 查看 **“操作”** 列可以看到向导的进度。 在生成脚本后，向导将根据您的选择将脚本保存到某一文件或者使用它们发布到某一 Web 服务。 在上述各步骤完成后，单击 **“结果”** 列中的值可以看到相应步骤的结果。  
  
 **保存报告** - 单击此项可将向导的进度结果保存到文件中。  
  
 **取消** - 单击此项可在完成处理前或出错时关闭向导。  
  
 “完成”**** - 单击此项可在完成处理后或出错时关闭向导。  
  
## <a name="see-also"></a>另请参阅  
 [安装 SMO](../server-management-objects-smo/installing-smo.md)   
 [将数据库复制到其他服务器](../databases/copy-databases-to-other-servers.md)  
  
  
