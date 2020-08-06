---
title: SQL Server 2014 中不推荐使用的全文搜索功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f03bf6f53652665941e63cf39337085440d0519c
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87689838"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2014"></a>SQL Server 2014 中不推荐使用的全文搜索功能
  本主题说明 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中仍然可用但却不推荐使用的全文搜索功能。 按照计划， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]未来版本将不再具有这些功能。 在新的应用程序中不应使用这些不推荐使用的功能。  
  
 可以使用 **SQL Server:Deprecated Features** 对象性能计数器监视不推荐使用的功能的使用情况并跟踪事件。 有关详细信息，请参阅 [使用 SQL Server 对象](../performance-monitor/use-sql-server-objects.md)。  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>SQL Server 的下一版本中不支持的功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的下一版本将不支持以下全文搜索功能。  
  
|不推荐使用的功能|替代功能|功能名称|功能 ID|  
|------------------------|-----------------|------------------|----------------|  
|FULLTEXTCATALOGPROPERTY 属性：LogSize|无。|FULLTEXTCATALOGPROPERTY** ( "LogSize" ) **|211|  
|FULLTEXTSERVICEPROPERTY 属性：<br /><br /> ConnectTimeout<br /><br /> DataTimeout|无。|FULLTEXTSERVICEPROPERTY** ( "ConnectTimeout" ) **<br /><br /> FULLTEXTSERVICEPROPERTY** ( "DataTimeout"**) |210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service 操作值：clean_up、connect_timeout 和 data_timeout 返回零|无|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|sys.dm_fts_active_catalogs 列：<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> 状态<br /><br /> status_description<br /><br /> worker_count|无。|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|sys.dm_fts_memory_buffers 列：<br /><br /> row_count|无。|dm_fts_memory_buffers.row_count|225|  
|sys.fulltext_catalogs 列：<br /><br /> path<br /><br /> data_space_id<br /><br /> file_id 列|无。|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>SQL Server 未来版本中不支持的功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的下一版本支持以下全文搜索功能，但以后的版本将删除这些功能。 具体是哪一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本现在还未确定。  
  
 **功能名称** 值在跟踪事件中作为 ObjectName，而在性能计数器和 sys.dm_os_performance_counters 中作为实例名称。 **功能 ID** 值在跟踪事件中作为 ObjectId。  
  
|不推荐使用的功能|替代功能|功能名称|功能 ID|  
|------------------------|-----------------|------------------|----------------|  
|CONTAINS 和 CONTAINSTABLE 泛型 NEAR 运算符：<br /><br /> {<simple_term> &#124 <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|自定义 NEAR 运算符：<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,\<distance> [,\<order>] ]<br /><br /> }<br /><br /> )<br /><br /> \<distance> ::= {*integer* &#124; **MAX**}<br /><br /> \<order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|CREATE FULLTEXT CATALOG 选项：<br /><br /> 在路径 "*rootpath*" 中<br /><br /> ON FILEGROUP *filegroup*|无。|CREATE FULLTEXT CATLOG IN PATH<br /><br /> 无。*|237<br /><br /> 内容.<sup>*</sup>|  
|DATABASEPROPERTYEX 属性：IsFullTextEnabled|无。|DATABASEPROPERTYEX** ( "IsFullTextEnabled" ) **|202|  
|sp_detach_db 选项：<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|无。|sp_detach_db @keepfulltextindexfile|226|  
|sp_fulltext_service 操作值：resource_usage 没有函数。|无|sp_fulltext_service @action=resource_usage|200|  
  
 \***SQL Server：弃用的功能**对象不监视在文件组*文件*组上创建全文 CATLOG 的发生次数。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server，不推荐使用的功能对象](../performance-monitor/sql-server-deprecated-features-object.md)   
 [对全文搜索的重大更改](../../database-engine/breaking-changes-to-full-text-search.md)   
 [SQL Server 2014 中不推荐使用的数据库引擎功能](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
