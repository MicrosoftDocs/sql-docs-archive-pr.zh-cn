---
title: 对 SQL Server 标识符进行编码和解码 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 88e7ebbc81d9c3cb91b1bf678075c5b5d0884890
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87687951"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>对 SQL Server 标识符进行编码和解码
  SQL Server 分隔标识符有时候包含 Windows PowerShell 路径名称中不支持的字符。 可以通过对其十六进制值进行编码来指定这些字符。  
  
1.  **开始之前：**  [限制和局限](#LimitationsRestrictions)  
  
2.  **处理特殊字符：**  [对标识符进行编码](#EncodeIdent)、 [对标识符进行解码](#DecodeIdent)  
  
## <a name="before-you-begin"></a>开始之前  
 对于 Windows PowerShell 路径名称中不支持的字符，可以表示或编码为 "%" 字符，后跟代表该字符的位模式的十六进制值，如 "xx" 中所示 **%** 。 对于 Windows PowerShell 路径中不支持的字符，始终可以使用编码来处理字符。  
  
 **Encode-SqlName** cmdlet 将 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 标识符作为输入。 它输出一个字符串，其中包含所有不受 Windows PowerShell 语言支持且已经用“%xx”编码的字符。 **Decode-SqlName** cmdlet 将经过编码的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 标识符作为输入并返回初始标识符。  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
 `Encode-Sqlname` 和 `Decode-Sqlname` cmdlet 仅对 SQL Server 分隔标识符中允许、但在 PowerShell 路径中不支持的字符进行编码和解码。 下面是可通过 **Encode-SqlName** 编码并可通过 **Decode-SqlName**解码的字符：  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**字符**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**十六进制编码**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="encoding-an-identifier"></a><a name="EncodeIdent"></a> 对标识符进行编码  
 **对 PowerShell 路径中的 SQL Server 标识符进行编码**  
  
-   使用以下两种方法之一对 SQL Server 标识符进行编码：  
  
    -   使用语法 %XX（其中，XX 是十六进制代码）为不支持的字符指定十六进制代码。  
  
    -   将标识符以带引号的字符串的形式传递到 `Encode-Sqlname` cmdlet  
  
### <a name="examples-encoding"></a>示例（编码）  
 此示例指定“:”字符 (%3A) 的编码版本：  
  
```  
Set-Location Table%3ATest  
```  
  
 或者，可以使用 **Encode-SqlName** 生成受 Windows PowerShell 支持的名称：  
  
```powershell
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="decoding-an-identifier"></a><a name="DecodeIdent"></a>对标识符进行解码  
 **对 PowerShell 路径中的 SQL Server 标识符进行解码**  
  
 使用 `Decode-Sqlname` cmdlet 可用编码表示的字符替代十六进制编码。  
  
### <a name="examples-decoding"></a>示例（解码）  
 下面的示例返回“Table:Test”：  
  
```powershell
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server PowerShell 中的标识符](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供程序](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
