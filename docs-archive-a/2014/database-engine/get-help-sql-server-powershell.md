---
title: 获取 SQL Server PowerShell 帮助 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: f1d97a3b694eebb924f9e1ff228d4d38da4f45ec
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87690039"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  有关使用 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序和 cmdlet 的信息有多个来源， 这包括 Windows PowerShell 环境中提供的帮助。  
  
## <a name="before-you-begin"></a>开始之前  
 若要了解有关 Windows PowerShell 的信息，请参阅 [Windows PowerShell 入门指南](https://technet.microsoft.com/library/hh857337.aspx)。  
  
 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet 和提供程序的概述，请参阅 [SQL Server PowerShell](../powershell/sql-server-powershell.md)。  
  
### <a name="help-in-the-windows-powershell-environment"></a>Windows PowerShell 环境中的帮助  
 使用 **Get-Help** cmdlet 可在 Windows PowerShell 环境中获得帮助。 **Get-Help** 为 Windows PowerShell 语言以及 Windows PowerShell 中的各种 cmdlet 和提供程序提供基本帮助。  
  
 有关使用 **Get-Help**的方式的详细信息，请参阅 [Get-Help：获取帮助](https://go.microsoft.com/fwlink/?LinkId=102136)。  
  
### <a name="sql-server-powershell-provider-help"></a>SQL Server PowerShell 提供程序帮助  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供程序实现 SQLSERVER 虚拟驱动器上的若干文件夹，例如 SQLSERVER:\SQL 和 SQLSERVER:\DAC 文件夹。 每个文件夹都与一个 SQL Server 可管理性对象模型相关联。 虽然您可以列出与 SQL Server 路径中的每个节点关联的方法和属性，便不能在 PowerShell 环境中获取它们的帮助。 有关带有指向关联的编程参考的文件夹的表，请参阅 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)。  
  
### <a name="invoke-sqlcmd-help"></a>Invoke-Sqlcmd 帮助  
 **Invoke-Sqlcmd** cmdlet 将可由 **sqlcmd** 实用工具运行的查询或脚本文件作为输入。 可以使用 **Get-Help** 获取有关 **Invoke-Sqlcmd** 及其参数的信息，但是 **Get-Help** 不作用于 **sqlcmd** 查询。  
  
 *-Query* 或 *-QueryFromFile* 输入可以包含：  
  
-   **sqlcmd** 变量和命令。 有关这些变量和命令的信息，请参阅 [sqlcmd Utility](../tools/sqlcmd-utility.md)的“备注”部分。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。 有关 [!INCLUDE[tsql](../includes/tsql-md.md)] 语言的详细信息，请参阅 [TRANSACT-SQL 引用（数据库引擎）](/sql/t-sql/language-reference)。  
  
-   XQuery 语句。 有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支持的 XQuery 语言的详细信息，请参阅 [XQuery 语言参考 (SQL Server)](/sql/xquery/xquery-language-reference-sql-server)。  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>获取 SQL Server cmdlet 的帮助  
 **获取有关 cmdlet 的帮助信息**  
  
-   运行 Get-Help 并且指定 cmdlet 的名称和要返回的帮助级别。  
  
### <a name="example-cmdlet-get-help"></a>示例：cmdlet Get-Help  
 以下示例返回 **Invoke-Sqlcmd**的各个级别的帮助：  
  
```powershell
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>获取提供程序的列表  

### <a name="to-get-a-list-of-active-providers"></a>获取活动提供程序的列表
  
1.  运行 Get-Help 并且指定提供程序类别。  
  
 有关在 Windows PowerShell 中获得提供程序帮助的详细信息，请参阅 [驱动器和提供程序](https://go.microsoft.com/fwlink/?LinkId=102137)。  
  
### <a name="example-get-a-list-of-providers"></a>示例：获取提供程序的列表  
 下面的代码返回当前在 Windows PowerShell 会话中启用的提供程序的列表：  
  
```powershell
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>获取有关 SQL Server 提供程序的帮助  
 **获取有关提供程序的帮助**  
  
1.  运行 Get-Help 并且指定名称 SQLServer  
  
### <a name="example-get-sql-server-provider-help"></a>示例：获取 SQL Server 提供程序帮助  
 此示例将返回有关 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供程序的基本信息：  
  
```powershell
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>列出方法和属性  
 **列出 SQL Server 提供程序路径中的节点的方法和属性**  
  
1.  使用 CD 命令转到 SQL Server 路径中的节点，或创建一个指向该位置的变量集。  
  
2.  运行具有-Type 参数且设置为方法或属性的**Get Member** cmdlet  
  
### <a name="examples-listing-methods-and-properties"></a>示例：列出方法和属性  
 此示例列出 Databases 节点支持的方法：  
  
```powershell
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 此示例列出已经设置为 SMO Table 对象的变量的属性：  
  
```powershell
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell 提供程序](../powershell/sql-server-powershell-provider.md)   
 [使用数据库引擎 cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
