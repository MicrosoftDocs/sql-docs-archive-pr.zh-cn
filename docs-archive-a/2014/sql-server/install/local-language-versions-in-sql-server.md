---
title: SQL Server 中的本地语言版本 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 646ffaed1e4b709c2c26030379f0a7f223f221e6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688439"
---
# <a name="local-language-versions-in-sql-server"></a>SQL Server 中的本地语言版本
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 Windows 操作系统所支持的所有语言。  
  
## <a name="cross-language-support"></a>跨语言支持  
  
-   所有操作系统的本地化版本均支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 英文版。  
  
-   通过使用 Windows 多语言用户界面包 (MUI) 设置，具有相应语言的已本地化的操作系统或者支持的操作系统的英文版本支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本。 有关详细信息，请参阅 [Configure Operating System to Support Localized Versions](../../../2014/sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本只能升级到同一语言的本地化版本，并且不能升级到英文版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本也可以与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的英文实例并行安装。  
  
##  <a name="configure-operating-system-to-support-localized-versions"></a><a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 在支持的操作系统的英文版上，通过使用 Windows 多语言用户界面包 (MUI) 设置，支持使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本。  
  
 不过，在运行英语版操作系统（具有非英文 MUI 设置）的服务器上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地化版本之前，必须先验证某些操作系统设置。 需要验证下列操作系统设置是否匹配要安装的本地化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的语言：  
  
-   操作系统用户界面设置  
  
-   操作系统用户区域设置  
  
-   系统区域设置  
  
 如果这些设置与要安装的本地化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的语言不匹配，请使用下列过程正确设置这些操作系统设置。  
  
> [!CAUTION]  
>  不支持在同一台计算机上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的不同语言版本。  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>更改操作系统用户界面设置  
  
1.  安装与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地化版本匹配的操作系统 MUI（如果尚未安装）。  
  
2.  在 Control Panel 中，打开 **Regional and Language Options**。  
  
3.  在 **Languages** 选项卡上，从列表中为 **Language used in menus and dialogs**选择一个值。  
  
     此设置将影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的用户界面语言，所以它必须与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地化版本匹配。  
  
4.  单击 **Apply** 确认更改，然后单击 **OK** 关闭窗口。  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>更改操作系统用户区域设置  
  
1.  安装与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地化版本匹配的操作系统 MUI（如果尚未安装）。  
  
2.  在 Control Panel 中，打开 **Regional and Language Options**。  
  
3.  在 **Regional Options** 选项卡上，从列表中为 **Select an item to match its preferences**选择一个值。  
  
     此设置将影响特定于区域性的数据格式。  
  
4.  单击 **Apply** 确认更改，然后单击 **OK** 关闭窗口。  
  
#### <a name="to-change-the-system-locale-setting"></a>更改系统区域设置  
  
1.  安装与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的本地化版本匹配的操作系统 MUI（如果尚未安装）。  
  
2.  在 Control Panel 中，打开 **Regional and Language Options**。  
  
3.  在“高级”  选项卡上，从列表中为“选择一种语言来匹配要使用的非 Unicode 程序的语言版本”  选择一个值。  
  
     此设置将使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序可以为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装选择最佳默认排序规则。  
  
4.  单击 **Apply** 确认更改，然后单击 **OK** 关闭窗口。  
  
## <a name="see-also"></a>另请参阅  
 [安装 SQL Server 2014 的硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md)   
 [安装 SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
  
  
