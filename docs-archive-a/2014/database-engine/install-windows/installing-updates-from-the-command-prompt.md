---
title: 从命令提示符安装更新 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d3ced6cd72bfc972743d0f9d8c7c2a9ce57dfdd1
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87578387"
---
# <a name="installing-updates-from-the-command-prompt"></a>从命令提示符安装更新
  请根据您所在单位的需要测试并修改安装脚本。  
  
## <a name="sample-syntax-for-installation"></a>安装的示例语法  
 更新包的名称可能会有变化，可能包含语言、版本和处理器组件。 在命令提示符下应用更新，从而将 <package_name> 替换为更新包的名称：  
  
-   更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的单个实例和所有共享组件（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具）：您可以通过使用 InstanceName 参数或 InstanceID 参数指定实例。 若要更新的已准备实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，必须指定 InstanceID 参数<package_name # C1.exe/Qs/IAcceptSQLServerLicenseTerms/Action = Patch/InstanceName = MyInstance 或 <package_name # C3.exe/Qs/IAcceptSQLServerLicenseTerms/Action = patch/InstanceID = \<Instance ID> 。  
  
-   安装程序可以将最新的产品更新与主安装相集成，以便可以同时安装主产品及其适用的更新。 您可以准备数据库引擎实例的安装以包含产品更新： setup.exe/q/IAcceptSQLServerLicenseTerms/ACTION = PrepareImage/UpdateEnabled = True/UpdateEnabled = True/UpdateSource = \<path where the update is downloaded> /INSTANCEID =/FEATURES \<Instance ID> = SQLEngine。  
  
-   仅更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享组件（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具）：<更新包名称>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
  
-   更新计算机上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和所有共享组件（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具）：<更新包名称>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances。  
  
 在命令提示符下删除更新，将 <更新包名称> 替换为更新包的名称：  
  
-   从单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和所有共享组件（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具）删除更新：<包名称>.exe /qs /Action=RemovePatch /InstanceName=MyInstance。  
  
-   仅从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享组件（如 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和管理工具）删除更新：<包名称>.exe /qs /Action=RemovePatch  
  
    > [!NOTE]  
    >  更新安装程序可以确保共享组件始终采用不低于最高级别的实例版本。  
  
## <a name="supported-command-prompt-parameters"></a>支持的命令提示符参数  
  
> [!IMPORTANT]  
>  请尽可能在运行时提供安全凭据。 如果必须将凭据存储在脚本文件中，请确保该文件的安全以防受到未经授权的访问。  
  
|开关|说明|  
|------------|-----------------|  
|**/?**|显示无人参与安装命令提示符帮助|  
|**/action=Patch 或 /action=RemovePatch**|指定安装操作：Patch 或 RemovePatch。|  
|**/allinstances**|将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新应用于所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以及所有不识别实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享组件。|  
|**/instancename = instancename** <sup>1</sup>|将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新应用于名为 InstanceName 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以及所有不识别实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享组件。|  
|**/InstanceID=Inst1**|将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新应用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 实例，以及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共享组件和不识别实例的组件。|  
|**/quiet**|在无人参与模式下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新安装程序。|  
|**/qs**|仅显示进度 UI 对话。|  
|**/UpdateEnabled**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序是否应发现和加入产品更新。 有效值为 True 和 False 或 1 和 0。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将包含找到的更新。|  
|**/IAcceptSQLServerLicenseTerms**|仅在为无人参与安装指定了 /Q 或 /QS 参数时是必需的。|  
  
 <sup>1</sup>不能指定此参数来将更新应用到已准备的实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 必须指定 /instanceID 参数。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 服务安装概述](../../sql-server/install/overview-of-sql-server-servicing-installation.md)  
  
  
