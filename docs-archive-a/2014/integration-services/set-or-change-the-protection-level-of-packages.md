---
title: 设置或更改包的保护级别 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services],security
- security [Integration Services],protection levels
- protection level for packages [Integration Services]
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
author: chugugrace
ms.author: chugu
ms.openlocfilehash: da8e63028498097b4321e4ef1383fbc8aa5845b6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87693401"
---
# <a name="set-or-change-the-protection-level-of-packages"></a>设置或更改包的保护级别
  若要控制对包内容以及其中包含的敏感值（如密码）的访问，请设置 `ProtectionLevel` 属性的值。 项目中所含的包需要具有与项目相同的保护级别才能生成项目。 如果更改项目的 `ProtectionLevel` 属性设置，需要为包手动更新该属性设置。  
  
 有关如何在 `ProtectionLevel` 包生命周期中的不同阶段确定适用于你的包的设置的信息，请参阅[对包中敏感数据的访问控制](security/access-control-for-sensitive-data-in-packages.md)。 有关 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中安全功能的概述，请参阅[安全性概述 (Integration Services)](security/security-overview-integration-services.md)。  
  
 本主题中的过程介绍如何使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 dtutil 命令提示实用工具来更改 `ProtectionLevel` 属性。  
  
> [!NOTE]  
>  除了本主题中的过程外，当导入或导出包时，您通常可以设置或更改包的 `ProtectionLevel` 属性。 当使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 导入和导出向导保存包时，您也可以更改包的 `ProtectionLevel` 属性。  
  
### <a name="to-set-or-change-the-protection-level-of-a-package-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中设置或更改包的保护级别  
  
1.  `ProtectionLevel`在主题中查看属性的可用值，[设置包的保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定包的适当值。  
  
2.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含该包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包。  
  
4.  如果“属性”窗口未显示包的属性，请单击设计图面。  
  
5.  在属性窗口的 "**安全**" 组中，为属性选择适当的值 `ProtectionLevel` 。  
  
     如果选择的保护级别需要密码，请输入密码作为 **PackagePassword** 属性的值。  
  
6.  在 **“文件”** 菜单上，选择 **“保存选定项”** 以保存修改的包。  
  
### <a name="to-set-or-change-the-protection-level-of-packages-at-the-command-prompt"></a>在命令提示符下设置或更改包的保护级别  
  
1.  `ProtectionLevel`在主题中查看属性的可用值，[设置包的保护级别](security/access-control-for-sensitive-data-in-packages.md)，并确定包的适当值。  
  
2.  `Encrypt`在主题[dtutil 实用工具](dtutil-utility.md)中查看选项的映射，然后确定要用作所选属性的值的相应整数 `ProtectionLevel` 。  
  
3.  打开命令提示符窗口。  
  
4.  在命令提示符下，导航到您要为其设置 `ProtectionLevel` 属性的包所在的文件夹。  
  
     下面步骤中所示的语法示例假设此文件夹是当前文件夹。  
  
5.  使用与下列示例之一相类似的命令，设置或更改包的保护级别。  
  
    -   下面的命令将文件系统中的单个包的 `ProtectionLevel` 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   下面的命令将文件系统中特定文件夹内所有包的 `ProtectionLevel` 属性设置为级别 2“使用密码加密敏感数据”，密码为“strongpassword”：  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         如果您在批文件中使用类似的命令，则请输入文件占位符“%f”作为批文件中的“%%f”。  
  
## <a name="see-also"></a>另请参阅  
 [dtutil 实用工具](dtutil-utility.md)  
  
  
