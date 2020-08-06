---
title: 在表格模式下安装 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
ms.openlocfilehash: a677fd7770f646067cafb8fedf6d3705ccf2de3c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87688327"
---
# <a name="install-analysis-services-in-tabular-mode"></a>在表格模式下安装 Analysis Services
  如果您要安装 Analysis Services 以便使用新增的表格建模功能，则必须在支持这种模型的服务器模式下安装 Analysis Services。 服务器是表格模式，在安装过程中配置。  
  
 在这种模式下安装了服务器后，可以用它来承载在表格模型设计器中构建的解决方案。 如果您想通过网络来访问表格模型数据，则需要表格模式服务器。  
  
 可在安装向导或命令行安装程序中指定表格模式。 以下部分介绍了各种方法。  
  
## <a name="installation-wizard"></a>安装向导  
 下面的列表显示了 SQL Server 安装向导中的哪些页用来在表格模式下安装 Analysis Services：  
  
1.  从安装程序的功能树中选择 **“Analysis Services”** 。  
  
     ![设置显示 Analsyis Services 的功能树](../../../sql-server/install/media/ssas-setupas.gif "设置显示 Analsyis Services 的功能树")  
  
2.  在 "Analysis Services 配置" 页上，确保选择 "**表格模式**"。  
  
     ![包含 Analysis Services 配置选项的“设置”页](../../../sql-server/install/media/ssas-setupasconfig.gif "包含 Analysis Services 配置选项的“设置”页")  
  
 表格模式使用 xVelocity 内存中分析引擎 (VertiPaq)，该引擎是部署到 Analysis Services 的表格模型的默认存储器。 将表格模型解决方案部署到服务器之后，可以有选择性地配置表格解决方案，以便将 DirectQuery 磁盘存储作为受内存限制的存储的替代项。  
  
## <a name="command-line-setup"></a>命令行安装程序  
 SQL Server 安装程序包含一个用来指定服务器模式的新参数 (`ASSERVERMODE`)。 下面的示例说明了用来在表格服务器模式下安装 Analysis Services 的命令行安装程序。  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` 必须少于 17 个字符。  
  
 所有占位符帐户的值必须替换为有效的帐户和密码。  
  
 未使用提供的示例命令行语法安装工具（例如 SQL Server Management Studio 或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]）。 有关添加功能的详细信息，请参阅[从命令提示符安装 SQL Server 2014](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)。  
  
 `ASSERVERMODE` 区分大小写。  所有值必须以大写形式表示。 下表对 `ASSERVERMODE` 的有效值进行了说明。  
  
|值|说明|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|这是默认值。 如果不设置 `ASSERVERMODE`，则服务器将在多维服务器模式下安装。|  
|POWERPIVOT|此值是可选的。 实际上，如果设置 `ROLE` 参数，服务器模式就会自动设置为 1，从而使得 `ASSERVERMODE` 成为 PowerPivot for SharePoint 安装的可选项。 有关详细信息，请参阅[从命令提示符安装 PowerPivot](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md)。|  
|TABULAR|如果是在使用命令行安装程序在表格模式下安装 Analysis Services，则此值是必需的。|  
  
## <a name="see-also"></a>另请参阅  
 [确定 Analysis Services 实例的服务器模式](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [为表格模型数据库配置内存中或 DirectQuery 访问](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [&#40;SSAS 表格&#41;的表格建模](../../tabular-models/tabular-models-ssas.md)  
  
  
