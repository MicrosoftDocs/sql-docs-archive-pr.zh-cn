---
title: 使用语义搜索来查找相似和相关文档 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b11493b5b04fa9308e3afbe56176251225248338
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87591214"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>使用语义搜索来查找相似和相关文档
  说明在为统计语义索引配置的列上如何查找相似或相关的文档或文本值，以及如何查找其相似或相关程度的信息。  
  
##  <a name="finding-similar-or-related-documents"></a><a name="BasicsQuerySimilar"></a>查找相似或相关文档  
  
###  <a name="how-to-find-similar-or-related-documents-with-semanticsimilaritytable"></a><a name="HowToQuerySimilar"></a>如何：通过 SEMANTICSIMILARITYTABLE 查找相似或相关文档  
 若要标识特定列中相似或相关文档，请查询函数 [semanticsimilaritytable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)。  
  
 **SEMANTICSIMILARITYTABLE** 返回一个表，该表由指定列中其内容在语义上类似于指定文档的零个、一个或多个行构成。 可以在 SELECT 语句的 FROM 子句中像引用常规表名那样引用此行集函数。  
  
 不能跨列查询相似的文档。 **SEMANTICSIMILARITYTABLE** 函数只从与源列相同的列检索结果，源列由 **source_key** 参数标识。  
  
 有关 **SEMANTICSIMILARITYTABLE** 函数所需的参数和它返回的结果表的详细信息，请参阅 [semanticsimilaritytable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)。  
  
> [!IMPORTANT]  
>  针对的列必须启用了全文索引和语义索引。  
  
###  <a name="example-find-the-top-documents-that-are-similar-to-another-document"></a><a name="HowToIdentifySimilar"></a>示例：查找与另一个文档类似的顶级文档  
 下面的示例 *@CandidateID* 从 AdventureWorks2012 示例数据库的 humanresources.jobcandidate 表中检索与指定的候选项类似的前10个候选项。  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="finding-information-about-how-documents-are-similar-or-related"></a><a name="BasicsQuerySimilarity"></a>查找有关文档相似或相关程度的信息  
  
###  <a name="how-to-find-information-about-how-documents-are-similar-or-related-with-semanticsimilaritydetailstable"></a><a name="HowToQuerySimilarity"></a>如何：查找有关文档如何与 SEMANTICSIMILARITYDETAILSTABLE 相关的信息或与之相关的信息  
 若要获取使文档相似或相关的关键短语的信息，可以查询函数 [semanticsimilaritydetailstable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)。  
  
 **SEMANTICSIMILARITYDETAILSTABLE** 返回一个表，该表包含其内容在语义上相似的两个文档（源文档和匹配的文档）共有的关键短语的零个、一个或多个行。 可以在 SELECT 语句的 FROM 子句中像引用常规表名那样引用此行集函数。  
  
 有关 **SEMANTICSIMILARITYDETAILSTABLE** 函数所需的参数和它返回的结果表的详细信息，请参阅 [semanticsimilaritydetailstable (Transact-SQL)](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)。  
  
> [!IMPORTANT]  
>  针对的列必须启用了全文索引和语义索引。  
  
###  <a name="example-find-the-top-key-phrases-that-are-similar-between-documents"></a><a name="HowToSimilarPhrases"></a>示例：查找文档之间相似的主要短语  
 以下示例检索 5 个关键短语，它们在 AdventureWorks2012 示例数据库的 **HumanResources.JobCandidate** 表中的两个指定候选人间具有最高的相似性得分。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  
