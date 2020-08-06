---
title: " (SSAS) 连接到 Microsoft SQL Server 并行数据仓库 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlparadatawh.f1
ms.assetid: 98c879ee-7257-40c9-bc85-6766bd3b4885
author: minewiskan
ms.author: owend
ms.openlocfilehash: 082d6b34077d1bde11b527d3bfff907073eed16e
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87579208"
---
# <a name="connect-to-a-microsoft-sql-server-parallel-data-warehouse-ssas"></a>连接到 Microsoft SQL Server Parallel Data Warehouse (SSAS)
  “表导入向导”**** 的这一页可用于指定用于连接到 Microsoft SQL Server Parallel Data Warehouse (PDW) 的设置。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 SQL Server PDW 是一种扩展性很强的工具，它通过大规模并行处理以很低的成本提供高性能。 有关 SQL Server PDW 的详细信息，请参阅网站 [SQL Server 2008 R2 Parallel Data Warehouse](https://go.microsoft.com/fwlink/?LinkId=150895)。 可以使用 SQL Server 身份验证连接到的数据仓库。 若要连接到数据源，必须在计算机上安装适当的访问接口。  
  
> [!NOTE]  
>  在此页中选择数据库时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选数据库中读取，则导入将不会成功。  
  
## <a name="ui-element-list"></a>UI 元素列表  
 **友好的连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **服务器名称**  
 键入要连接到的服务器的名称或 IP 地址。  
  
 **用户名**  
 为数据库连接指定用户名。  
  
 在为数据源构造连接字符串时，将使用该用户名。 在“表格属性”窗口和“导入向导”中预览和筛选数据时，也使用这些凭据。 这些凭据不用于导入或刷新数据；而是使用在“模拟信息”页中指定的 Windows 凭据。  
  
 **密码**  
 为数据库连接指定密码。  
  
 **保存密码**  
 指定是否存储已在“密码”**** 框中输入的密码。  
  
 **数据库名称**  
 从数据库列表中选择数据库。  
  
 **高级**  
 使用 "**设置高级属性**" 对话框设置附加的连接属性。 有关详细信息，请参阅[设置高级属性 (SSAS)](set-advanced-properties-ssas.md)。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  
