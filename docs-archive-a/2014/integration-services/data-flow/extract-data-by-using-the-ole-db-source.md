---
title: 使用 OLE DB 源提取数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 352d62cc66e3f17fb10839086e7ee9c5307f1a17
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87694053"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>使用 OLE DB 源提取数据
  若要添加并配置 OLE DB 源，包必须已包含至少一个数据流任务。  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>使用 OLE DB 源提取数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 中将 OLE DB 源拖动到设计图面。  
  
4.  双击此 OLE DB 源。  
  
5.  在 **“OLE DB 源编辑器”** 对话框中的 **“连接管理器”** 页上，选择现有的 OLE DB 连接管理器，或单击 **“新建”** 创建新的连接管理器。 有关详细信息，请参阅 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
6.  选择数据访问方法：  
  
    -   **“表或视图”** 在 OLE DB 连接管理器连接到的数据库中，选择表或视图。  
  
    -   **表名变量或视图名变量** 在 OLE DB 连接管理器连接到的数据库中，选择包含表名称或视图名称的用户定义变量。  
  
    -   **SQL 命令** 键入 SQL 命令或单击 **“生成查询”** ，以使用 **“查询生成器”** 编写 SQL 命令。  
  
        > [!NOTE]  
        >  此命令可以包含参数。 有关详细信息，请参阅 [将查询参数映射到数据流组件中的变量](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
    -   **变量中的 SQL 命令** 选择包含 SQL 命令的用户定义变量。  
  
        > [!NOTE]  
        >  这些变量必须在包含 OLE DB 源的同一个数据流任务的作用域内定义，或在同一个包的作用域内定义；此外，变量的数据类型还必须为字符串。  
  
7.  若要更新外部列和输出列之间的映射，请单击 **“列”** ，并在 **“外部列”** 列表中选择其他列。  
  
8.  也可以通过编辑 **“输出列”** 列表中的值来更新输出列的名称。  
  
9. 若要配置错误输出，请单击 **“错误输出”** 。 有关详细信息，请参阅 [在数据流组件中配置错误输出](../configure-an-error-output-in-a-data-flow-component.md)。  
  
10. 可以单击 **“预览”** ，查看最多 200 行 OLE DB 源所提取的数据。  
  
11. 单击“确定”。   
  
12. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 源](ole-db-source.md)   
 [Integration Services 转换](transformations/integration-services-transformations.md)   
 [Integration Services 路径](integration-services-paths.md)   
 [数据流任务](../control-flow/data-flow-task.md)  
  
  
