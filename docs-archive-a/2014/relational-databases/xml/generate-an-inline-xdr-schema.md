---
title: 生成内联 XDR 架构 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e2bb7b4b482b79ab5550540dd5b24ffdd8d6636
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694375"
---
# <a name="generate-an-inline-xdr-schema"></a>生成内联 XDR 架构
  FOR XML 中的 **XMLDATA** 指令将返回一个内联 XDR 架构以及查询结果。 但是，XDR 架构不支持 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本中引入的所有新数据类型和其他增强功能。 您可以改为使用 [XMLSCHEMA](generate-an-inline-xsd-schema.md)指令来请求内联 XSD 架构。  
  
> [!IMPORTANT]  
>  不推荐使用 FOR XML 选项的 XMLDATA 指令。 如果是 RAW 和 AUTO 模式，请使用 XSD 生成。 在 EXPLICIT 模式下，没有 XMLDATA 指令的替代项。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 另请注意关于内联 XDR 架构支持的以下信息：  
  
-   如果 FOR XML 查询结果包括 **xml** 类型的列，而您请求内联 XDR 架构，将返回错误。 内联 XDR 不支持这些类型。  
  
-   **(n)varchar(max)** 和 **(n)varbinary(max)** 类型将分别映射到 **(n)varchar(n)** 和 **varbinary(n)** 。  
  
-   如果兼容模式设置为 90 或更高的值，则 **timestamp** 值将被视为 **varbinary(8)** 数据，并作为二进制数据来处理，然后按以下方式返回结果：  
  
    -   如果指定了 **binary base64** ，则使用 Base 64 编码。  
  
    -   如果未指定 **binary base64** ，则在 AUTO 模式中使用 URL 编码。  
  
  
