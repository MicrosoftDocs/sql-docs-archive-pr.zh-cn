---
title: 安装和卸载 OData 源组件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fad0a86c6226f408b0495569d0a853dd7340aeca
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87586889"
---
# <a name="install-and-uninstall-odata-source-component"></a>安装和卸载 OData 源组件
  本主题提供有关在计算机上安装或删除 OData 源组件的说明。  
  
## <a name="installation"></a>安装  
 OData 源组件要求在计算机上安装以下必备组件。  
  
-   SQL Server Data Tools（用于设计包）  
  
-   SQL Server Integration Services（用于在 Visual Studio 外部运行包）  
  
 若要安装 OData 源组件，请下载[SQL Server 2014 功能包](https://go.microsoft.com/fwlink/p/?LinkId=391999)，并运行以下 MSI 文件之一。  
  
-   用于 64 位平台的 ODataSourceForSQLServer2014-amd64.msi  
  
-   用于 32 位平台的 ODataSourceForSQLServer2014-x86.msi  
  
> [!IMPORTANT]  
>  64 位安装程序将同时安装 32 位和 64 位版本的 OData 源组件。 如果使用 32 位操作系统，则只需运行 32 位安装程序。  
  
## <a name="uninstallation"></a>卸载  
 可以通过 "**程序和功能**" 菜单卸载 OData 源组件。 ** (x64) 项查找 MICROSOFT SQL SERVER SSIS OData 源组件**，并单击 "**卸载**"。  
  
  
