---
title: 指定架构选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52064cc189dc62152814436d2d11326a74c89ff6
ms.sourcegitcommit: ad4d92dce894592a259721a1571b1d8736abacdb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87691178"
---
# <a name="specify-schema-options"></a>指定架构选项
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中指定架构选项。 在发布表或视图时，可以控制为发布的对象复制的对象创建选项。 创建项目时可以设置这些选项，还可以在以后更改它们。 如果没有为某项目显式指定这些选项，将定义默认的选项集。  
  
> [!NOTE]  
>  使用复制存储过程时的默认架构选项可能与使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]添加项目时的默认选项不同。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **指定架构选项，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制和局限  
  
-   如果在创建发布后更改架构选项，则必须生成新的快照。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建议  
  
-   有关架构选项的完整列表，请参阅 sp_addarticle 的** \@ schema_option**参数[&#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)和[sp_addmergearticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在“项目属性 - \<Article>”对话框的“属性”选项卡上指定架构选项，例如是否将约束和触发器复制到订阅服务器 。 此选项卡可在新建发布向导和“发布属性 - \<Publication>”对话框中获得。 有关如何使用该向导和如何访问该对话框的详细信息，请参阅[创建发布](create-a-publication.md)和[查看和修改发布属性](view-and-modify-publication-properties.md)。  
  
#### <a name="to-specify-schema-options"></a>指定架构选项  
  
1.  在“新建发布”向导或“发布属性 - \<Publication>”对话框的“项目”页面上，选择一个项目，然后单击“项目属性”  。  
  
2.  选择要将架构选项更改应用于哪些项目：  
  
    -   单击“设置突出显示的 \<ObjectType> 项目的属性”以启动“项目属性 - \<ObjectName>”对话框；在此对话框中进行的属性更改仅应用于在“项目”页上的对象窗格中突出显示的对象。    
  
    -   单击“设置所有 \<ObjectType> 项目的属性”以启动“所有 \<ObjectType> 项目的属性”对话框；在此对话框中进行的属性更改应用于“项目”页面上对象窗格中该类型的所有对象，包括尚未选择进行发布的对象  。  
  
        > [!NOTE]  
        >  在“所有 \<ObjectType> 项目的属性”对话框中进行的属性更改会替代之前在“项目属性 - \<ObjectName>”对话框中进行的任何更改。  例如，若要为某对象类型的所有项目设置一些默认值，但还希望为单个对象设置一些属性，请首先设置所有项目的默认值。 然后再设置单个对象的属性。  
  
3.  在“项目属性 - \<Article>”对话框的“属性”选项卡的“将对象和设置复制到订阅服务器”和“目标对象”部分中，为各选项指定值   。  
  
4.  根据需要修改属性，然后单击 **“确定”** 。  
  
5.  如果处于“发布属性 - \<Publication>”对话框中，请单击“确定”以保存并关闭该对话框 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 架构选项指定为十六进制值，该值为一个或多个选项的 [|（位或）](/sql/t-sql/language-elements/bitwise-or-transact-sql) 结果。 有关详细信息，请参阅 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 和 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。  
  
> [!NOTE]  
>  必须先将架构选项值从 **binary** 转换为 **int** ，才能执行位运算。 有关详细信息，请参阅 [CAST 和 CONVERT (Transact-SQL)](/sql/t-sql/functions/cast-and-convert-transact-sql)。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>为快照或事务发布定义项目时指定架构选项  
  
1.  在发布服务器上，对发布数据库执行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 指定项目所属的**发布的名称、项目 \@ ** ** \@ 的**名称、要发布的数据库对象** \@ source_object**、 ** \@ 类型**的数据库对象类型，以及** \@ schema_option**的一个或多个架构选项的[| (位或) ](/sql/t-sql/language-elements/bitwise-or-transact-sql)结果。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>为合并发布定义项目时指定架构选项  
  
1.  在发布服务器上，对发布数据库执行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 指定项目所属的**发布的名称、项目 \@ **的名称、要为** \@ source_object**发布的数据库对象， ** \@ **以及** \@ Schema_option**的一个或多个架构选项的[| (按位或) ](/sql/t-sql/language-elements/bitwise-or-transact-sql)结果。 有关详细信息，请参阅 [定义项目](define-an-article.md)。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>更改快照发布或事务发布中的现有项目的架构选项  
  
1.  在发布服务器上，对发布数据库执行 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql)。 指定项目所属的** \@ 发布的名称，并指定** ** \@ 项目的项目名称。** 记下结果集中 **schema_option** 列的值。  
  
2.  使用步骤 1 中的值和所需的架构选项值执行 [&（按位与）](/sql/t-sql/language-elements/bitwise-and-transact-sql)运算，以确定是否设置了此选项。  
  
    -   如果结果为 **0**，则表示未设置此选项。  
  
    -   如果结果为选项值，则表示已设置此选项。  
  
3.  如果未设置此选项，则使用步骤 1 中的值和所需的架构选项值执行 [|（位或）](/sql/t-sql/language-elements/bitwise-or-transact-sql) 运算。  
  
4.  在发布服务器上，对发布数据库执行 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)。 指定项目所属的**发布的名称、项目 \@ ** ** \@ 的项目名称、** ** \@ 属性**的**schema_option**的值，以及** \@ 值**的步骤3中的十六进制结果。  
  
5.  运行快照代理以生成新快照。 有关详细信息，请参阅 [创建并应用初始快照](../create-and-apply-the-initial-snapshot.md)。  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>为合并发布中的现有项目更改架构选项  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)。 指定项目所属的** \@ 发布的名称，并指定** ** \@ 项目的项目名称。** 记下结果集中 **schema_option** 列的值。  
  
2.  使用步骤 1 中的值和所需的架构选项值执行 [&（按位与）](/sql/t-sql/language-elements/bitwise-and-transact-sql)运算，以确定是否设置了此选项。  
  
    -   如果结果为 **0**，则表示未设置此选项。  
  
    -   如果结果为选项值，则表示已设置此选项。  
  
3.  如果未设置此选项，则使用步骤 1 中的值和所需的架构选项值执行 [|（位或）](/sql/t-sql/language-elements/bitwise-or-transact-sql) 运算。  
  
4.  在发布服务器上，对发布数据库执行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)。 指定项目所属的**发布的名称、项目 \@ ** ** \@ 的项目名称、** ** \@ 属性**的**schema_option**的值，以及** \@ 值**的步骤3中的十六进制结果。  
  
5.  运行快照代理以生成新快照。 有关详细信息，请参阅 [创建并应用初始快照](../create-and-apply-the-initial-snapshot.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../transactional/article-options-for-transactional-replication.md)  
  
  
