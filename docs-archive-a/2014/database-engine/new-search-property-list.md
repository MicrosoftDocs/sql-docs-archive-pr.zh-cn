---
title: 新搜索属性列表 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
author: rothja
ms.author: jroth
ms.openlocfilehash: 48c9e475b380d5f0c7310e33717f261c38acbbd4
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590352"
---
# <a name="new-search-property-list"></a>新建搜索属性列表
  使用此对话框可以创建搜索属性列表。  
  
## <a name="options"></a>选项  
 **搜索属性列表名称**  
 输入搜索属性列表的名称。  
  
 **所有者**  
 指定搜索属性列表的所有者。 如果希望将所有权分配给您自己（即分配给当前用户），请将此字段留空。 若要指定另一个用户，请单击浏览按钮。  
  
### <a name="create-search-property-list-options"></a>创建搜索属性列表选项  
 单击下列选项之一：  
  
 **创建空的搜索属性列表**  
 创建一个没有任何属性的搜索属性列表。  
  
 **从现有搜索属性列表创建**  
 将现有搜索属性列表复制到到新的属性列表。 搜索属性列表是数据库对象，因此，您必须指定包含要复制的属性列表的数据库。  
  
 **源数据库**  
 指定现有搜索属性列表所属的数据库的名称。 默认情况下选择当前数据库。 （可选）如果当前连接与该数据库中的用户 ID 相关联，您可以使用列表框来选择其他数据库。  
  
 **源搜索属性列表**  
 从属于所选数据库的搜索属性列表中选择一个现有搜索属性列表的名称。  
  
## <a name="permissions"></a>权限  
 请参阅[CREATE SEARCH PROPERTY LIST &#40;transact-sql&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)。  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>使用 SQL Server Management Studio 管理搜索属性列表  
 有关如何创建、查看、更改或删除搜索属性列表以及如何为属性搜索配置全文索引的信息，请参阅 [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;创建搜索属性列表](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [用搜索属性列表搜索文档属性](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
