---
title: 卸载报表生成器 (报表生成器) 的独立版本 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cda13248d1aa14ee3d57a951872d3ad8ded17da9
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589441"
---
# <a name="uninstall-the-stand-alone-version-of-report-builder-report-builder"></a>卸载报表生成器的独立版本（报表生成器）
  可以从控制面板或命令行卸载报表生成器的独立版本。 在未卸载 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 的情况下，无法卸载报表生成器的 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 版本。  
  
 除了使用 /x 选项而不是 /i 选项外，从命令行卸载报表生成器所使用的语法与安装时使用的语法完全相同。 用于卸载的命令行也可包括 /quiet 选项和其他标准选项。 如果已删除报表生成器 Windows Installer 包 (ReportBuilder3_x86.msi)，则无法轻松地使用命令行卸载报表生成器。 若要了解有关如何能够通过使用报表生成器的 GUID 将其删除的详细信息，请参阅 msdn 库中 msiexec 程序的文档。  
  
 如果报表生成器使用的文件夹中包含自定义文件，则在删除报表生成器时会保留这些文件夹和文件。 仅删除报表生成器文件。  
  
### <a name="to-uninstall-report-builder-from-the-control-panel"></a>从控制面板卸载报表生成器  
  
1.  在 **“开始”** 菜单上，单击 **“控制面板”** 。  
  
2.  在“控制面板”中，单击 **“程序和功能”**。  
  
3.  在“名称”**** 列表中找到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 报表生成器并单击它。  
  
4.  单击“卸载”****。  
  
5.  如果提示需要确认卸载报表生成器，请单击 **“是”**。  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>从命令行卸载报表生成器  
  
1.  在 **“开始”** 菜单上，单击 **“运行”** 。  
  
2.  在 "**打开**" 文本框中，键入`cmd.`  
  
3.  在命令提示符窗口中，导航到包含 ReportBuilder3_x86.msi 的文件夹。  
  
4.  键入如下基本命令行：  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 如果要包括日志记录，请使用如下命令行：  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
1.  按 **Enter**。  
  
## <a name="see-also"></a>另请参阅  
 [安装、卸载和报表生成器支持](../install-uninstall-and-report-builder-support.md)   
 [安装报表生成器 &#40;报表生成器的独立版本&#41;](install-report-builder.md)  
  
  
