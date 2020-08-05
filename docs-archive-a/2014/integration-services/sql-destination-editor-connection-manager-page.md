---
title: SQL 目标编辑器 (连接管理器页) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.connection.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f3a552968cb297de337e1f0c406b444d95dc5a6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87580788"
---
# <a name="sql-destination-editor-connection-manager-page"></a>SQL 目标编辑器（“连接管理器”页）
  可以使用 **“SQL 目标编辑器”** 对话框的 **“连接管理器”** 页，指定数据源信息以及预览结果。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]目标将数据加载到数据库中的表或视图中 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
 若要了解有关 SQL Server 目标的详细信息，请参阅 [SQL Server Destination](data-flow/sql-server-destination.md)。  
  
## <a name="options"></a>选项  
 **“无缓存”**  
 从列表中选择现有连接，或通过单击“新建”**** 创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”  对话框创建新的连接。  
  
 **使用表或视图**  
 从列表中选择现有的表或视图，或单击“新建”**** 创建新的连接。  
  
 **新建**  
 通过使用“创建表”  对话框创建一个新表。  
  
> [!NOTE]  
>  单击 **“新建”** 时， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 将基于所连接的数据源生成一条默认的 CREATE TABLE 语句。 即使源表包含一个已声明了 FILESTREAM 属性的列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。 若要运行具有 FILESTREAM 属性的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 组件，首先要在目标数据库上实现 FILESTREAM 存储。 然后在 **“创建表”** 对话框中将 FILESTREAM 属性添加到 CREATE TABLE 语句中。 有关详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
 **预览**  
 使用“预览查询结果”  对话框预览结果。 预览最多可以显示 200 行。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 目标编辑器 &#40;映射 "页面&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [SQL 目标编辑器 &#40;高级页面&#41;](../../2014/integration-services/sql-destination-editor-advanced-page.md)   
 [使用 SQL Server 目标大容量加载数据](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
