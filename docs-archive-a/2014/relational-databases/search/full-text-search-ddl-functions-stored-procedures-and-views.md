---
title: 全文搜索 DDL、函数、存储过程和视图 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 98c36715-4195-482e-a4a3-d93ff65b75f1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 29b026ac60fd3f7d00ca519c4ced84533ce9740f
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87590145"
---
# <a name="full-text-search-ddl-functions-stored-procedures-and-views"></a>全文搜索 DDL、函数、存储过程和视图
  列出支持全文搜索（包括属性搜索功能）的 Transact-SQL 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象。  
  
 此列表中不包括不推荐使用的对象。  
  
 有关支持语义搜索的数据库对象的列表，请参阅 [Semantic Search DDL, Functions, Stored Procedures, and Views](../views/views.md)。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL 数据定义语言 (DDL) 语句  
  
-   [CREATE FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [CREATE FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [CREATE FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)  
  
-   [CREATE SEARCH PROPERTY LIST (Transact-SQL)](/sql/t-sql/statements/create-search-property-list-transact-sql)  
  
-   [ALTER FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)  
  
-   [ALTER FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
-   [ALTER FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)  
  
-   [ALTER SEARCH PROPERTY LIST (Transact-SQL)](/sql/t-sql/statements/alter-search-property-list-transact-sql)  
  
-   [DROP FULLTEXT CATALOG (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-catalog-transact-sql)  
  
-   [DROP FULLTEXT INDEX (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
-   [DROP FULLTEXT STOPLIST (Transact-SQL)](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
-   [DROP SEARCH PROPERTY LIST (Transact-SQL)](/sql/t-sql/statements/drop-search-property-list-transact-sql)  
  
##  <a name="system-predicates-and-functions"></a><a name="func"></a> 系统谓词和功能  
  
-   [CONTAINS (Transact-SQL)](/sql/t-sql/queries/contains-transact-sql)  
  
-   [CONTAINSTABLE (Transact-SQL)](/sql/relational-databases/system-functions/containstable-transact-sql)  
  
-   [FREETEXT (Transact-SQL)](/sql/t-sql/queries/freetext-transact-sql)  
  
-   [FREETEXTTABLE (Transact-SQL)](/sql/relational-databases/system-functions/freetexttable-transact-sql)  
  
##  <a name="system-metadata-functions"></a><a name="meta"></a> 系统元数据函数  
  
-   [COLUMNPROPERTY (Transact-SQL)](/sql/t-sql/functions/columnproperty-transact-sql)  
  
-   [FULLTEXTCATALOGPROPERTY (Transact-SQL)](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)  
  
-   [FULLTEXTSERVICEPROPERTY (Transact-SQL)](/sql/t-sql/functions/fulltextserviceproperty-transact-sql)  
  
-   [INDEXPROPERTY (Transact-SQL)](/sql/t-sql/functions/indexproperty-transact-sql)  
  
-   [OBJECTPROPERTY (Transact-SQL)](/sql/t-sql/functions/objectpropertyex-transact-sql)  
  
-   [OBJECTPROPERTYEX (Transact-SQL)](/sql/t-sql/functions/objectproperty-transact-sql)  
  
-   [SERVERPROPERTY (Transact-SQL)](/sql/t-sql/functions/serverproperty-transact-sql)  
  
##  <a name="system-stored-procedures"></a><a name="proc"></a> 系统存储过程  
  
-   [sp_fulltext_keymappings (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql)  
  
-   [sp_fulltext_load_thesaurus_file (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql)  
  
-   [sp_fulltext_pendingchanges (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql)  
  
-   [sp_fulltext_service (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)  
  
-   [sp_help_fulltext_system_components (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql)  
  
##  <a name="system-views---catalog-views"></a><a name="cat"></a> 系统视图 - 目录视图  
  
-   [sys.fulltext_catalogs (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)  
  
-   [sys.fulltext_document_types (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)  
  
-   [sys.fulltext_index_catalog_usages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)  
  
-   [sys.fulltext_index_columns (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
-   [sys.fulltext_index_fragments (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)  
  
-   [sys.fulltext_indexes (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)  
  
-   [sys.fulltext_languages (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)  
  
-   [sys.fulltext_stoplists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
-   [sys.fulltext_stopwords (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)  
  
-   [sys.fulltext_system_stopwords (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-fulltext-system-stopwords-transact-sql)  
  
-   [sys.registered_search_properties (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql)  
  
-   [sys.registered_search_property_lists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
##  <a name="system-views---dynamic-management-views"></a><a name="dmv"></a> 系统视图 - 动态管理视图  
  
-   [sys.dm_fts_active_catalogs (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql)  
  
-   [sys.dm_fts_fdhosts (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql)  
  
-   [sys.dm_fts_index_keywords (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)  
  
-   [sys.dm_fts_index_keywords_by_document (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)  
  
-   [sys.dm_fts_index_keywords_by_property (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql)  
  
-   [sys.dm_fts_index_population (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)  
  
-   [sys.dm_fts_memory_buffers (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql)  
  
-   [sys.dm_fts_memory_pools (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql)  
  
-   [sys.dm_fts_outstanding_batches (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql)  
  
-   [sys.dm_fts_parser (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
-   [sys.dm_fts_population_ranges (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql)  
  
  
