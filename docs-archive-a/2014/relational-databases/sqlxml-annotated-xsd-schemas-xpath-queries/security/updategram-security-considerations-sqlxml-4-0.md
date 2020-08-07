---
title: " (SQLXML 4.0) 的 Updategram 安全注意事项 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
author: rothja
ms.author: jroth
ms.openlocfilehash: eb0319285e6e8cf6e8b3e70f3eb6b9923de06f55
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87589472"
---
# <a name="updategram-security-considerations-sqlxml-40"></a>updategram 的安全注意事项 (SQLXML 4.0)
  以下是使用 updategram 的安全准则：  
  
-   使用 updategram 更新数据时，不要使用默认映射。 如果使用默认映射，则 updategram 中的元素名称会映射到表名称，属性名称会映射到列。 这会公开数据库中的数据库表和列信息，从而可能成为潜在的安全隐患。 相反，如果指定单独的映射架构将 updategram 中的元素和属性映射到数据库表和列，则 updategram 元素和属性名称可以为任意名称，且架构只在必要时才将这些名称映射到数据库表和列。 因此，数据库信息不会在 updategram 中公开。  
  
-   切勿允许用户创建和执行自己的 updategram。 建议将 updategram 作为模板驻留在服务器上，而不是在 ASP 类型应用程序中动态创建 updategram，因为这样可能会给数据库中的数据带来风险。 如果只允许用户通过作为模板提供的 updategram 访问数据，则可避免这种风险。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Updategram 修改 SQLXML 4.0 中的数据](../updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
